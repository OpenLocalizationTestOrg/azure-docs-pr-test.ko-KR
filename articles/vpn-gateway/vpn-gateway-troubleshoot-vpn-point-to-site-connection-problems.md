---
title: "aaaTroubleshoot Azure 지점 및 사이트 간 연결 문제 | Microsoft Docs"
description: "자세한 내용은 방법 tootroubleshoot 지점 및 사이트 연결 문제입니다."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="4cf4a-103">문제 해결: Azure 지점 및 사이트 간 연결 문제</span><span class="sxs-lookup"><span data-stu-id="4cf4a-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="4cf4a-104">이 문서에서는 발생할 수 있는 일반적인 지점 및 사이트 간 연결 문제를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="4cf4a-105">또한 이러한 문제의 가능한 원인과 해결 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="4cf4a-106">VPN 클라이언트 오류: 인증서를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf4a-107">증상</span><span class="sxs-lookup"><span data-stu-id="4cf4a-107">Symptom</span></span>

<span data-ttu-id="4cf4a-108">Hello VPN 클라이언트를 사용 하 여 tooconnect tooan Azure 가상 네트워크를 시도 하면 hello 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-108">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="4cf4a-109">**이 확장할 수 있는 인증 프로토콜에 사용할 수 있는 인증서를 찾을 수 없습니다. (오류 798)**</span><span class="sxs-lookup"><span data-stu-id="4cf4a-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="4cf4a-110">원인</span><span class="sxs-lookup"><span data-stu-id="4cf4a-110">Cause</span></span>

<span data-ttu-id="4cf4a-111">Hello 클라이언트 인증서가 없을 경우이 문제가 발생 **인증서-Current User\Personal\Certificates**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-111">This problem occurs if hello client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf4a-112">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf4a-112">Solution</span></span>

