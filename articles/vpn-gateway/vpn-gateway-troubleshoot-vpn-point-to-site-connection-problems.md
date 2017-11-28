---
title: "Azure 지점 및 사이트 간 연결 문제 해결 | Microsoft Docs"
description: "지점 및 사이트 간 연결 문제를 해결하는 방법을 알아봅니다."
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
ms.openlocfilehash: de37c8ffd47a2b8e201d18e3a20b5325d528ad59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="47e2a-103">문제 해결: Azure 지점 및 사이트 간 연결 문제</span><span class="sxs-lookup"><span data-stu-id="47e2a-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="47e2a-104">이 문서에서는 발생할 수 있는 일반적인 지점 및 사이트 간 연결 문제를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="47e2a-105">또한 이러한 문제의 가능한 원인과 해결 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="47e2a-106">VPN 클라이언트 오류: 인증서를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="47e2a-107">증상</span><span class="sxs-lookup"><span data-stu-id="47e2a-107">Symptom</span></span>

<span data-ttu-id="47e2a-108">VPN 클라이언트를 사용하여 Azure 가상 네트워크에 연결하려고 할 때 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-108">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="47e2a-109">**이 확장할 수 있는 인증 프로토콜에 사용할 수 있는 인증서를 찾을 수 없습니다. (오류 798)**</span><span class="sxs-lookup"><span data-stu-id="47e2a-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="47e2a-110">원인</span><span class="sxs-lookup"><span data-stu-id="47e2a-110">Cause</span></span>

<span data-ttu-id="47e2a-111">클라이언트 인증서가 **인증서 - Current User\Personal\Certificates**에서 누락된 경우 이 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-111">This problem occurs if the client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="47e2a-112">해결 방법</span><span class="sxs-lookup"><span data-stu-id="47e2a-112">Solution</span></span>

