---
title: "지점 및 사이트 간에 대한 인증서 생성 및 내보내기: PowerShell: Azure | Microsoft Docs"
description: "이 문서의 단계 toocreate 자체 서명 된 루트 인증서를 포함 하 고 hello 공개 키를 내보내고 Windows 10에서 PowerShell을 사용 하 여 클라이언트 인증서를 생성 합니다."
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
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="e62a2-103">Windows 10에서 PowerShell을 사용하여 지점 및 사이트 간 연결에 대한 인증서 생성 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="e62a2-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="e62a2-104">지점 및 사이트 연결 tooauthenticate 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="e62a2-105">이 문서는 toocreate는 자체 서명 된 루트 인증서 방법을 보여 줍니다 하 고 Windows 10에서 PowerShell을 사용 하 여 클라이언트 인증서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="e62a2-106">찾으려는 경우 지점-사이트 구성 단계에 대 한 방법을 tooupload 루트 인증서를 다음 hello 기사 hello ' 구성 지점 및 사이트 간 ' 중 하나를 선택 목록 등.</span><span class="sxs-lookup"><span data-stu-id="e62a2-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e62a2-107">자체 서명된 인증서 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="e62a2-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="e62a2-108">자체 서명된 인증서 만들기 - MakeCert</span><span class="sxs-lookup"><span data-stu-id="e62a2-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="e62a2-109">지점 및 사이트 간 구성 - Resource Manager - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e62a2-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="e62a2-110">지점 및 사이트 간 구성 - Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="e62a2-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="e62a2-111">지점 및 사이트 간 구성 - Classic - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e62a2-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="e62a2-112">Windows 10을 실행 하는 컴퓨터에이 문서의 hello 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-112">You must perform hello steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="e62a2-113">hello PowerShell cmdlet toogenerate 인증서를 사용 하는 hello Windows 10 운영 체제의 일부 이며 다른 버전의 Windows에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-113">hello PowerShell cmdlets that you use toogenerate certificates are part of hello Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="e62a2-114">hello Windows 10 컴퓨터는 필요한 toogenerate hello 인증서만 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-114">hello Windows 10 computer is only needed toogenerate hello certificates.</span></span> <span data-ttu-id="e62a2-115">생성 된 hello 인증서는, 업로드 하거나 모든 지원 되는 클라이언트 운영 체제에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-115">Once hello certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="e62a2-116">액세스 tooa Windows 10 컴퓨터가 없는 경우 사용할 수 있습니다 [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-116">If you do not have access tooa Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificates.</span></span> <span data-ttu-id="e62a2-117">hello 두 방법 중 하나를 사용 하 여 생성 하는 수에 인증서를 설치할 모든 [지원](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) 클라이언트 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-117">hello certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="e62a2-118"><a name="rootcert"></a>자체 서명된 루트 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="e62a2-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="e62a2-119">Hello New-selfsignedcertificate cmdlet toocreate 자체 서명 된 루트 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-119">Use hello New-SelfSignedCertificate cmdlet toocreate a self-signed root certificate.</span></span> <span data-ttu-id="e62a2-120">추가 매개 변수 정보는 [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e62a2-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="e62a2-121">Windows 10을 실행하는 컴퓨터에서 상승된 권한으로 Windows PowerShell 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="e62a2-122">다음 예에서는 toocreate hello 자체 서명 된 루트 인증서 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-122">Use hello following example toocreate hello self-signed root certificate.</span></span> <span data-ttu-id="e62a2-123">hello 다음 예제에서는 ' 인증서-현재 User\Personal\Certificates'에 자동으로 설치 되는 ' P2SRootCert' 라는 자체 서명 된 루트 인증서</span><span class="sxs-lookup"><span data-stu-id="e62a2-123">hello following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="e62a2-124">열어 hello 인증서를 볼 수 있습니다 *certmgr.msc*, 또는 *사용자 인증서 관리*합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-124">You can view hello certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="e62a2-125"><a name="cer"></a>내보내기 hello 공개 키 (.cer)</span><span class="sxs-lookup"><span data-stu-id="e62a2-125"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="e62a2-126">hello exported.cer 파일 업로드 tooAzure 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-126">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="e62a2-127">자세한 내용은 [지점 및 사이트 간 연결 구성](vpn-gateway-howto-point-to-site-rm-ps.md#upload)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e62a2-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="e62a2-128">신뢰할 수 있는 루트 인증서가 tooadd [이 섹션](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) hello 문서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-128">tooadd an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of hello article.</span></span>

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a><span data-ttu-id="e62a2-129">Hello 자체 서명 된 루트 인증서와 공개 키 toostore 내보낼 것 (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="e62a2-129">Export hello self-signed root certificate and public key toostore it (optional)</span></span>

<span data-ttu-id="e62a2-130">Tooexport hello 자체 서명 된 루트 인증서를 안전 하 게 저장을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-130">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="e62a2-131">필요한 경우 나중에 다른 컴퓨터에서 해당 인증서를 설치하고 더 많은 클라이언트 인증서를 생성하거나 다른 .cer 파일을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="e62a2-132">tooexport hello 루트 인증서를.pfx, 루트 인증서 선택 hello 및 사용 하 여 동일한 단계에 설명 된 대로 hello로 자체 서명 된 [클라이언트 인증서 내보내기](#clientexport)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-132">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="e62a2-133"><a name="clientcert"></a>클라이언트 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="e62a2-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="e62a2-134">Tooa 연결 하는 각 클라이언트 컴퓨터 VNet 지점-사이트를 사용 하 여 클라이언트 인증서가 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-134">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="e62a2-135">Hello 자체 서명 된 루트 인증서에서 클라이언트 인증서를 생성 하 고 내보낸 hello 클라이언트 인증서를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-135">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="e62a2-136">Hello 클라이언트 인증서 설치 되어 있지 않으면 인증이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-136">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="e62a2-137">hello 다음 단계에 관한 자체 서명 된 루트 인증서에서 클라이언트 인증서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-137">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="e62a2-138">Hello에서 여러 클라이언트 인증서를 생성할 수 있습니다 동일한 루트 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-138">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="e62a2-139">다음 hello 단계를 사용 하 여 클라이언트 인증서를 생성할 때 hello 클라이언트 인증서가 자동으로 컴퓨터에 설치 hello toogenerate hello 인증서를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-139">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="e62a2-140">Tooinstall 다른 클라이언트 컴퓨터에서 클라이언트 인증서를 사용 하도록 하려는 경우에 hello 인증서를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-140">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>

<span data-ttu-id="e62a2-141">hello 예제 hello New-selfsignedcertificate cmdlet toogenerate 1 년이 지나면 만료 되는 클라이언트 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-141">hello examples use hello New-SelfSignedCertificate cmdlet toogenerate a client certificate that expires in one year.</span></span> <span data-ttu-id="e62a2-142">Hello 클라이언트 인증서에 대 한 다른 만료 값을 설정 하는 등의 추가 매개 변수 정보를 참조 하십시오. [New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-142">For additional parameter information, such as setting a different expiration value for hello client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="e62a2-143">예 1</span><span class="sxs-lookup"><span data-stu-id="e62a2-143">Example 1</span></span>

<span data-ttu-id="e62a2-144">이 예제는 hello 이전 섹션에서 '$cert' 변수를 선언 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-144">This example uses hello declared '$cert' variable from hello previous section.</span></span> <span data-ttu-id="e62a2-145">hello 단계를 사용 하 여 hello 자체 서명 된 루트 인증서를 만들거나 추가 클라이언트 인증서에서에서 만드는 새 PowerShell 콘솔 세션 후 hello PowerShell 콘솔을 닫은 경우 [예 2](#ex2)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-145">If you closed hello PowerShell console after creating hello self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use hello steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="e62a2-146">수정 하 고 hello 예제 toogenerate 클라이언트 인증서를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-146">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="e62a2-147">다음 예에서는 수정 하지 않고 hello를 실행 하는 경우 hello 결과 'P2SChildCert' 이라는 클라이언트 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-147">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="e62a2-148">다른 값인지 tooname hello 자식 인증서 원한다 면 hello CN 값을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-148">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="e62a2-149">이 예제를 실행 하는 경우에 hello TextExtension를 변경 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="e62a2-149">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="e62a2-150">자동으로 생성 하는 hello 클라이언트 인증서는 컴퓨터에 '인증서-Current User\Personal\Certificates'에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-150">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="e62a2-151"><a name="ex2"></a>예 2</span><span class="sxs-lookup"><span data-stu-id="e62a2-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="e62a2-152">추가 클라이언트 인증서를 만드는 경우 또는 동일한 hello를 사용 하지는 PowerShell 세션을 사용 하 여 toocreate 자체 서명 된 루트 인증서를 사용 하 여 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-152">If you are creating additional client certificates, or are not using hello same PowerShell session that you used toocreate your self-signed root certificate, use hello following steps:</span></span>

1. <span data-ttu-id="e62a2-153">Hello 컴퓨터에 설치 되어 있는 hello 자체 서명 된 루트 인증서를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-153">Identify hello self-signed root certificate that is installed on hello computer.</span></span> <span data-ttu-id="e62a2-154">이 cmdlet은 컴퓨터에 설치된 인증서 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="e62a2-155">즉, 다음 위치에 tooit tooa 텍스트 복사 hello 지문 목록에서 반환 되는 hello로 hello 주체 이름의 찾을 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-155">Locate hello subject name from hello returned list, then copy hello thumbprint that is located next tooit tooa text file.</span></span> <span data-ttu-id="e62a2-156">다음 예제는 hello에 두 개의 인증서.</span><span class="sxs-lookup"><span data-stu-id="e62a2-156">In hello following example, there are two certificates.</span></span> <span data-ttu-id="e62a2-157">hello CN 이름은 toogenerate 자식 인증서를 제거할 hello 자체 서명 된 루트 인증서의 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-157">hello CN name is hello name of hello self-signed root certificate from which you want toogenerate a child certificate.</span></span> <span data-ttu-id="e62a2-158">이 경우에는 'P2SRootCert'입니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="e62a2-159">Hello 이전 단계의 hello 지문을 사용 하 여 hello 루트 인증서에 대 한 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-159">Declare a variable for hello root certificate using hello thumbprint from hello previous step.</span></span> <span data-ttu-id="e62a2-160">지문을 toogenerate 자식 인증서를 제거할 hello 루트 인증서의 hello 지 문으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-160">Replace THUMBPRINT with hello thumbprint of hello root certificate from which you want toogenerate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="e62a2-161">예를 들어 P2SRootCert에 대 한 hello 지문을 사용 하 여 hello 이전 단계에서 hello 변수 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-161">For example, using hello thumbprint for P2SRootCert in hello previous step, hello variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="e62a2-162">수정 하 고 hello 예제 toogenerate 클라이언트 인증서를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-162">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="e62a2-163">다음 예에서는 수정 하지 않고 hello를 실행 하는 경우 hello 결과 'P2SChildCert' 이라는 클라이언트 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-163">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="e62a2-164">다른 값인지 tooname hello 자식 인증서 원한다 면 hello CN 값을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-164">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="e62a2-165">이 예제를 실행 하는 경우에 hello TextExtension를 변경 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="e62a2-165">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="e62a2-166">자동으로 생성 하는 hello 클라이언트 인증서는 컴퓨터에 '인증서-Current User\Personal\Certificates'에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-166">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="e62a2-167"><a name="clientexport"></a>클라이언트 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="e62a2-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="e62a2-168"><a name="install"></a>내보낸 클라이언트 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="e62a2-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e62a2-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e62a2-169">Next steps</span></span>

<span data-ttu-id="e62a2-170">지점 및 사이트 간 구성을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="e62a2-171">에 대 한 **리소스 관리자** 배포 모델 단계 참조 [지점 및 사이트 연결 tooa VNet 구성](vpn-gateway-howto-point-to-site-resource-manager-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="e62a2-172">에 대 한 **클래식** 배포 모델 단계 참조 [지점-사이트 VPN 연결 tooa VNet (클래식)를 구성](vpn-gateway-howto-point-to-site-classic-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62a2-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