<span data-ttu-id="4cf4a-113">Hello hello 인증서 저장소 (Certmgr.msc)의 위치를 따라 해당 hello 클라이언트 인증서가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-113">Make sure that hello client certificate is installed in hello following location of hello Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="4cf4a-114">**인증서 - Current User\Personal\Certificates**</span><span class="sxs-lookup"><span data-stu-id="4cf4a-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="4cf4a-115">Tooinstall 클라이언트 인증서를 hello 하는 방법에 대 한 자세한 내용은 참조 [지점 및 사이트 간 연결에 대 한 인증서를 생성 및 내보내기](vpn-gateway-certificates-point-to-site.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-115">For more information about how tooinstall hello client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4cf4a-116">Hello 클라이언트 인증서를 가져올 때 hello를 선택 하지 않으면 **강력한 개인 키 보호 사용** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-116">When you import hello client certificate, do not select hello **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="4cf4a-117">VPN 클라이언트 오류: hello 메시지를 받은 예기치 않은 형식이 잘못 되었습니다</span><span class="sxs-lookup"><span data-stu-id="4cf4a-117">VPN client error: hello message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf4a-118">증상</span><span class="sxs-lookup"><span data-stu-id="4cf4a-118">Symptom</span></span>

<span data-ttu-id="4cf4a-119">Hello VPN 클라이언트를 사용 하 여 tooconnect tooan Azure 가상 네트워크를 시도 하면 hello 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-119">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="4cf4a-120">**hello 메시지를 받은 예기치 않은 형식이 잘못 되었습니다. (오류 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="4cf4a-120">**hello message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="4cf4a-121">원인</span><span class="sxs-lookup"><span data-stu-id="4cf4a-121">Cause</span></span>

<span data-ttu-id="4cf4a-122">이 문제는 hello 루트 인증서의 공개 키 hello Azure VPN 게이트웨이로 업로드 되지 않으면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-122">This problem occurs if hello root certificate public key is not uploaded into hello Azure VPN gateway.</span></span> <span data-ttu-id="4cf4a-123">Hello 키가 손상 되었거나 만료 된 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-123">It can also occur if hello key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf4a-124">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf4a-124">Solution</span></span>

<span data-ttu-id="4cf4a-125">이 문제를 hello 루트의 hello 상태를 확인이 Azure 포털 toosee hello에 인증서가 해지 여부를 tooresolve 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-125">tooresolve this problem, check hello status of hello root certificate in hello Azure portal toosee whether it was revoked.</span></span> <span data-ttu-id="4cf4a-126">해지 되지 않은 경우에 toodelete hello 루트 인증서와 reupload 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-126">If it is not revoked, try toodelete hello root certificate and reupload.</span></span> <span data-ttu-id="4cf4a-127">자세한 내용은 [인증서 만들기](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="4cf4a-128">VPN 클라이언트 오류: 인증서 체인이 처리되었지만 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="4cf4a-129">증상</span><span class="sxs-lookup"><span data-stu-id="4cf4a-129">Symptom</span></span> 

<span data-ttu-id="4cf4a-130">Hello VPN 클라이언트를 사용 하 여 tooconnect tooan Azure 가상 네트워크를 시도 하면 hello 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-130">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="4cf4a-131">**인증서 체인이 처리 되었지만 트러스트 공급자 hello 신뢰 되지 않는 루트 인증서에서 종료 되었습니다.**</span><span class="sxs-lookup"><span data-stu-id="4cf4a-131">**A certificate chain processed but terminated in a root certificate which is not trusted by hello trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="4cf4a-132">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf4a-132">Solution</span></span>

1. <span data-ttu-id="4cf4a-133">인증서를 다음 해당 hello hello 올바른 위치에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-133">Make sure that hello following certificates are in hello correct location:</span></span>

    | <span data-ttu-id="4cf4a-134">인증서</span><span class="sxs-lookup"><span data-stu-id="4cf4a-134">Certificate</span></span> | <span data-ttu-id="4cf4a-135">위치</span><span class="sxs-lookup"><span data-stu-id="4cf4a-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="4cf4a-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="4cf4a-136">AzureClient.pfx</span></span>  | <span data-ttu-id="4cf4a-137">Current User\Personal\Certificates</span><span class="sxs-lookup"><span data-stu-id="4cf4a-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="4cf4a-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="4cf4a-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="4cf4a-139">Current User\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="4cf4a-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="4cf4a-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="4cf4a-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="4cf4a-141">Local Computer\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="4cf4a-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="4cf4a-142">Hello 인증서가 이미 hello 위치, toodelete hello 인증서를 시도 하 고 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-142">If hello certificates are already in hello location, try toodelete hello certificates and reinstall them.</span></span> <span data-ttu-id="4cf4a-143">hello  **azuregateway-*GUID*. cloudapp.net** 인증서가 hello Azure 포털에서에서 다운로드 한 hello VPN 클라이언트 구성 패키지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-143">hello **azuregateway-*GUID*.cloudapp.net** certificate is in hello VPN client configuration package that you downloaded from hello Azure portal.</span></span> <span data-ttu-id="4cf4a-144">파일 archivers tooextract hello 파일 hello 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-144">You can use file archivers tooextract hello files from hello package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="4cf4a-145">파일 다운로드 오류: 대상 URI를 지정하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf4a-146">증상</span><span class="sxs-lookup"><span data-stu-id="4cf4a-146">Symptom</span></span>

<span data-ttu-id="4cf4a-147">Hello 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-147">You receive hello following error message:</span></span>

<span data-ttu-id="4cf4a-148">**파일 다운로드 오류. 대상 URI가 지정되지 않았습니다.**</span><span class="sxs-lookup"><span data-stu-id="4cf4a-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="4cf4a-149">원인</span><span class="sxs-lookup"><span data-stu-id="4cf4a-149">Cause</span></span> 

<span data-ttu-id="4cf4a-150">이 문제는 잘못된 게이트웨이 형식 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="4cf4a-151">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf4a-151">Solution</span></span>

<span data-ttu-id="4cf4a-152">hello VPN 게이트웨이 유형 이어야 합니다 **VPN**, hello VPN 형식 이어야 하 고 **RouteBased**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-152">hello VPN gateway type must be **VPN**, and hello VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="4cf4a-153">VPN 클라이언트 오류: Azure VPN 사용자 지정 스크립트가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="4cf4a-154">증상</span><span class="sxs-lookup"><span data-stu-id="4cf4a-154">Symptom</span></span>

<span data-ttu-id="4cf4a-155">Hello VPN 클라이언트를 사용 하 여 tooconnect tooan Azure 가상 네트워크를 시도 하면 hello 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-155">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="4cf4a-156">**사용자 지정 스크립트 (tooupdate 프로그램 라우팅 테이블) 실패 했습니다. (오류 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="4cf4a-156">**Custom script (tooupdate your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="4cf4a-157">원인</span><span class="sxs-lookup"><span data-stu-id="4cf4a-157">Cause</span></span>

<span data-ttu-id="4cf4a-158">이 문제는 바로 가기를 사용 하 여 tooopen hello 사이트와 지점 간 VPN 연결을 시도 하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-158">This problem might occur if you are trying tooopen hello site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf4a-159">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf4a-159">Solution</span></span> 

<span data-ttu-id="4cf4a-160">Hello 바로 가기에서 여 하는 대신에 직접 hello VPN 패키지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-160">Open hello VPN package directly instead of opening it from hello shortcut.</span></span>

## <a name="cannot-install-hello-vpn-client"></a><span data-ttu-id="4cf4a-161">Hello VPN 클라이언트를 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-161">Cannot install hello VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="4cf4a-162">원인</span><span class="sxs-lookup"><span data-stu-id="4cf4a-162">Cause</span></span> 

<span data-ttu-id="4cf4a-163">추가 인증서가 필요한 tootrust hello VPN 게이트웨이 가상 네트워크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-163">An additional certificate is required tootrust hello VPN gateway for your virtual network.</span></span> <span data-ttu-id="4cf4a-164">hello 인증서 hello Azure 포털에서에서 생성 되는 hello VPN 클라이언트 구성 패키지에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-164">hello certificate is included in hello VPN client configuration package that is generated from hello Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf4a-165">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf4a-165">Solution</span></span>

<span data-ttu-id="4cf4a-166">Hello VPN 클라이언트 구성 패키지를 추출 하 고 hello.cer 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-166">Extract hello VPN client configuration package, and find hello .cer file.</span></span> <span data-ttu-id="4cf4a-167">tooinstall hello 인증서, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-167">tooinstall hello certificate, follow these steps:</span></span>

1. <span data-ttu-id="4cf4a-168">mmc.exe를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="4cf4a-169">Hello 추가 **인증서** 스냅인.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-169">Add hello **Certificates** snap-in.</span></span>
3. <span data-ttu-id="4cf4a-170">선택 hello **컴퓨터** hello 로컬 컴퓨터에 대 한 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-170">Select hello **Computer** account for hello local computer.</span></span>
4. <span data-ttu-id="4cf4a-171">마우스 오른쪽 단추로 클릭 hello **신뢰할 수 있는 루트 인증 기관** 노드.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-171">Right-click hello **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="4cf4a-172">클릭 **All 작업** > **가져오기**, 및 찾아보기 toohello.cer 파일 hello VPN 클라이언트 구성 패키지에서 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-172">Click **All-Task** > **Import**, and browse toohello .cer file you extracted from hello VPN client configuration package.</span></span>
5. <span data-ttu-id="4cf4a-173">Hello 컴퓨터를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-173">Restart hello computer.</span></span> 
6. <span data-ttu-id="4cf4a-174">Tooinstall hello VPN 클라이언트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-174">Try tooinstall hello VPN client.</span></span>

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a><span data-ttu-id="4cf4a-175">Azure 포털 오류: toosave hello VPN 게이트웨이 실패 했으며 hello 데이터가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-175">Azure portal error: Failed toosave hello VPN gateway, and hello data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf4a-176">증상</span><span class="sxs-lookup"><span data-stu-id="4cf4a-176">Symptom</span></span>

<span data-ttu-id="4cf4a-177">Hello Azure 포털에서에서 VPN 게이트웨이 hello에 대 한 toosave hello 변경 하면 hello 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-177">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span>

<span data-ttu-id="4cf4a-178">**실패 한 toosave 가상 네트워크 게이트웨이 &lt;* 게이트웨이 이름*&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-178">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="4cf4a-179">인증서 &lt;*인증서 ID*&gt;에 대한 데이터가 유효하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="4cf4a-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="4cf4a-180">원인</span><span class="sxs-lookup"><span data-stu-id="4cf4a-180">Cause</span></span> 

<span data-ttu-id="4cf4a-181">업로드 한 hello 루트 인증서 공개 키 예: 공백에 잘못 된 문자가 포함 되어 있는 경우이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-181">This problem might occur if hello root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf4a-182">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf4a-182">Solution</span></span>

<span data-ttu-id="4cf4a-183">Hello 인증서의 hello 데이터 줄 바꿈 (캐리지 리턴) 등의 잘못 된 문자가 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-183">Make sure that hello data in hello certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="4cf4a-184">hello 전체 값에는 긴 한 줄 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-184">hello entire value should be one long line.</span></span> <span data-ttu-id="4cf4a-185">hello 텍스트 다음은 hello 인증서의 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-185">hello following text is a sample of hello certificate:</span></span>

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a><span data-ttu-id="4cf4a-186">Azure 포털 오류: toosave hello VPN 게이트웨이 실패 했으며 hello 리소스 이름이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-186">Azure portal error: Failed toosave hello VPN gateway, and hello resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf4a-187">증상</span><span class="sxs-lookup"><span data-stu-id="4cf4a-187">Symptom</span></span>

<span data-ttu-id="4cf4a-188">Hello Azure 포털에서에서 VPN 게이트웨이 hello에 대 한 toosave hello 변경 하면 hello 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-188">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span> 

<span data-ttu-id="4cf4a-189">**실패 한 toosave 가상 네트워크 게이트웨이 &lt;* 게이트웨이 이름*&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-189">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="4cf4a-190">리소스 이름 &lt; *tooupload를 시도 하는 인증서 이름이* &gt; 가 잘못 되었습니다. * *입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-190">Resource name &lt;*certificate name you try tooupload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="4cf4a-191">원인</span><span class="sxs-lookup"><span data-stu-id="4cf4a-191">Cause</span></span>

<span data-ttu-id="4cf4a-192">Hello 인증서의 hello 이름에 공백 같은 잘못 된 문자가 포함 되어이 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-192">This problem occurs because hello name of hello certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="4cf4a-193">Azure Portal 오류: VPN 패키지 파일 다운로드 오류 503</span><span class="sxs-lookup"><span data-stu-id="4cf4a-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf4a-194">증상</span><span class="sxs-lookup"><span data-stu-id="4cf4a-194">Symptom</span></span>

<span data-ttu-id="4cf4a-195">Toodownload hello VPN 클라이언트 구성 패키지에서 하면 hello 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-195">When you try toodownload hello VPN client configuration package, you receive hello following error message:</span></span>

<span data-ttu-id="4cf4a-196">**Toodownload hello 파일에 실패 했습니다. 오류 세부 정보: 503 오류입니다. hello 서버 사용 중입니다.**</span><span class="sxs-lookup"><span data-stu-id="4cf4a-196">**Failed toodownload hello file. Error details: error 503. hello server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="4cf4a-197">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf4a-197">Solution</span></span>

<span data-ttu-id="4cf4a-198">이 오류는 임시 네트워크 문제로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="4cf4a-199">Toodownload hello VPN 패키지를 몇 분 후에 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-199">Try toodownload hello VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a><span data-ttu-id="4cf4a-200">Azure VPN 게이트웨이 업그레이드할: 모든 P2S 클라이언트는 tooconnect 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-200">Azure VPN Gateway upgrade: All P2S clients are unable tooconnect</span></span>

### <a name="cause"></a><span data-ttu-id="4cf4a-201">원인</span><span class="sxs-lookup"><span data-stu-id="4cf4a-201">Cause</span></span>

<span data-ttu-id="4cf4a-202">Hello 인증서가 50%를 넘는 경우 그 수명은 통해 hello 인증서 롤오버 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-202">If hello certificate is more than 50 percent through its lifetime, hello certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf4a-203">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf4a-203">Solution</span></span>

<span data-ttu-id="4cf4a-204">tooresolve이이 문제를 만들고 새 인증서 toohello VPN 클라이언트를 재배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-204">tooresolve this problem, create and redistribute new certificates toohello VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="4cf4a-205">한 번에 너무 많은 VPN 클라이언트 연결</span><span class="sxs-lookup"><span data-stu-id="4cf4a-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="4cf4a-206">각 VPN 게이트웨이에 대 한 최대 허용 연결 수 hello은 128입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-206">For each VPN gateway, hello maximum number of allowable connections is 128.</span></span> <span data-ttu-id="4cf4a-207">Hello hello Azure 포털에에서 연결 된 클라이언트의 총 수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-207">You can see hello total number of connected clients in hello Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a><span data-ttu-id="4cf4a-208">지점-사이트 VPN 10.0.0.0/8 toohello 경로 테이블에 대 한 경로 제대로 추가</span><span class="sxs-lookup"><span data-stu-id="4cf4a-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 toohello route table</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf4a-209">증상</span><span class="sxs-lookup"><span data-stu-id="4cf4a-209">Symptom</span></span>

<span data-ttu-id="4cf4a-210">Hello hello 지점-사이트 클라이언트에서 VPN 연결에서 전화 걸 때 hello VPN 클라이언트 hello Azure 가상 네트워크에 대 한 경로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-210">When you dial hello VPN connection on hello point-to-site client, hello VPN client should add a route toward hello Azure virtual network.</span></span> <span data-ttu-id="4cf4a-211">hello IP 도우미 서비스는 hello VPN 클라이언트의 hello 서브넷에 대 한 경로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-211">hello IP helper service should add a route for hello subnet of hello VPN clients.</span></span> 

<span data-ttu-id="4cf4a-212">VPN 클라이언트 범위 hello 10.0.0.0/8 10.0.12.0/24 등의 더 작은 서브넷 tooa 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-212">hello VPN client range belongs tooa smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="4cf4a-213">10.0.12.0/24에 대한 경로 대신 우선 순위가 더 높은 10.0.0.0/8에 대한 경로가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="4cf4a-214">이 잘못 된 경로 정의 된 특정 경로 없는 다른 온-프레미스 네트워크 tooanother 서브넷 10.50.0.0/24, 같은 hello 10.0.0.0/8 범위 내에 속하는와 연결을 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-214">This incorrect route breaks connectivity with other on-premises networks that might belong tooanother subnet within hello 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="4cf4a-215">원인</span><span class="sxs-lookup"><span data-stu-id="4cf4a-215">Cause</span></span>

<span data-ttu-id="4cf4a-216">이 동작은 Windows 클라이언트용으로 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="4cf4a-217">Hello 클라이언트 hello PPP IPCP 프로토콜을 사용 하는 경우 hello 서버 (이 경우 hello VPN 게이트웨이)에서 hello 터널 인터페이스에 대 한 hello IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-217">When hello client uses hello PPP IPCP protocol, it obtains hello IP address for hello tunnel interface from hello server (hello VPN gateway in this case).</span></span> <span data-ttu-id="4cf4a-218">그러나 hello 프로토콜의 제한 때문에 hello 클라이언트 없는 hello 서브넷 마스크입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-218">However, because of a limitation in hello protocol, hello client does not have hello subnet mask.</span></span> <span data-ttu-id="4cf4a-219">다른 방식으로 tooget 없습니다 있기 때문에, hello 클라이언트 시도 tooguess hello 서브넷 마스크 hello 터널 인터페이스 IP 주소의 hello 클래스에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-219">Because there is no other way tooget it, hello client tries tooguess hello subnet mask based on hello class of hello tunnel interface IP address.</span></span> 

<span data-ttu-id="4cf4a-220">따라서 경로 정적 매핑과 다음 hello에 따라 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-220">Therefore, a route is added based on hello following static mapping:</span></span> 

<span data-ttu-id="4cf4a-221">--> 적용/8 주소 tooclass A 속하는 경우</span><span class="sxs-lookup"><span data-stu-id="4cf4a-221">If address belongs tooclass A --> apply /8</span></span>

<span data-ttu-id="4cf4a-222">B--> tooclass 적용/16 주소 속하는 경우</span><span class="sxs-lookup"><span data-stu-id="4cf4a-222">If address belongs tooclass B --> apply /16</span></span>

<span data-ttu-id="4cf4a-223">C--> tooclass 적용/24 주소 속하는 경우</span><span class="sxs-lookup"><span data-stu-id="4cf4a-223">If address belongs tooclass C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="4cf4a-224">VPN 클라이언트는 네트워크 파일 공유에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf4a-225">증상</span><span class="sxs-lookup"><span data-stu-id="4cf4a-225">Symptom</span></span>

<span data-ttu-id="4cf4a-226">VPN 클라이언트 hello toohello Azure 가상 네트워크를 연결 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-226">hello VPN client has connected toohello Azure virtual network.</span></span> <span data-ttu-id="4cf4a-227">그러나 hello 클라이언트 네트워크 공유에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-227">However, hello client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="4cf4a-228">원인</span><span class="sxs-lookup"><span data-stu-id="4cf4a-228">Cause</span></span>

<span data-ttu-id="4cf4a-229">hello SMB 프로토콜은 파일 공유 액세스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-229">hello SMB protocol is used for file share access.</span></span> <span data-ttu-id="4cf4a-230">Hello 연결 시작 되 면 hello VPN 클라이언트 hello 세션 자격 증명을 추가 하 고 hello 오류 발생 시.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-230">When hello connection is initiated, hello VPN client adds hello session credentials and hello failure occurs.</span></span> <span data-ttu-id="4cf4a-231">Hello 연결이 설정 된 후 hello 클라이언트는 toouse hello Kerberos 인증에 대 한 자격 증명 캐시를 강제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-231">After hello connection is established, hello client is forced toouse hello cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="4cf4a-232">이 프로세스는 쿼리 toohello 키 배포 센터 (도메인 컨트롤러) tooget 토큰을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-232">This process initiates queries toohello Key Distribution Center (a domain controller) tooget a token.</span></span> <span data-ttu-id="4cf4a-233">Hello 클라이언트 hello 인터넷에 연결 하기 때문에 수 tooreach hello 도메인 컨트롤러 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-233">Because hello client connects from hello Internet, it might not be able tooreach hello domain controller.</span></span> <span data-ttu-id="4cf4a-234">따라서 hello 클라이언트에서 Kerberos tooNTLM 조치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-234">Therefore, hello client cannot fail over from Kerberos tooNTLM.</span></span> 

<span data-ttu-id="4cf4a-235">hello만 시간이 hello 클라이언트 자격 증명은 유효한 인증서를가 하는 경우에 대 한 라는 메시지가 표시 됩니다 (SAN UPN =) hello 도메인 toowhich 조인에서 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-235">hello only time that hello client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by hello domain toowhich it is joined.</span></span> <span data-ttu-id="4cf4a-236">또한 클라이언트 hello에 물리적으로 연결 된 toohello 도메인 네트워크 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-236">hello client also must be physically connected toohello domain network.</span></span> <span data-ttu-id="4cf4a-237">이 경우 hello 클라이언트 toouse hello 인증서 시도 아웃 toohello 도메인 컨트롤러에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-237">In this case, hello client tries toouse hello certificate and reaches out toohello domain controller.</span></span> <span data-ttu-id="4cf4a-238">그런 다음 hello 키 배포 센터 "KDC_ERR_C_PRINCIPAL_UNKNOWN" 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-238">Then hello Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="4cf4a-239">클라이언트 hello에서는 강제 toofail tooNTLM 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-239">hello client is forced toofail over tooNTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="4cf4a-240">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf4a-240">Solution</span></span>

<span data-ttu-id="4cf4a-241">hello 문제 toowork hello hello 다음 레지스트리 하위 키에서에서 도메인 자격 증명 캐싱을 사용 하지 않도록 설정:</span><span class="sxs-lookup"><span data-stu-id="4cf4a-241">toowork around hello problem, disable hello caching of domain credentials from hello following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a><span data-ttu-id="4cf4a-242">Hello VPN 클라이언트를 다시 설치한 후 windows에서 hello 지점-사이트 VPN 연결을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-242">Cannot find hello point-to-site VPN connection in Windows after reinstalling hello VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf4a-243">증상</span><span class="sxs-lookup"><span data-stu-id="4cf4a-243">Symptom</span></span>

<span data-ttu-id="4cf4a-244">Hello 지점-사이트 VPN 연결을 제거한 다음 hello VPN 클라이언트를 다시 설치 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-244">You remove hello point-to-site VPN connection and then reinstall hello VPN client.</span></span> <span data-ttu-id="4cf4a-245">이 경우 VPN 연결 hello 성공적으로 구성 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-245">In this situation, hello VPN connection is not configured successfully.</span></span> <span data-ttu-id="4cf4a-246">Hello VPN 연결 hello에 표시 되지 않으면 **네트워크 연결** Windows에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-246">You do not see hello VPN connection in hello **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf4a-247">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf4a-247">Solution</span></span>

<span data-ttu-id="4cf4a-248">tooresolve hello 문제를 delete hello 오래 된 VPN 클라이언트 구성 파일에서 **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, hello VPN 클라이언트 설치 프로그램을 다시 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4cf4a-248">tooresolve hello problem, delete hello old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run hello VPN client installer again.</span></span>