<span data-ttu-id="47e2a-113">클라이언트 인증서(Certmgr.msc)가 인증서 저장소의 다음 위치에 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-113">Make sure that the client certificate is installed in the following location of the Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="47e2a-114">**인증서 - Current User\Personal\Certificates**</span><span class="sxs-lookup"><span data-stu-id="47e2a-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="47e2a-115">클라이언트 인증서를 설치하는 방법에 대한 자세한 내용은 [지점 및 사이트 간 연결에 대한 인증서를 생성 및 내보내기](vpn-gateway-certificates-point-to-site.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47e2a-115">For more information about how to install the client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="47e2a-116">클라이언트 인증서를 가져올 때 **강력한 개인 키 보호 사용** 옵션을 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-116">When you import the client certificate, do not select the **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-the-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="47e2a-117">VPN 클라이언트 오류: 예기치 않거나 형식이 잘못된 메시지를 수신했습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-117">VPN client error: The message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="47e2a-118">증상</span><span class="sxs-lookup"><span data-stu-id="47e2a-118">Symptom</span></span>

<span data-ttu-id="47e2a-119">VPN 클라이언트를 사용하여 Azure 가상 네트워크에 연결하려고 할 때 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-119">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="47e2a-120">**예기치 않거나 형식이 잘못된 메시지를 수신했습니다. (오류 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="47e2a-120">**The message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="47e2a-121">원인</span><span class="sxs-lookup"><span data-stu-id="47e2a-121">Cause</span></span>

<span data-ttu-id="47e2a-122">Azure VPN 게이트웨이에 루트 인증서 공개 키를 업로드하지 않은 경우 이 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-122">This problem occurs if the root certificate public key is not uploaded into the Azure VPN gateway.</span></span> <span data-ttu-id="47e2a-123">키가 손상되거나 만료되는 경우에도 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-123">It can also occur if the key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="47e2a-124">해결 방법</span><span class="sxs-lookup"><span data-stu-id="47e2a-124">Solution</span></span>

<span data-ttu-id="47e2a-125">이 문제를 해결하려면 Azure Portal에서 루트 인증서가 해지되었는지 여부를 확인하기 위해 해당 인증서의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-125">To resolve this problem, check the status of the root certificate in the Azure portal to see whether it was revoked.</span></span> <span data-ttu-id="47e2a-126">해지되지 않은 경우 루트 인증서를 삭제하고 다시 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-126">If it is not revoked, try to delete the root certificate and reupload.</span></span> <span data-ttu-id="47e2a-127">자세한 내용은 [인증서 만들기](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47e2a-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="47e2a-128">VPN 클라이언트 오류: 인증서 체인이 처리되었지만 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="47e2a-129">증상</span><span class="sxs-lookup"><span data-stu-id="47e2a-129">Symptom</span></span> 

<span data-ttu-id="47e2a-130">VPN 클라이언트를 사용하여 Azure 가상 네트워크에 연결하려고 할 때 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-130">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="47e2a-131">**인증서 체인이 처리되었지만 트러스트 공급자가 신뢰하지 않는 루트 인증서에서 종료되었습니다.**</span><span class="sxs-lookup"><span data-stu-id="47e2a-131">**A certificate chain processed but terminated in a root certificate which is not trusted by the trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="47e2a-132">해결 방법</span><span class="sxs-lookup"><span data-stu-id="47e2a-132">Solution</span></span>

1. <span data-ttu-id="47e2a-133">다음 인증서가 올바른 위치에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-133">Make sure that the following certificates are in the correct location:</span></span>

    | <span data-ttu-id="47e2a-134">인증서</span><span class="sxs-lookup"><span data-stu-id="47e2a-134">Certificate</span></span> | <span data-ttu-id="47e2a-135">위치</span><span class="sxs-lookup"><span data-stu-id="47e2a-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="47e2a-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="47e2a-136">AzureClient.pfx</span></span>  | <span data-ttu-id="47e2a-137">Current User\Personal\Certificates</span><span class="sxs-lookup"><span data-stu-id="47e2a-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="47e2a-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="47e2a-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="47e2a-139">Current User\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="47e2a-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="47e2a-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="47e2a-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="47e2a-141">Local Computer\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="47e2a-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="47e2a-142">인증서가 이미 있으면 해당 인증서를 삭제하고 다시 설치하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-142">If the certificates are already in the location, try to delete the certificates and reinstall them.</span></span> <span data-ttu-id="47e2a-143">**azuregateway-*GUID*.cloudapp.net** 인증서는 Azure Portal에서 다운로드한 VPN 클라이언트 구성 패키지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-143">The **azuregateway-*GUID*.cloudapp.net** certificate is in the VPN client configuration package that you downloaded from the Azure portal.</span></span> <span data-ttu-id="47e2a-144">패키지에서 파일을 추출하려면 파일 실행자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-144">You can use file archivers to extract the files from the package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="47e2a-145">파일 다운로드 오류: 대상 URI를 지정하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="47e2a-146">증상</span><span class="sxs-lookup"><span data-stu-id="47e2a-146">Symptom</span></span>

<span data-ttu-id="47e2a-147">다음과 같은 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-147">You receive the following error message:</span></span>

<span data-ttu-id="47e2a-148">**파일 다운로드 오류. 대상 URI가 지정되지 않았습니다.**</span><span class="sxs-lookup"><span data-stu-id="47e2a-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="47e2a-149">원인</span><span class="sxs-lookup"><span data-stu-id="47e2a-149">Cause</span></span> 

<span data-ttu-id="47e2a-150">이 문제는 잘못된 게이트웨이 형식 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="47e2a-151">해결 방법</span><span class="sxs-lookup"><span data-stu-id="47e2a-151">Solution</span></span>

<span data-ttu-id="47e2a-152">VPN 게이트웨이 형식은 **VPN**이어야 하고 VPN 형식은 **경로 기반**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-152">The VPN gateway type must be **VPN**, and the VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="47e2a-153">VPN 클라이언트 오류: Azure VPN 사용자 지정 스크립트가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="47e2a-154">증상</span><span class="sxs-lookup"><span data-stu-id="47e2a-154">Symptom</span></span>

<span data-ttu-id="47e2a-155">VPN 클라이언트를 사용하여 Azure 가상 네트워크에 연결하려고 할 때 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-155">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="47e2a-156">**(라우팅 테이블을 업데이트하는) 사용자 지정 스크립트에 실패했습니다. (오류 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="47e2a-156">**Custom script (to update your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="47e2a-157">원인</span><span class="sxs-lookup"><span data-stu-id="47e2a-157">Cause</span></span>

<span data-ttu-id="47e2a-158">이 문제는 바로 가기를 사용하여 사이트 및 지점 간 VPN 연결을 시도하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-158">This problem might occur if you are trying to open the site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="47e2a-159">해결 방법</span><span class="sxs-lookup"><span data-stu-id="47e2a-159">Solution</span></span> 

<span data-ttu-id="47e2a-160">바로 가기로 열지 않고 직접 VPN 패키지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-160">Open the VPN package directly instead of opening it from the shortcut.</span></span>

## <a name="cannot-install-the-vpn-client"></a><span data-ttu-id="47e2a-161">VPN 클라이언트를 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-161">Cannot install the VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="47e2a-162">원인</span><span class="sxs-lookup"><span data-stu-id="47e2a-162">Cause</span></span> 

<span data-ttu-id="47e2a-163">가상 네트워크에 대한 VPN Gateway를 신뢰하기 위해 추가 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-163">An additional certificate is required to trust the VPN gateway for your virtual network.</span></span> <span data-ttu-id="47e2a-164">인증서는 Azure Portal에서 생성되는 VPN 클라이언트 구성 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-164">The certificate is included in the VPN client configuration package that is generated from the Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="47e2a-165">해결 방법</span><span class="sxs-lookup"><span data-stu-id="47e2a-165">Solution</span></span>

<span data-ttu-id="47e2a-166">VPN 클라이언트 구성 패키지를 추출하고 .cer 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-166">Extract the VPN client configuration package, and find the .cer file.</span></span> <span data-ttu-id="47e2a-167">인증서를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="47e2a-167">To install the certificate, follow these steps:</span></span>

1. <span data-ttu-id="47e2a-168">mmc.exe를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="47e2a-169">**인증서** 스냅인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-169">Add the **Certificates** snap-in.</span></span>
3. <span data-ttu-id="47e2a-170">로컬 컴퓨터의 **컴퓨터** 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-170">Select the **Computer** account for the local computer.</span></span>
4. <span data-ttu-id="47e2a-171">**신뢰할 수 있는 루트 인증 기관** 노드를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-171">Right-click the **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="47e2a-172">**모든 작업** > **가져오기**를 클릭하고 VPN 클라이언트 구성 패키지에서 추출한 .cer 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-172">Click **All-Task** > **Import**, and browse to the .cer file you extracted from the VPN client configuration package.</span></span>
5. <span data-ttu-id="47e2a-173">컴퓨터를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-173">Restart the computer.</span></span> 
6. <span data-ttu-id="47e2a-174">VPN 클라이언트를 설치해봅니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-174">Try to install the VPN client.</span></span>

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-data-is-invalid"></a><span data-ttu-id="47e2a-175">Azure Portal 오류: VPN 게이트웨이를 저장하지 못했으며 데이터가 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-175">Azure portal error: Failed to save the VPN gateway, and the data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="47e2a-176">증상</span><span class="sxs-lookup"><span data-stu-id="47e2a-176">Symptom</span></span>

<span data-ttu-id="47e2a-177">Azure Portal에서 VPN Gateway에 변경 내용을 저장하려고 할 때 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-177">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span>

<span data-ttu-id="47e2a-178">**가상 네트워크 게이트웨이 &lt;*게이트웨이 이름*&gt;을 저장하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-178">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="47e2a-179">인증서 &lt;*인증서 ID*&gt;에 대한 데이터가 유효하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="47e2a-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="47e2a-180">원인</span><span class="sxs-lookup"><span data-stu-id="47e2a-180">Cause</span></span> 

<span data-ttu-id="47e2a-181">업로드한 루트 인증서 공개 키가 공백과 같은 유효하지 않은 문자를 포함하는 경우 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-181">This problem might occur if the root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="47e2a-182">해결 방법</span><span class="sxs-lookup"><span data-stu-id="47e2a-182">Solution</span></span>

<span data-ttu-id="47e2a-183">인증서의 데이터에 줄 바꿈(캐리지 리턴)과 같은 유효하지 않은 문자가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-183">Make sure that the data in the certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="47e2a-184">전체 값은 한 줄이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-184">The entire value should be one long line.</span></span> <span data-ttu-id="47e2a-185">다음 텍스트는 인증서의 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-185">The following text is a sample of the certificate:</span></span>

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

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-resource-name-is-invalid"></a><span data-ttu-id="47e2a-186">Azure Portal 오류: VPN 게이트웨이를 저장하지 못했으며 리소스 이름이 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-186">Azure portal error: Failed to save the VPN gateway, and the resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="47e2a-187">증상</span><span class="sxs-lookup"><span data-stu-id="47e2a-187">Symptom</span></span>

<span data-ttu-id="47e2a-188">Azure Portal에서 VPN Gateway에 변경 내용을 저장하려고 할 때 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-188">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span> 

<span data-ttu-id="47e2a-189">**가상 네트워크 게이트웨이 &lt;*게이트웨이 이름*&gt;을 저장하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-189">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="47e2a-190">리소스 이름 &lt;*업로드하려는 인증서 이름*&gt;이 유효하지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="47e2a-190">Resource name &lt;*certificate name you try to upload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="47e2a-191">원인</span><span class="sxs-lookup"><span data-stu-id="47e2a-191">Cause</span></span>

<span data-ttu-id="47e2a-192">이 문제는 인증서의 이름이 공백과 같은 유효하지 않은 문자를 포함하기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-192">This problem occurs because the name of the certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="47e2a-193">Azure Portal 오류: VPN 패키지 파일 다운로드 오류 503</span><span class="sxs-lookup"><span data-stu-id="47e2a-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="47e2a-194">증상</span><span class="sxs-lookup"><span data-stu-id="47e2a-194">Symptom</span></span>

<span data-ttu-id="47e2a-195">VPN 클라이언트 구성 패키지를 다운로드하려고 할 때 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-195">When you try to download the VPN client configuration package, you receive the following error message:</span></span>

<span data-ttu-id="47e2a-196">**파일을 다운로드하지 못했습니다. 오류 세부 정보: 오류 503 서버가 사용 중입니다.**</span><span class="sxs-lookup"><span data-stu-id="47e2a-196">**Failed to download the file. Error details: error 503. The server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="47e2a-197">해결 방법</span><span class="sxs-lookup"><span data-stu-id="47e2a-197">Solution</span></span>

<span data-ttu-id="47e2a-198">이 오류는 임시 네트워크 문제로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="47e2a-199">VPN 패키지를 몇 분 후에 다시 다운로드해봅니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-199">Try to download the VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-to-connect"></a><span data-ttu-id="47e2a-200">Azure VPN Gateway 업그레이드: 모든 P2S 클라이언트를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-200">Azure VPN Gateway upgrade: All P2S clients are unable to connect</span></span>

### <a name="cause"></a><span data-ttu-id="47e2a-201">원인</span><span class="sxs-lookup"><span data-stu-id="47e2a-201">Cause</span></span>

<span data-ttu-id="47e2a-202">인증서가 수명의 50%를 넘는 경우 롤오버됩니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-202">If the certificate is more than 50 percent through its lifetime, the certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="47e2a-203">해결 방법</span><span class="sxs-lookup"><span data-stu-id="47e2a-203">Solution</span></span>

<span data-ttu-id="47e2a-204">이 문제를 해결하려면 VPN 클라이언트에 새 인증서를 만들고 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-204">To resolve this problem, create and redistribute new certificates to the VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="47e2a-205">한 번에 너무 많은 VPN 클라이언트 연결</span><span class="sxs-lookup"><span data-stu-id="47e2a-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="47e2a-206">각 VPN Gateway의 최대 허용 연결 수는 128개입니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-206">For each VPN gateway, the maximum number of allowable connections is 128.</span></span> <span data-ttu-id="47e2a-207">Azure Portal에서 연결된 클라이언트의 총 수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-207">You can see the total number of connected clients in the Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-to-the-route-table"></a><span data-ttu-id="47e2a-208">지점 및 사이트 간 VPN은 10.0.0.0/8의 경로를 경로 테이블에 올바르게 않게 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 to the route table</span></span>

### <a name="symptom"></a><span data-ttu-id="47e2a-209">증상</span><span class="sxs-lookup"><span data-stu-id="47e2a-209">Symptom</span></span>

<span data-ttu-id="47e2a-210">지점 및 사이트 간 클라이언트에서 VPN 연결을 사용하는 경우 VPN 클라이언트는 Azure 가상 네트워크에 대한 경로를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-210">When you dial the VPN connection on the point-to-site client, the VPN client should add a route toward the Azure virtual network.</span></span> <span data-ttu-id="47e2a-211">IP 도우미 서비스는 VPN 클라이언트의 서브넷에 대한 경로를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-211">The IP helper service should add a route for the subnet of the VPN clients.</span></span> 

<span data-ttu-id="47e2a-212">VPN 클라이언트 범위는 10.0.12.0/24와 같은 10.0.0.0/8의 더 작은 서브넷에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-212">The VPN client range belongs to a smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="47e2a-213">10.0.12.0/24에 대한 경로 대신 우선 순위가 더 높은 10.0.0.0/8에 대한 경로가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="47e2a-214">이 잘못된 경로는 정의된 특정 경로가 없는 10.50.0.0/24와 같은 10.0.0.0/8 범위 내에서 다른 서브넷에 속할 수 있는 다른 온-프레미스 네트워크와의 연결을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-214">This incorrect route breaks connectivity with other on-premises networks that might belong to another subnet within the 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="47e2a-215">원인</span><span class="sxs-lookup"><span data-stu-id="47e2a-215">Cause</span></span>

<span data-ttu-id="47e2a-216">이 동작은 Windows 클라이언트용으로 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="47e2a-217">클라이언트가 PPP IPCP 프로토콜을 사용하는 경우 서버(이 경우에 VPN 게이트웨이)의 터널 인터페이스에 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-217">When the client uses the PPP IPCP protocol, it obtains the IP address for the tunnel interface from the server (the VPN gateway in this case).</span></span> <span data-ttu-id="47e2a-218">그러나 프로토콜의 제한 사항 때문에 클라이언트에는 서브넷 마스크가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-218">However, because of a limitation in the protocol, the client does not have the subnet mask.</span></span> <span data-ttu-id="47e2a-219">가져올 다른 방법이 없기 때문에 클라이언트는 터널 인터페이스 IP 주소의 클래스에 따라 서브넷 마스크를 추측하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-219">Because there is no other way to get it, the client tries to guess the subnet mask based on the class of the tunnel interface IP address.</span></span> 

<span data-ttu-id="47e2a-220">따라서 다음과 같은 고정 매핑에 따라 경로가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-220">Therefore, a route is added based on the following static mapping:</span></span> 

<span data-ttu-id="47e2a-221">주소가 클래스 A에 속하는 경우 --> /8 적용</span><span class="sxs-lookup"><span data-stu-id="47e2a-221">If address belongs to class A --> apply /8</span></span>

<span data-ttu-id="47e2a-222">주소가 클래스 B에 속하는 경우 --> /16 적용</span><span class="sxs-lookup"><span data-stu-id="47e2a-222">If address belongs to class B --> apply /16</span></span>

<span data-ttu-id="47e2a-223">주소가 클래스 C에 속하는 경우 --> /24 적용</span><span class="sxs-lookup"><span data-stu-id="47e2a-223">If address belongs to class C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="47e2a-224">VPN 클라이언트는 네트워크 파일 공유에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="47e2a-225">증상</span><span class="sxs-lookup"><span data-stu-id="47e2a-225">Symptom</span></span>

<span data-ttu-id="47e2a-226">VPN 클라이언트가 Azure 가상 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-226">The VPN client has connected to the Azure virtual network.</span></span> <span data-ttu-id="47e2a-227">그러나 클라이언트는 네트워크 공유에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-227">However, the client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="47e2a-228">원인</span><span class="sxs-lookup"><span data-stu-id="47e2a-228">Cause</span></span>

<span data-ttu-id="47e2a-229">SMB 프로토콜은 파일 공유 액세스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-229">The SMB protocol is used for file share access.</span></span> <span data-ttu-id="47e2a-230">연결을 시작할 때 VPN 클라이언트는 세션 자격 증명을 추가하고 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-230">When the connection is initiated, the VPN client adds the session credentials and the failure occurs.</span></span> <span data-ttu-id="47e2a-231">연결이 설정되면 클라이언트는 Kerberos 인증에 캐시 자격 증명을 사용하도록 강제됩니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-231">After the connection is established, the client is forced to use the cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="47e2a-232">이 프로세스는 토큰을 가져오는 키 배포 센터(도메인 컨트롤러)에 대한 쿼리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-232">This process initiates queries to the Key Distribution Center (a domain controller) to get a token.</span></span> <span data-ttu-id="47e2a-233">클라이언트가 인터넷에 연결되기 때문에 도메인 컨트롤러에 도달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-233">Because the client connects from the Internet, it might not be able to reach the domain controller.</span></span> <span data-ttu-id="47e2a-234">따라서 클라이언트는 Kerberos에서 NTLM으로 장애 조치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-234">Therefore, the client cannot fail over from Kerberos to NTLM.</span></span> 

<span data-ttu-id="47e2a-235">클라이언트에 자격 증명에 대한 메시지가 표시되는 유일한 시점은 연결된 도메인에서 발급된 유효한 인증서(SAN=UPN)를 갖고 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-235">The only time that the client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by the domain to which it is joined.</span></span> <span data-ttu-id="47e2a-236">클라이언트도 도메인 네트워크에 물리적으로 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-236">The client also must be physically connected to the domain network.</span></span> <span data-ttu-id="47e2a-237">이 경우에 클라이언트는 인증서를 사용하고 도메인 컨트롤러에 도달하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-237">In this case, the client tries to use the certificate and reaches out to the domain controller.</span></span> <span data-ttu-id="47e2a-238">그런 다음 키 배포 센터는 "KDC_ERR_C_PRINCIPAL_UNKNOWN" 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-238">Then the Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="47e2a-239">클라이언트를 NTLM으로 장애 조치하도록 강제합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-239">The client is forced to fail over to NTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="47e2a-240">해결 방법</span><span class="sxs-lookup"><span data-stu-id="47e2a-240">Solution</span></span>

<span data-ttu-id="47e2a-241">문제를 해결하려면 다음 레지스트리 하위 키의 도메인 자격 증명 캐싱을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-241">To work around the problem, disable the caching of domain credentials from the following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set the value to 1 


## <a name="cannot-find-the-point-to-site-vpn-connection-in-windows-after-reinstalling-the-vpn-client"></a><span data-ttu-id="47e2a-242">VPN 클라이언트를 다시 설치한 후에 Windows에서 지점 및 사이트 간 VPN 연결을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-242">Cannot find the point-to-site VPN connection in Windows after reinstalling the VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="47e2a-243">증상</span><span class="sxs-lookup"><span data-stu-id="47e2a-243">Symptom</span></span>

<span data-ttu-id="47e2a-244">지점 및 사이트 간 VPN 연결을 제거한 다음 VPN 클라이언트를 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-244">You remove the point-to-site VPN connection and then reinstall the VPN client.</span></span> <span data-ttu-id="47e2a-245">이 경우에 VPN 연결이 성공적으로 구성되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-245">In this situation, the VPN connection is not configured successfully.</span></span> <span data-ttu-id="47e2a-246">VPN 연결이 Windows의 **네트워크 연결** 설정에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-246">You do not see the VPN connection in the **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="47e2a-247">해결 방법</span><span class="sxs-lookup"><span data-stu-id="47e2a-247">Solution</span></span>

<span data-ttu-id="47e2a-248">이 문제를 해결하려면 **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**에서 기존 VPN 클라이언트 구성 파일을 삭제하고 VPN 클라이언트 설치 프로그램을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47e2a-248">To resolve the problem, delete the old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run the VPN client installer again.</span></span>
