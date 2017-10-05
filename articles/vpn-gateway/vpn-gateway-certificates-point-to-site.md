---
title: "지점 및 사이트 간에 대한 인증서 생성 및 내보내기: PowerShell: Azure | Microsoft Docs"
description: "이 문서에는 Windows 10의 PowerShell을 사용하여 자체 서명된 루트 인증서를 만들고, 공용 키를 내보내고, 클라이언트 인증서를 생성하는 단계가 나와 있습니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: f96b9b212b9322d0677e49ff95184d0feccca2df
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="6b37e-103">Windows 10에서 PowerShell을 사용하여 지점 및 사이트 간 연결에 대한 인증서 생성 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="6b37e-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="6b37e-104">지점 및 사이트 간 연결은 인증서를 사용하여 인증을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-104">Point-to-Site connections use certificates to authenticate.</span></span> <span data-ttu-id="6b37e-105">이 문서에서는 Windows 10에서 PowerShell을 사용하여 자체 서명된 루트 인증서를 만들고 클라이언트 인증서를 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-105">This article shows you how to create a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="6b37e-106">루트 인증서 업로드 방법 등 지점 및 사이트 간 구성 단계를 찾고 있는 경우 다음 목록에서 '지점 및 사이트 간 구성' 문서 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-106">If you are looking for Point-to-Site configuration steps, such as how to upload root certificates, select one of the 'Configure Point-to-Site' articles from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b37e-107">자체 서명된 인증서 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b37e-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="6b37e-108">자체 서명된 인증서 만들기 - MakeCert</span><span class="sxs-lookup"><span data-stu-id="6b37e-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="6b37e-109">지점 및 사이트 간 구성 - Resource Manager - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6b37e-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="6b37e-110">지점 및 사이트 간 구성 - Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b37e-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="6b37e-111">지점 및 사이트 간 구성 - Classic - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6b37e-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="6b37e-112">Windows 10을 실행하는 컴퓨터에서 이 문서의 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-112">You must perform the steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="6b37e-113">인증서를 생성하는 데 사용하는 PowerShell cmdlet은 Windows 10 운영 체제의 일부이며 다른 Windows 버전에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-113">The PowerShell cmdlets that you use to generate certificates are part of the Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="6b37e-114">Windows 10 컴퓨터는 인증서 생성에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-114">The Windows 10 computer is only needed to generate the certificates.</span></span> <span data-ttu-id="6b37e-115">인증서를 생성한 후에는 지원되는 모든 클라이언트 운영 체제에 업로드하거나 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-115">Once the certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="6b37e-116">Windows 10 컴퓨터에 액세스할 수 없는 경우 [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)를 사용하여 인증서를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-116">If you do not have access to a Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) to generate certificates.</span></span> <span data-ttu-id="6b37e-117">두 방법 중 하나를 사용하여 생성하는 인증서는 [지원되는](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) 모든 클라이언트 운영 체제에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-117">The certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="6b37e-118"><a name="rootcert"></a>자체 서명된 루트 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="6b37e-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="6b37e-119">New-SelfSignedCertificate cmdlet을 사용하여 자체 서명된 루트 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-119">Use the New-SelfSignedCertificate cmdlet to create a self-signed root certificate.</span></span> <span data-ttu-id="6b37e-120">추가 매개 변수 정보는 [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b37e-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="6b37e-121">Windows 10을 실행하는 컴퓨터에서 상승된 권한으로 Windows PowerShell 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="6b37e-122">다음 예제를 사용하여 자체 서명된 루트 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-122">Use the following example to create the self-signed root certificate.</span></span> <span data-ttu-id="6b37e-123">다음 예제에서는 'Certificates-Current User\Personal\Certificates'에 자동으로 설치된 'P2SRootCert'라는 자체 서명된 루트 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-123">The following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="6b37e-124">*certmgr.msc* 또는 *사용자 인증서 관리*를 열어 인증서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-124">You can view the certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="6b37e-125"><a name="cer"></a>공개 키(.cer) 내보내기</span><span class="sxs-lookup"><span data-stu-id="6b37e-125"><a name="cer"></a>Export the public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="6b37e-126">exported.cer 파일을 Azure에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-126">The exported.cer file must be uploaded to Azure.</span></span> <span data-ttu-id="6b37e-127">자세한 내용은 [지점 및 사이트 간 연결 구성](vpn-gateway-howto-point-to-site-rm-ps.md#upload)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b37e-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="6b37e-128">신뢰할 수 있는 루트 인증서를 추가하려면 문서의 [이 섹션](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b37e-128">To add an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of the article.</span></span>

### <a name="export-the-self-signed-root-certificate-and-public-key-to-store-it-optional"></a><span data-ttu-id="6b37e-129">자체 서명된 루트 인증서 및 공개 키를 내보낸 다음 저장(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="6b37e-129">Export the self-signed root certificate and public key to store it (optional)</span></span>

<span data-ttu-id="6b37e-130">자체 서명된 루트 인증서를 내보낸 다음 안전하게 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-130">You may want to export the self-signed root certificate and store it safely.</span></span> <span data-ttu-id="6b37e-131">필요한 경우 나중에 다른 컴퓨터에서 해당 인증서를 설치하고 더 많은 클라이언트 인증서를 생성하거나 다른 .cer 파일을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="6b37e-132">자체 서명된 루트 인증서를 .pfx로 내보내려면 루트 인증서를 선택하고 [클라이언트 인증서 내보내기](#clientexport)에서 설명하는 것과 같은 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-132">To export the self-signed root certificate as a .pfx, select the root certificate and use the same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="6b37e-133"><a name="clientcert"></a>클라이언트 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="6b37e-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="6b37e-134">지점 및 사이트 간을 사용하여 VNet에 연결하는 각 클라이언트 컴퓨터에 클라이언트 인증서가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-134">Each client computer that connects to a VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="6b37e-135">자체 서명된 루트 인증서에서 클라이언트 인증서를 생성한 후 클라이언트 인증서를 내보내고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-135">You generate a client certificate from the self-signed root certificate, and then export and install the client certificate.</span></span> <span data-ttu-id="6b37e-136">클라이언트 인증서가 설치되어 있지 않으면 인증이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-136">If the client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="6b37e-137">다음 단계는 자체 서명된 루트 인증서에서 클라이언트 인증서를 생성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-137">The following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="6b37e-138">동일한 루트 인증서에서 여러 클라이언트 인증서를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-138">You may generate multiple client certificates from the same root certificate.</span></span> <span data-ttu-id="6b37e-139">다음 단계를 사용하여 클라이언트 인증서를 생성하는 경우 클라이언트 인증서가 인증서를 생성하는 데 사용하는 컴퓨터에 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-139">When you generate client certificates using the steps below, the client certificate is automatically installed on the computer that you used to generate the certificate.</span></span> <span data-ttu-id="6b37e-140">다른 클라이언트 컴퓨터에 클라이언트 인증서를 설치하려는 경우 인증서를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-140">If you want to install a client certificate on another client computer, you can export the certificate.</span></span>

<span data-ttu-id="6b37e-141">예제에서는 New-SelfSignedCertificate cmdlet을 사용하여 1년 후에 만료되는 클라이언트 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-141">The examples use the New-SelfSignedCertificate cmdlet to generate a client certificate that expires in one year.</span></span> <span data-ttu-id="6b37e-142">클라이언트 인증서에 대해 다른 만료 값을 설정하는 등의 추가 매개 변수 정보는 [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b37e-142">For additional parameter information, such as setting a different expiration value for the client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="6b37e-143">예 1</span><span class="sxs-lookup"><span data-stu-id="6b37e-143">Example 1</span></span>

<span data-ttu-id="6b37e-144">이 예제에서는 이전 섹션에서 선언된 '$cert' 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-144">This example uses the declared '$cert' variable from the previous section.</span></span> <span data-ttu-id="6b37e-145">자체 서명된 루트 인증서를 만든 후 PowerShell 콘솔을 종료했거나 새 PowerShell 콘솔 세션에서 추가 클라이언트 인증서를 생성하려는 경우 [예제 2](#ex2)의 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-145">If you closed the PowerShell console after creating the self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use the steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="6b37e-146">샘플을 수정 및 실행하여 클라이언트 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-146">Modify and run the example to generate a client certificate.</span></span> <span data-ttu-id="6b37e-147">다음 예제를 수정하지 않고 실행할 경우 결과적으로 'P2SChildCert'라는 클라이언트 인증서가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-147">If you run the following example without modifying it, the result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="6b37e-148">자식 인증서에 다른 이름을 지정하려는 경우 CN 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-148">If you want to name the child certificate something else, modify the CN value.</span></span> <span data-ttu-id="6b37e-149">이 예제를 실행하는 경우는 TextExtension을 변경하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6b37e-149">Do not change the TextExtension when running this example.</span></span> <span data-ttu-id="6b37e-150">생성하는 클라이언트 인증서는 컴퓨터의 'Certificates - Current User\Personal\Certificates'에 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-150">The client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="6b37e-151"><a name="ex2"></a>예 2</span><span class="sxs-lookup"><span data-stu-id="6b37e-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="6b37e-152">추가 클라이언트 인증서를 만들거나 자체 서명된 루트 인증서를 만드는 데 사용한 것과 동일한 PowerShell 세션을 사용하지 않을 경우 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-152">If you are creating additional client certificates, or are not using the same PowerShell session that you used to create your self-signed root certificate, use the following steps:</span></span>

1. <span data-ttu-id="6b37e-153">컴퓨터에 설치되어 있는 자체 서명된 루트 인증서를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-153">Identify the self-signed root certificate that is installed on the computer.</span></span> <span data-ttu-id="6b37e-154">이 cmdlet은 컴퓨터에 설치된 인증서 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="6b37e-155">반환된 목록에서 주체 이름을 찾은 다음 텍스트 파일에 옆에 있는 지문을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-155">Locate the subject name from the returned list, then copy the thumbprint that is located next to it to a text file.</span></span> <span data-ttu-id="6b37e-156">다음 예제에는 두 개의 인증서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-156">In the following example, there are two certificates.</span></span> <span data-ttu-id="6b37e-157">CN 이름은 자식 인증서를 생성하려는 자체 서명된 루트 인증서의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-157">The CN name is the name of the self-signed root certificate from which you want to generate a child certificate.</span></span> <span data-ttu-id="6b37e-158">이 경우에는 'P2SRootCert'입니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="6b37e-159">이전 단계의 지문을 사용하여 루트 인증서에 대한 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-159">Declare a variable for the root certificate using the thumbprint from the previous step.</span></span> <span data-ttu-id="6b37e-160">THUMBPRINT을 자식 인증서를 생성하려는 루트 인증서의 지문으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-160">Replace THUMBPRINT with the thumbprint of the root certificate from which you want to generate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="6b37e-161">예를 들어 이전 단계의 P2SRootCert에 대한 지문을 사용할 경우 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-161">For example, using the thumbprint for P2SRootCert in the previous step, the variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="6b37e-162">샘플을 수정 및 실행하여 클라이언트 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-162">Modify and run the example to generate a client certificate.</span></span> <span data-ttu-id="6b37e-163">다음 예제를 수정하지 않고 실행할 경우 결과적으로 'P2SChildCert'라는 클라이언트 인증서가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-163">If you run the following example without modifying it, the result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="6b37e-164">자식 인증서에 다른 이름을 지정하려는 경우 CN 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-164">If you want to name the child certificate something else, modify the CN value.</span></span> <span data-ttu-id="6b37e-165">이 예제를 실행하는 경우는 TextExtension을 변경하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6b37e-165">Do not change the TextExtension when running this example.</span></span> <span data-ttu-id="6b37e-166">생성하는 클라이언트 인증서는 컴퓨터의 'Certificates - Current User\Personal\Certificates'에 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-166">The client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="6b37e-167"><a name="clientexport"></a>클라이언트 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="6b37e-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="6b37e-168"><a name="install"></a>내보낸 클라이언트 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="6b37e-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="6b37e-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b37e-169">Next steps</span></span>

<span data-ttu-id="6b37e-170">지점 및 사이트 간 구성을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="6b37e-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="6b37e-171">**Resource Manager** 배포 모델 단계의 경우 [VNet에 지점 및 사이트 간 연결 구성](vpn-gateway-howto-point-to-site-resource-manager-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b37e-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection to a VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="6b37e-172">**클래식** 배포 모델 단계의 경우 [VNet에 지점 및 사이트 간 VPN 연결 구성(클래식)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b37e-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection to a VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>