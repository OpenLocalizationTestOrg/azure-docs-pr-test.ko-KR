---
title: "aaaSplit 병합 보안 구성 | Microsoft Docs"
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
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="6f2b9-103">분할-병합 보안 구성</span><span class="sxs-lookup"><span data-stu-id="6f2b9-103">Split-merge security configuration</span></span>
<span data-ttu-id="6f2b9-104">toouse hello 분할/병합 서비스 올바르게 보안을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-104">toouse hello Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="6f2b9-105">hello 서비스는 Microsoft Azure SQL 데이터베이스의 탄력적인 크기 조정 기능은 hello의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-105">hello service is part of hello Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="6f2b9-106">자세한 내용은 [탄력적인 확장 분할 및 병합 서비스 자습서](sql-database-elastic-scale-configure-deploy-split-and-merge.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="6f2b9-107">인증서 구성</span><span class="sxs-lookup"><span data-stu-id="6f2b9-107">Configuring certificates</span></span>
<span data-ttu-id="6f2b9-108">인증서는 두 가지 방법으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="6f2b9-109">tooConfigure hello SSL 인증서</span><span class="sxs-lookup"><span data-stu-id="6f2b9-109">tooConfigure hello SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="6f2b9-110">tooConfigure 클라이언트 인증서</span><span class="sxs-lookup"><span data-stu-id="6f2b9-110">tooConfigure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a><span data-ttu-id="6f2b9-111">tooobtain 인증서</span><span class="sxs-lookup"><span data-stu-id="6f2b9-111">tooobtain certificates</span></span>
<span data-ttu-id="6f2b9-112">Hello 또는 공용 ca (인증 기관)에서 인증서를 구할 수 [Windows 인증서 서비스](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-112">Certificates can be obtained from public Certificate Authorities (CAs) or from hello [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="6f2b9-113">이들은 기본 hello 메서드 tooobtain 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-113">These are hello preferred methods tooobtain certificates.</span></span>

<span data-ttu-id="6f2b9-114">이러한 옵션을 사용할 수 없는 경우 **자체 서명된 인증서**를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-toogenerate-certificates"></a><span data-ttu-id="6f2b9-115">도구 toogenerate 인증서</span><span class="sxs-lookup"><span data-stu-id="6f2b9-115">Tools toogenerate certificates</span></span>
* [<span data-ttu-id="6f2b9-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="6f2b9-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="6f2b9-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="6f2b9-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a><span data-ttu-id="6f2b9-118">toorun hello 도구</span><span class="sxs-lookup"><span data-stu-id="6f2b9-118">toorun hello tools</span></span>
* <span data-ttu-id="6f2b9-119">Visual Studio용 개발자 명령 프롬프트에서 [Visual Studio 명령 프롬프트를 참조하세요](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="6f2b9-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="6f2b9-120">설치되어 있는 경우 다음으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="6f2b9-121">가져오기 WDK에서 hello [Windows 8.1: 키트 및 도구 다운로드](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="6f2b9-121">Get hello WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="tooconfigure-hello-ssl-certificate"></a><span data-ttu-id="6f2b9-122">tooconfigure hello SSL 인증서</span><span class="sxs-lookup"><span data-stu-id="6f2b9-122">tooconfigure hello SSL certificate</span></span>
<span data-ttu-id="6f2b9-123">SSL 인증서는 필요한 tooencrypt hello 통신 하 고 hello 서버 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-123">A SSL certificate is required tooencrypt hello communication and authenticate hello server.</span></span> <span data-ttu-id="6f2b9-124">아래 세 가지 시나리오 hello 중 가장 적합 hello 선택한 모든 단계를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-124">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="6f2b9-125">자체 서명된 새로운 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="6f2b9-126">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="6f2b9-127">자체 서명된 SSL 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="6f2b9-128">SSL 인증서 tooCloud 서비스 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-128">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="6f2b9-129">서비스 구성 파일에서 SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f2b9-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="6f2b9-130">SSL 인증 기관 가져오기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="6f2b9-131">toouse hello 인증서에서 기존 인증서 저장</span><span class="sxs-lookup"><span data-stu-id="6f2b9-131">toouse an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="6f2b9-132">인증서 저장소에서 SSL 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="6f2b9-133">SSL 인증서 tooCloud 서비스 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-133">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="6f2b9-134">서비스 구성 파일에서 SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f2b9-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="6f2b9-135">toouse PFX 파일에 기존 인증서</span><span class="sxs-lookup"><span data-stu-id="6f2b9-135">toouse an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="6f2b9-136">SSL 인증서 tooCloud 서비스 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-136">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="6f2b9-137">서비스 구성 파일에서 SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f2b9-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a><span data-ttu-id="6f2b9-138">tooconfigure 클라이언트 인증서</span><span class="sxs-lookup"><span data-stu-id="6f2b9-138">tooconfigure client certificates</span></span>
<span data-ttu-id="6f2b9-139">주문 tooauthenticate 요청 toohello 서비스에서 클라이언트 인증서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-139">Client certificates are required in order tooauthenticate requests toohello service.</span></span> <span data-ttu-id="6f2b9-140">아래 세 가지 시나리오 hello 중 가장 적합 hello 선택한 모든 단계를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-140">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="6f2b9-141">클라이언트 인증서 해제</span><span class="sxs-lookup"><span data-stu-id="6f2b9-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="6f2b9-142">클라이언트 인증서 기반 인증 해제</span><span class="sxs-lookup"><span data-stu-id="6f2b9-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="6f2b9-143">자체 서명된 새로운 클라이언트 인증서 발급</span><span class="sxs-lookup"><span data-stu-id="6f2b9-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="6f2b9-144">자체 서명된 인증 기관 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="6f2b9-145">CA 인증서 tooCloud 서비스 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-145">Upload CA Certificate tooCloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="6f2b9-146">서비스 구성 파일의 CA 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f2b9-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="6f2b9-147">클라이언트 인증서 발급</span><span class="sxs-lookup"><span data-stu-id="6f2b9-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="6f2b9-148">클라이언트 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="6f2b9-149">클라이언트 인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="6f2b9-150">클라이언트 인증서 지문 복사</span><span class="sxs-lookup"><span data-stu-id="6f2b9-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="6f2b9-151">Hello 서비스 구성 파일에서에서 허용 하는 클라이언트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-151">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="6f2b9-152">기존 클라이언트 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="6f2b9-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="6f2b9-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="6f2b9-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="6f2b9-154">CA 인증서 tooCloud 서비스 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-154">Upload CA Certificate tooCloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="6f2b9-155">서비스 구성 파일의 CA 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f2b9-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="6f2b9-156">클라이언트 인증서 지문 복사</span><span class="sxs-lookup"><span data-stu-id="6f2b9-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="6f2b9-157">Hello 서비스 구성 파일에서에서 허용 하는 클라이언트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-157">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="6f2b9-158">클라이언트 인증서 해지 확인 구성</span><span class="sxs-lookup"><span data-stu-id="6f2b9-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="6f2b9-159">허용된 IP 주소</span><span class="sxs-lookup"><span data-stu-id="6f2b9-159">Allowed IP addresses</span></span>
<span data-ttu-id="6f2b9-160">액세스 toohello 서비스 끝점의 IP 주소 범위를 제한 된 toospecific 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-160">Access toohello service endpoints can be restricted toospecific ranges of IP addresses.</span></span>

## <a name="tooconfigure-encryption-for-hello-store"></a><span data-ttu-id="6f2b9-161">hello 저장소에 대 한 tooconfigure 암호화</span><span class="sxs-lookup"><span data-stu-id="6f2b9-161">tooconfigure encryption for hello store</span></span>
<span data-ttu-id="6f2b9-162">인증서는 필수 tooencrypt hello 자격 증명을 hello 메타 데이터 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-162">A certificate is required tooencrypt hello credentials that are stored in hello metadata store.</span></span> <span data-ttu-id="6f2b9-163">아래 세 가지 시나리오 hello 중 가장 적합 hello 선택한 모든 단계를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-163">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="6f2b9-164">자체 서명된 새로운 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="6f2b9-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="6f2b9-165">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="6f2b9-166">자체 서명된 암호화 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="6f2b9-167">암호화 인증서 tooCloud 서비스 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-167">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="6f2b9-168">서비스 구성 파일에서 암호화 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f2b9-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="6f2b9-169">Hello 인증서 저장소에서 기존 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-169">Use an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="6f2b9-170">인증서 저장소에서 암호화 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="6f2b9-171">암호화 인증서 tooCloud 서비스 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-171">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="6f2b9-172">서비스 구성 파일에서 암호화 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f2b9-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="6f2b9-173">PFX 파일에서 기존 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="6f2b9-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="6f2b9-174">암호화 인증서 tooCloud 서비스 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-174">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="6f2b9-175">서비스 구성 파일에서 암호화 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f2b9-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a><span data-ttu-id="6f2b9-176">hello 기본 구성</span><span class="sxs-lookup"><span data-stu-id="6f2b9-176">hello default configuration</span></span>
<span data-ttu-id="6f2b9-177">hello 기본 구성은 모든 액세스 toohello HTTP 끝점을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-177">hello default configuration denies all access toohello HTTP endpoint.</span></span> <span data-ttu-id="6f2b9-178">이 hello hello 요청 toothese 끝점 데이터베이스 자격 증명 등과 같은 기밀 정보를 전달할 수 있으므로 권장 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-178">This is hello recommended setting, since hello requests toothese endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="6f2b9-179">hello 기본 구성은 모든 액세스 toohello HTTPS 끝점을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-179">hello default configuration allows all access toohello HTTPS endpoint.</span></span> <span data-ttu-id="6f2b9-180">이 설정을 추가로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-180">This setting may be restricted further.</span></span>

### <a name="changing-hello-configuration"></a><span data-ttu-id="6f2b9-181">Hello 구성 변경</span><span class="sxs-lookup"><span data-stu-id="6f2b9-181">Changing hello Configuration</span></span>
<span data-ttu-id="6f2b9-182">hello tooand 끝점 적용 되는 액세스 제어 규칙의 그룹에에서 구성 된 hello  **<EndpointAcls>**  hello 섹션인 **서비스 구성 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-182">hello group of access control rules that apply tooand endpoint are configured in hello **<EndpointAcls>** section in hello **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="6f2b9-183">액세스 제어 그룹에서 hello 규칙에 구성 된는 <AccessControl name=""> hello 서비스 구성 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-183">hello rules in an access control group are configured in a <AccessControl name=""> section of hello service configuration file.</span></span> 

<span data-ttu-id="6f2b9-184">hello 형식 설명서 네트워크 액세스 제어 목록에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-184">hello format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="6f2b9-185">예를 들어 tooallow hello 범위 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS 끝점의 유일한 Ip hello 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-185">For example, tooallow only IPs in hello range 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint, hello rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="6f2b9-186">서비스 거부 방지</span><span class="sxs-lookup"><span data-stu-id="6f2b9-186">Denial of service prevention</span></span>
<span data-ttu-id="6f2b9-187">다른 두 가지 메커니즘 toodetect 지원 및 서비스 거부 공격을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-187">There are two different mechanisms supported toodetect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="6f2b9-188">원격 호스트당 동시 요청 수 제한(기본적으로 해제됨)</span><span class="sxs-lookup"><span data-stu-id="6f2b9-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="6f2b9-189">원격 호스트당 액세스 속도 제한(기본적으로 설정됨)</span><span class="sxs-lookup"><span data-stu-id="6f2b9-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="6f2b9-190">이 기능을 기반으로 hello IIS에서 동적 IP 보안에서 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-190">These are based on hello features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="6f2b9-191">때 hello 요소 뒤의 조심이 구성 변경:</span><span class="sxs-lookup"><span data-stu-id="6f2b9-191">When changing this configuration beware of hello following factors:</span></span>

* <span data-ttu-id="6f2b9-192">프록시 및 네트워크 주소 변환 장치 hello 원격 호스트 정보에 대해의 hello 동작</span><span class="sxs-lookup"><span data-stu-id="6f2b9-192">hello behavior of proxies and Network Address Translation devices over hello remote host information</span></span>
* <span data-ttu-id="6f2b9-193">Hello 웹 역할에서 각 요청 tooany 리소스 (예: 스크립트, 이미지 등 로드) 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-193">Each request tooany resource in hello web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="6f2b9-194">동시 액세스 수 제한</span><span class="sxs-lookup"><span data-stu-id="6f2b9-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="6f2b9-195">이 동작을 구성 하는 hello 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-195">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="6f2b9-196">이 보호 DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-196">Change DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="6f2b9-197">액세스 속도 제한</span><span class="sxs-lookup"><span data-stu-id="6f2b9-197">Restricting rate of access</span></span>
<span data-ttu-id="6f2b9-198">이 동작을 구성 하는 hello 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-198">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a><span data-ttu-id="6f2b9-199">Hello 응답 tooa 구성 요청을 거부 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-199">Configuring hello response tooa denied request</span></span>
<span data-ttu-id="6f2b9-200">hello 다음 설정을 구성 합니다 hello 응답 tooa를 요청을 거부 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-200">hello following setting configures hello response tooa denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="6f2b9-201">IIS에서 동적 IP 보안에 대 한 기타 지원 되는 값에 대 한 toohello 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-201">Refer toohello documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="6f2b9-202">서비스 인증서 구성 작업</span><span class="sxs-lookup"><span data-stu-id="6f2b9-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="6f2b9-203">이 항목은 참조용일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-203">This topic is for reference only.</span></span> <span data-ttu-id="6f2b9-204">에 설명 된 hello 구성 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-204">Please follow hello configuration steps outlined in:</span></span>

* <span data-ttu-id="6f2b9-205">Hello SSL 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="6f2b9-205">Configure hello SSL certificate</span></span>
* <span data-ttu-id="6f2b9-206">클라이언트 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="6f2b9-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="6f2b9-207">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-207">Create a self-signed certificate</span></span>
<span data-ttu-id="6f2b9-208">다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="6f2b9-209">toocustomize:</span><span class="sxs-lookup"><span data-stu-id="6f2b9-209">toocustomize:</span></span>

* <span data-ttu-id="6f2b9-210">-n hello로 서비스 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-210">-n with hello service URL.</span></span> <span data-ttu-id="6f2b9-211">와일드카드("CN=*.cloudapp.net") 및 대체 이름("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net")이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="6f2b9-212">-e hello 인증서 만료 날짜와 함께 강력한 암호를 만들고 대화 상자가 나타나면이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-212">-e with hello certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="6f2b9-213">자체 서명된 SSL 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="6f2b9-214">다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="6f2b9-215">암호를 입력하고 다음 옵션을 사용하여 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="6f2b9-216">예, hello 개인 키를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-216">Yes, export hello private key</span></span>
* <span data-ttu-id="6f2b9-217">확장된 속성 모두 내보내기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="6f2b9-218">인증서 저장소에서 SSL 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="6f2b9-219">인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-219">Find certificate</span></span>
* <span data-ttu-id="6f2b9-220">작업-> 모든 작업 -> 내보내기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="6f2b9-221">다음 옵션을 사용하여 .PFX 파일로 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="6f2b9-222">예, hello 개인 키를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-222">Yes, export hello private key</span></span>
  * <span data-ttu-id="6f2b9-223">가능 하면 hello 인증 경로 있는 모든 인증서를 포함 * 모든 확장된 속성을 내보내려면</span><span class="sxs-lookup"><span data-stu-id="6f2b9-223">Include all certificates in hello certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-toocloud-service"></a><span data-ttu-id="6f2b9-224">SSL 인증서 toocloud 서비스 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-224">Upload SSL certificate toocloud service</span></span>
<span data-ttu-id="6f2b9-225">기존 컨트롤이 나 생성 hello로 인증서를 업로드 합니다. PFX 파일 hello SSL 키 쌍을 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-225">Upload certificate with hello existing or generated .PFX file with hello SSL key pair:</span></span>

* <span data-ttu-id="6f2b9-226">Hello 개인 키 정보를 보호 하는 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-226">Enter hello password protecting hello private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="6f2b9-227">서비스 구성 파일에서 SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f2b9-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="6f2b9-228">Hello 업로드 한 인증서 toohello 클라우드 서비스의 hello 문으로 hello 서비스 구성 파일의 설정에 따라 hello의 hello 지문 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-228">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="6f2b9-229">SSL 인증 기관 가져오기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-229">Import SSL certification authority</span></span>
<span data-ttu-id="6f2b9-230">Hello 서비스와 통신 하는 모든 계정/컴퓨터에서 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-230">Follow these steps in all account/machine that will communicate with hello service:</span></span>

* <span data-ttu-id="6f2b9-231">Hello를 두 번 클릭 합니다. Windows 탐색기에서 CER 파일</span><span class="sxs-lookup"><span data-stu-id="6f2b9-231">Double-click hello .CER file in Windows Explorer</span></span>
* <span data-ttu-id="6f2b9-232">Hello 인증서 대화 상자에 인증서 설치를 클릭 하십시오...</span><span class="sxs-lookup"><span data-stu-id="6f2b9-232">In hello Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="6f2b9-233">Hello 신뢰할 수 있는 루트 인증 기관 저장소로 인증서를 가져옵니다</span><span class="sxs-lookup"><span data-stu-id="6f2b9-233">Import certificate into hello Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="6f2b9-234">클라이언트 인증서 기반 인증 해제</span><span class="sxs-lookup"><span data-stu-id="6f2b9-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="6f2b9-235">사용 하지 않는 것을 사용 하면 공용 액세스 toohello 서비스 끝점에 대해 다른 메커니즘 (예: Microsoft Azure 가상 네트워크)에 도달 하지 못할 경우 및 클라이언트 인증서 기반 인증만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-235">Only client certificate-based authentication is supported and disabling it will allow for public access toohello service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="6f2b9-236">Hello 서비스 구성 파일 tooturn hello 기능에서 이러한 설정을 toofalse 해제 변경:</span><span class="sxs-lookup"><span data-stu-id="6f2b9-236">Change these settings toofalse in hello service configuration file tooturn hello feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="6f2b9-237">그런 다음 CA hello 인증서 설정에 hello hello SSL로 동일한 지문이 인증서를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-237">Then, copy hello same thumbprint as hello SSL certificate in hello CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="6f2b9-238">자체 서명된 인증 기관 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="6f2b9-239">다음 단계 toocreate 인증 기관으로 자체 서명 된 인증서 tooact hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-239">Execute hello following steps toocreate a self-signed certificate tooact as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="6f2b9-240">toocustomize 것</span><span class="sxs-lookup"><span data-stu-id="6f2b9-240">toocustomize it</span></span>

* <span data-ttu-id="6f2b9-241">-e hello 인증 만료 날짜와 함께</span><span class="sxs-lookup"><span data-stu-id="6f2b9-241">-e with hello certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="6f2b9-242">CA 공개 키 찾기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-242">Find CA public key</span></span>
<span data-ttu-id="6f2b9-243">모든 클라이언트 인증서 hello 서비스에서 신뢰할 수 있는 인증 기관에서 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-243">All client certificates must have been issued by a Certification Authority trusted by hello service.</span></span> <span data-ttu-id="6f2b9-244">Hello 공개 키 toohello toobe가는 hello 클라이언트 인증서를 발급 한 인증 기관을 인증에에서 사용 되 순서 tooupload 것 toohello 클라우드 서비스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-244">Find hello public key toohello Certification Authority that issued hello client certificates that are going toobe used for authentication in order tooupload it toohello cloud service.</span></span>

<span data-ttu-id="6f2b9-245">Hello 파일 hello 공개 키로 사용할 수 없는 경우 hello 인증서 저장소에서 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-245">If hello file with hello public key is not available, export it from hello certificate store:</span></span>

* <span data-ttu-id="6f2b9-246">인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-246">Find certificate</span></span>
  * <span data-ttu-id="6f2b9-247">발급 한 클라이언트 인증서에 대 한 검색 hello 같은 인증 기관</span><span class="sxs-lookup"><span data-stu-id="6f2b9-247">Search for a client certificate issued by hello same Certification Authority</span></span>
* <span data-ttu-id="6f2b9-248">Hello 인증서를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-248">Double-click hello certificate.</span></span>
* <span data-ttu-id="6f2b9-249">Hello 인증서 대화 상자에서 hello 인증 경로 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-249">Select hello Certification Path tab in hello Certificate dialog.</span></span>
* <span data-ttu-id="6f2b9-250">Hello 경로에 hello CA 항목을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-250">Double-click hello CA entry in hello path.</span></span>
* <span data-ttu-id="6f2b9-251">Hello 인증서 속성을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-251">Take notes of hello certificate properties.</span></span>
* <span data-ttu-id="6f2b9-252">닫기 hello **인증서** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-252">Close hello **Certificate** dialog.</span></span>
* <span data-ttu-id="6f2b9-253">인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-253">Find certificate</span></span>
  * <span data-ttu-id="6f2b9-254">위에서 언급 한 CA hello에 대 한 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-254">Search for hello CA noted above.</span></span>
* <span data-ttu-id="6f2b9-255">작업-> 모든 작업 -> 내보내기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="6f2b9-256">다음 옵션을 사용하여 .CER 파일로 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="6f2b9-257">**아니요, hello 개인 키를 내보내지 않습니다**</span><span class="sxs-lookup"><span data-stu-id="6f2b9-257">**No, do not export hello private key**</span></span>
  * <span data-ttu-id="6f2b9-258">가능 하면 hello 인증 경로 있는 모든 인증서를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-258">Include all certificates in hello certification path if possible.</span></span>
  * <span data-ttu-id="6f2b9-259">확장된 속성 모두 내보내기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-toocloud-service"></a><span data-ttu-id="6f2b9-260">CA 인증서 toocloud 서비스 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-260">Upload CA certificate toocloud service</span></span>
<span data-ttu-id="6f2b9-261">기존 컨트롤이 나 생성 hello로 인증서를 업로드 합니다. Hello CA 공개 키로 CER 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-261">Upload certificate with hello existing or generated .CER file with hello CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="6f2b9-262">서비스 구성 파일의 CA 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f2b9-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="6f2b9-263">Hello 업로드 한 인증서 toohello 클라우드 서비스의 hello 문으로 hello 서비스 구성 파일의 설정에 따라 hello의 hello 지문 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-263">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="6f2b9-264">Hello 동일 hello로 설정한 후의 hello 값을 업데이트 지문:</span><span class="sxs-lookup"><span data-stu-id="6f2b9-264">Update hello value of hello following setting with hello same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="6f2b9-265">클라이언트 인증서 발급</span><span class="sxs-lookup"><span data-stu-id="6f2b9-265">Issue client certificates</span></span>
<span data-ttu-id="6f2b9-266">각 개별 권한 있는 tooaccess hello 서비스는 클라이언트에 대해 인증서 발급 his/hers 배타적 사용 하 고 강력한 암호 tooprotect를 소유 his/hers 해당 개인 키를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-266">Each individual authorized tooaccess hello service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password tooprotect its private key.</span></span> 

<span data-ttu-id="6f2b9-267">단계를 수행 하는 hello CA 인증서에 hello 자체 서명 된 동일한 컴퓨터에서 생성 하 고 저장 된 hello에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-267">hello following steps must be executed in hello same machine where hello self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="6f2b9-268">사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="6f2b9-268">Customizing:</span></span>

* <span data-ttu-id="6f2b9-269">이 인증서로 인증할 수 toohello 클라이언트에 대 한 id-n</span><span class="sxs-lookup"><span data-stu-id="6f2b9-269">-n with an ID for toohello client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="6f2b9-270">-e hello 인증서 만료 날짜와 함께</span><span class="sxs-lookup"><span data-stu-id="6f2b9-270">-e with hello certificate expiration date</span></span>
* <span data-ttu-id="6f2b9-271">MyID.pvk 및 MyID.cer과 이 클라이언트 인증서의 고유한 파일 이름</span><span class="sxs-lookup"><span data-stu-id="6f2b9-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="6f2b9-272">이 명령은 만들고 한 번 사용 되는 암호 toobe 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-272">This command will prompt for a password toobe created and then used once.</span></span> <span data-ttu-id="6f2b9-273">강력한 암호를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="6f2b9-274">클라이언트 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="6f2b9-275">생성된 각 클라이언트 인증서에 대해 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="6f2b9-276">사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="6f2b9-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello client certificate

<span data-ttu-id="6f2b9-277">암호를 입력하고 다음 옵션을 사용하여 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="6f2b9-278">예, hello 개인 키를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-278">Yes, export hello private key</span></span>
* <span data-ttu-id="6f2b9-279">확장된 속성 모두 내보내기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-279">Export all extended properties</span></span>
* <span data-ttu-id="6f2b9-280">이 인증서를 발급 하는 hello 개별 toowhom hello 내보내기 암호를 선택 해야</span><span class="sxs-lookup"><span data-stu-id="6f2b9-280">hello individual toowhom this certificate is being issued should choose hello export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="6f2b9-281">클라이언트 인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-281">Import client certificate</span></span>
<span data-ttu-id="6f2b9-282">사용자에 대 한 클라이언트 인증서가 발급 된 각 개별 hello 키 쌍을 가져와야 hello 컴퓨터 자신이 사용 하 여 toocommunicate hello 서비스:</span><span class="sxs-lookup"><span data-stu-id="6f2b9-282">Each individual for whom a client certificate has been issued should import hello key pair in hello machines he/she will use toocommunicate with hello service:</span></span>

* <span data-ttu-id="6f2b9-283">Hello를 두 번 클릭 합니다. Windows 탐색기에서 PFX 파일</span><span class="sxs-lookup"><span data-stu-id="6f2b9-283">Double-click hello .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="6f2b9-284">Hello 개인 저장소와 적어도이 옵션으로 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-284">Import certificate into hello Personal store with at least this option:</span></span>
  * <span data-ttu-id="6f2b9-285">확장된 속성 모두 포함 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="6f2b9-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="6f2b9-286">클라이언트 인증서 지문 복사</span><span class="sxs-lookup"><span data-stu-id="6f2b9-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="6f2b9-287">대상에 대 한 클라이언트 인증서가 발급 된 각 개별 his/hers의 순서 tooobtain hello 지문에서 다음이 단계를 수행 해야 인증서 toohello 서비스 구성 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-287">Each individual for whom a client certificate has been issued must follow these steps in order tooobtain hello thumbprint of his/hers certificate which will be added toohello service configuration file:</span></span>

* <span data-ttu-id="6f2b9-288">Certmgr.exe 실행</span><span class="sxs-lookup"><span data-stu-id="6f2b9-288">Run certmgr.exe</span></span>
* <span data-ttu-id="6f2b9-289">Hello 개인 탭 선택</span><span class="sxs-lookup"><span data-stu-id="6f2b9-289">Select hello Personal tab</span></span>
* <span data-ttu-id="6f2b9-290">인증에 사용 되는 toobe hello 클라이언트 인증서를 두 번 클릭</span><span class="sxs-lookup"><span data-stu-id="6f2b9-290">Double-click hello client certificate toobe used for authentication</span></span>
* <span data-ttu-id="6f2b9-291">Hello 인증서 대화 상자가 열리면 hello 세부 정보 탭 선택</span><span class="sxs-lookup"><span data-stu-id="6f2b9-291">In hello Certificate dialog that opens, select hello Details tab</span></span>
* <span data-ttu-id="6f2b9-292">표시가 모두를 나타내는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="6f2b9-293">Hello 목록에서 지문 라는 hello 선택 필드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-293">Select hello field named Thumbprint in hello list</span></span>
* <span data-ttu-id="6f2b9-294">Hello 지문 안녕하세요 값 복사 * * hello 첫 번째 숫자 앞에 표시 되지 않는 유니코드 문자 삭제 * * 모든 공백 삭제</span><span class="sxs-lookup"><span data-stu-id="6f2b9-294">Copy hello value of hello thumbprint ** Delete non-visible Unicode characters in front of hello first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a><span data-ttu-id="6f2b9-295">Hello 서비스 구성 파일에 허용 된 클라이언트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-295">Configure Allowed clients in hello service configuration file</span></span>
<span data-ttu-id="6f2b9-296">Hello hello toohello 서비스 액세스를 허용 하는 hello 클라이언트 인증서의 지문 안녕하세요 쉼표로 구분 된 목록이 있는 hello 서비스 구성 파일의 설정에 따라 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-296">Update hello value of hello following setting in hello service configuration file with a comma-separated list of hello thumbprints of hello client certificates allowed access toohello service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="6f2b9-297">클라이언트 인증서 해지 확인 구성</span><span class="sxs-lookup"><span data-stu-id="6f2b9-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="6f2b9-298">클라이언트 인증서 해지 상태에 대 한 인증 기관 hello로 hello 기본 설정을 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-298">hello default setting does not check with hello Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="6f2b9-299">hello hello 클라이언트 인증서를 발급 한 인증 기관에서 이러한 검사를 지 원하는 경우 hello에 tooturn 검사 같이 hello hello X509RevocationMode 열거형에에서 정의 된 hello 값 중 하나가 지정 된 설정에 따라 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-299">tooturn on hello checks, if hello Certification Authority which issued hello client certificates supports such checks, change hello following setting with one of hello values defined in hello X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="6f2b9-300">자체 서명된 암호화 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="6f2b9-301">암호화 인증서에 대해 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="6f2b9-302">사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="6f2b9-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

<span data-ttu-id="6f2b9-303">암호를 입력하고 다음 옵션을 사용하여 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="6f2b9-304">예, hello 개인 키를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-304">Yes, export hello private key</span></span>
* <span data-ttu-id="6f2b9-305">확장된 속성 모두 내보내기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-305">Export all extended properties</span></span>
* <span data-ttu-id="6f2b9-306">Hello 인증서 toohello 클라우드 서비스에 업로드할 때 hello 암호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-306">You will need hello password when uploading hello certificate toohello cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="6f2b9-307">인증서 저장소에서 암호화 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="6f2b9-308">인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-308">Find certificate</span></span>
* <span data-ttu-id="6f2b9-309">작업-> 모든 작업 -> 내보내기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="6f2b9-310">다음 옵션을 사용하여 .PFX 파일로 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="6f2b9-311">예, hello 개인 키를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-311">Yes, export hello private key</span></span>
  * <span data-ttu-id="6f2b9-312">가능 하면 hello 인증 경로 있는 인증서 모두 포함</span><span class="sxs-lookup"><span data-stu-id="6f2b9-312">Include all certificates in hello certification path if possible</span></span> 
* <span data-ttu-id="6f2b9-313">확장된 속성 모두 내보내기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-toocloud-service"></a><span data-ttu-id="6f2b9-314">암호화 인증서 toocloud 서비스 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-314">Upload encryption certificate toocloud service</span></span>
<span data-ttu-id="6f2b9-315">기존 컨트롤이 나 생성 hello로 인증서를 업로드 합니다. PFX 파일 hello 암호화 키 쌍을 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-315">Upload certificate with hello existing or generated .PFX file with hello encryption key pair:</span></span>

* <span data-ttu-id="6f2b9-316">Hello 개인 키 정보를 보호 하는 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-316">Enter hello password protecting hello private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="6f2b9-317">서비스 구성 파일에서 암호화 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="6f2b9-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="6f2b9-318">Hello hello 업로드 한 인증서 toohello 클라우드 서비스의 hello 문으로 hello 서비스 구성 파일의 설정은 다음의 hello 지문 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-318">Update hello thumbprint value of hello following settings in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="6f2b9-319">일반 인증서 작업</span><span class="sxs-lookup"><span data-stu-id="6f2b9-319">Common certificate operations</span></span>
* <span data-ttu-id="6f2b9-320">Hello SSL 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="6f2b9-320">Configure hello SSL certificate</span></span>
* <span data-ttu-id="6f2b9-321">클라이언트 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="6f2b9-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="6f2b9-322">인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-322">Find certificate</span></span>
<span data-ttu-id="6f2b9-323">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-323">Follow these steps:</span></span>

1. <span data-ttu-id="6f2b9-324">Mmc.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="6f2b9-325">파일-> 스냅인 추가/제거로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="6f2b9-326">**인증서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="6f2b9-327">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-327">Click **Add**.</span></span>
5. <span data-ttu-id="6f2b9-328">Hello 인증서 저장소 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-328">Choose hello certificate store location.</span></span>
6. <span data-ttu-id="6f2b9-329">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-329">Click **Finish**.</span></span>
7. <span data-ttu-id="6f2b9-330">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-330">Click **OK**.</span></span>
8. <span data-ttu-id="6f2b9-331">**인증서**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="6f2b9-332">Hello 인증서 저장소 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-332">Expand hello certificate store node.</span></span>
10. <span data-ttu-id="6f2b9-333">Hello 인증서 자식 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-333">Expand hello Certificate child node.</span></span>
11. <span data-ttu-id="6f2b9-334">Hello 목록에 인증서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-334">Select a certificate in hello list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="6f2b9-335">인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-335">Export certificate</span></span>
<span data-ttu-id="6f2b9-336">Hello에 **인증서 내보내기 마법사**:</span><span class="sxs-lookup"><span data-stu-id="6f2b9-336">In hello **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="6f2b9-337">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-337">Click **Next**.</span></span>
2. <span data-ttu-id="6f2b9-338">선택 **예**, 다음 **hello 개인 키 내보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-338">Select **Yes**, then **Export hello private key**.</span></span>
3. <span data-ttu-id="6f2b9-339">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-339">Click **Next**.</span></span>
4. <span data-ttu-id="6f2b9-340">Hello 원하는 출력 파일 형식을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-340">Select hello desired output file format.</span></span>
5. <span data-ttu-id="6f2b9-341">Hello 원하는 옵션을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-341">Check hello desired options.</span></span>
6. <span data-ttu-id="6f2b9-342">**암호**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-342">Check **Password**.</span></span>
7. <span data-ttu-id="6f2b9-343">강력한 암호를 입력하고 이를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="6f2b9-344">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-344">Click **Next**.</span></span>
9. <span data-ttu-id="6f2b9-345">입력 하거나 위치 toostore hello 인증서 파일 이름을 찾습니다 (사용 하는 합니다. 확장명은 PFX)입니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-345">Type or browse a filename where toostore hello certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="6f2b9-346">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-346">Click **Next**.</span></span>
11. <span data-ttu-id="6f2b9-347">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-347">Click **Finish**.</span></span>
12. <span data-ttu-id="6f2b9-348">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="6f2b9-349">인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="6f2b9-349">Import certificate</span></span>
<span data-ttu-id="6f2b9-350">인증서 가져오기 마법사를 hello:</span><span class="sxs-lookup"><span data-stu-id="6f2b9-350">In hello Certificate Import Wizard:</span></span>

1. <span data-ttu-id="6f2b9-351">Hello 저장소 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-351">Select hello store location.</span></span>
   
   * <span data-ttu-id="6f2b9-352">선택 **현재 사용자** 현재 사용자에서 실행 중인 프로세스가 hello 서비스에 액세스 하는 경우에</span><span class="sxs-lookup"><span data-stu-id="6f2b9-352">Select **Current User** if only processes running under current user will access hello service</span></span>
   * <span data-ttu-id="6f2b9-353">선택 **로컬 컴퓨터** 이 컴퓨터의 다른 프로세스가 hello 서비스에 액세스 하는 경우</span><span class="sxs-lookup"><span data-stu-id="6f2b9-353">Select **Local Machine** if other processes in this computer will access hello service</span></span>
2. <span data-ttu-id="6f2b9-354">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-354">Click **Next**.</span></span>
3. <span data-ttu-id="6f2b9-355">파일에서 가져올 경우 hello 파일 경로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-355">If importing from a file, confirm hello file path.</span></span>
4. <span data-ttu-id="6f2b9-356">.PFX 파일을 가져오는 경우:</span><span class="sxs-lookup"><span data-stu-id="6f2b9-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="6f2b9-357">Hello 개인 키를 보호 하는 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-357">Enter hello password protecting hello private key</span></span>
   2. <span data-ttu-id="6f2b9-358">가져오기 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-358">Select import options</span></span>
5. <span data-ttu-id="6f2b9-359">Hello 저장소를 다음에 "장소" 인증서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-359">Select "Place" certificates in hello following store</span></span>
6. <span data-ttu-id="6f2b9-360">**찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-360">Click **Browse**.</span></span>
7. <span data-ttu-id="6f2b9-361">Hello 원하는 저장소를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-361">Select hello desired store.</span></span>
8. <span data-ttu-id="6f2b9-362">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="6f2b9-363">클릭 하 여 hello 신뢰할 수 있는 루트 인증 기관 저장소를 선택한 경우 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-363">If hello Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="6f2b9-364">모든 대화 상자 창에서 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="6f2b9-365">인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="6f2b9-365">Upload certificate</span></span>
<span data-ttu-id="6f2b9-366">Hello에 [Azure 포털](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="6f2b9-366">In hello [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="6f2b9-367">**클라우드 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="6f2b9-368">Hello 클라우드 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-368">Select hello cloud service.</span></span>
3. <span data-ttu-id="6f2b9-369">Hello 상단 메뉴에서 클릭 **인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-369">On hello top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="6f2b9-370">Hello 아래쪽 막대에서 클릭 **업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-370">On hello bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="6f2b9-371">Hello 인증서 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-371">Select hello certificate file.</span></span>
6. <span data-ttu-id="6f2b9-372">경우에 합니다. PFX 파일에서 개인 키 hello hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-372">If it is a .PFX file, enter hello password for hello private key.</span></span>
7. <span data-ttu-id="6f2b9-373">완료 되 면 hello hello 목록에 새 항목에서 hello 인증서 지문을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-373">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="6f2b9-374">기타 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="6f2b9-374">Other security considerations</span></span>
<span data-ttu-id="6f2b9-375">이 문서에서 설명 하는 hello SSL 설정을 hello HTTPS 끝점에서 사용 되는 경우 hello 서비스와 클라이언트 간의 통신을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-375">hello SSL settings described in this document encrypt communication between hello service and its clients when hello HTTPS endpoint is used.</span></span> <span data-ttu-id="6f2b9-376">중요 한 데이터베이스 액세스에 대 한 자격 증명 이후 며이 hello 통신에 포함 될 수 있는 다른 중요 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-376">This is important since credentials for database access and potentially other sensitive information are contained in hello communication.</span></span> <span data-ttu-id="6f2b9-377">그러나 Note, hello 서비스 메타 데이터 저장소에 대 한 Microsoft Azure 구독에서 제공 된 hello Microsoft Azure SQL 데이터베이스에서 해당 내부 테이블에 자격 증명을 포함 하는 내부 상태를 유지 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-377">Note, however, that hello service persists internal status, including credentials, in its internal tables in hello Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="6f2b9-378">해당 데이터베이스는 hello 다음 서비스 구성 파일의 설정의 일부분으로 정의 되었습니다 (합니다. CSCFG 파일):</span><span class="sxs-lookup"><span data-stu-id="6f2b9-378">That database was defined as part of hello following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="6f2b9-379">이 데이터베이스에 저장된 자격 증명은 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="6f2b9-380">그러나 모범 사례로, 웹 및 작업자 역할 모두 하면 서비스 배포의 toodate 위로 유지 되 고 안전 하 게은 둘 다 액세스 toohello 메타 데이터 데이터베이스와 hello 인증서가 저장 된 자격 증명의 암호화 / 해독에 사용 되는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f2b9-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up toodate and secure as they both have access toohello metadata database and hello certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

