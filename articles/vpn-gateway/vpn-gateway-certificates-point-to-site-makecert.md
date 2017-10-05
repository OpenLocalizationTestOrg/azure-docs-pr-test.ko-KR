---
title: "지점 및 사이트 간에 대한 인증서 생성 및 내보내기: MakeCert: Azure | Microsoft Docs"
description: "이 문서에는 MakeCert를 사용하여 자체 서명된 루트 인증서를 만들고, 공용 키를 내보내고, 클라이언트 인증서를 생성하는 단계가 나와 있습니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 4c51edac3b1cdafae8f9543bd0e3133b6a050f73
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a><span data-ttu-id="647f6-103">MakeCert를 사용하여 지점 및 사이트 간 연결에 대한 인증서 생성 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="647f6-103">Generate and export certificates for Point-to-Site connections using MakeCert</span></span>

<span data-ttu-id="647f6-104">지점 및 사이트 간 연결은 인증서를 사용하여 인증을 합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-104">Point-to-Site connections use certificates to authenticate.</span></span> <span data-ttu-id="647f6-105">이 문서에서는 MakeCert를 사용하여 자체 서명된 루트 인증서를 만들고 클라이언트 인증서를 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-105">This article shows you how to create a self-signed root certificate and generate client certificates using MakeCert.</span></span> <span data-ttu-id="647f6-106">루트 인증서 업로드 방법 등 지점 및 사이트 간 구성 단계를 찾고 있는 경우 다음 목록에서 '지점 및 사이트 간 구성' 문서 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-106">If you are looking for Point-to-Site configuration steps, such as how to upload root certificates, select one of the 'Configure Point-to-Site' articles from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="647f6-107">자체 서명된 인증서 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="647f6-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="647f6-108">자체 서명된 인증서 만들기 - MakeCert</span><span class="sxs-lookup"><span data-stu-id="647f6-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="647f6-109">지점 및 사이트 간 구성 - Resource Manager - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="647f6-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="647f6-110">지점 및 사이트 간 구성 - Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="647f6-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="647f6-111">지점 및 사이트 간 구성 - Classic - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="647f6-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

<span data-ttu-id="647f6-112">[Windows 10 PowerShell 단계](vpn-gateway-certificates-point-to-site.md)를 사용하여 인증서를 만드는 것이 좋지만 하나의 선택적 방법으로 이러한 MakeCert 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-112">While we recommend using the [Windows 10 PowerShell steps](vpn-gateway-certificates-point-to-site.md) to create your certificates, we provide these MakeCert instructions as an optional method.</span></span> <span data-ttu-id="647f6-113">두 방법 중 하나를 사용하여 생성하는 인증서는 [지원되는 모든 클라이언트 운영 체제](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-113">The certificates that you generate using either method can be installed on [any supported client operating system](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq).</span></span> <span data-ttu-id="647f6-114">그러나 MakeCert에는 다음과 같은 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-114">However, MakeCert has the following limitation:</span></span>

* <span data-ttu-id="647f6-115">MakeCert는 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-115">MakeCert is deprecated.</span></span> <span data-ttu-id="647f6-116">즉, 언제든지 이 도구가 제거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-116">This means that this tool could be removed at any point.</span></span> <span data-ttu-id="647f6-117">MakeCert를 더 이상 사용할 수 없는 경우 MakeCert를 사용하여 이미 생성한 인증서는 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-117">Any certificates that you already generated using MakeCert won't be affected when MakeCert is no longer available.</span></span> <span data-ttu-id="647f6-118">MakeCert는 메커니즘 유효성 검사에 사용되지 않으며 인증서를 생성하는 데에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-118">MakeCert is only used to generate the certificates, not as a validating mechanism.</span></span>

## <span data-ttu-id="647f6-119"><a name="rootcert"></a>자체 서명된 루트 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="647f6-119"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="647f6-120">다음 단계에서는 MakeCert를 사용하여 자체 서명된 인증서를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-120">The following steps show you how to create a self-signed certificate using MakeCert.</span></span> <span data-ttu-id="647f6-121">이러한 단계는 배포 모델에 한정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-121">These steps are not deployment-model specific.</span></span> <span data-ttu-id="647f6-122">리소스 관리자와 클래식에 대해 모두 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-122">They are valid for both Resource Manager and classic.</span></span>

1. <span data-ttu-id="647f6-123">[MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx)를 다운로드 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-123">Download and install [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).</span></span>
2. <span data-ttu-id="647f6-124">설치가 끝나면 일반적으로 'C:\Program Files (x86)\Windows Kits\10\bin\<arch>' 경로 아래에서 makecert.exe 유틸리티를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-124">After installation, you can typically find the makecert.exe utility under this path: 'C:\Program Files (x86)\Windows Kits\10\bin\<arch>'.</span></span> <span data-ttu-id="647f6-125">하지만 다른 위치에 설치되었을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-125">Although, it's possible that it was installed to another location.</span></span> <span data-ttu-id="647f6-126">관리자 권한으로 명령 프롬프트를 열고 MakeCert 유틸리티의 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-126">Open a command prompt as administrator and navigate to the location of the MakeCert utility.</span></span> <span data-ttu-id="647f6-127">적절한 위치에 대해 조정하여 다음 예제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-127">You can use the following example, adjusting for the proper location:</span></span>

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. <span data-ttu-id="647f6-128">사용자 컴퓨터의 개인 인증서 저장소에 인증서를 만들고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-128">Create and install a certificate in the Personal certificate store on your computer.</span></span> <span data-ttu-id="647f6-129">다음 예제에서는 P2S를 구성할 때 Azure에 업로드하는 해당 *.cer* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-129">The following example creates a corresponding *.cer* file that you upload to Azure when configuring P2S.</span></span> <span data-ttu-id="647f6-130">'P2SRootCert' 및 'P2SRootCert.cer'을 인증서에 사용하려는 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-130">Replace 'P2SRootCert' and 'P2SRootCert.cer' with the name that you want to use for the certificate.</span></span> <span data-ttu-id="647f6-131">인증서는 'Certificates - Current User\Personal\Certificates'에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-131">The certificate is located in your 'Certificates - Current User\Personal\Certificates'.</span></span>

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <span data-ttu-id="647f6-132"><a name="cer"></a>공개 키(.cer) 내보내기</span><span class="sxs-lookup"><span data-stu-id="647f6-132"><a name="cer"></a>Export the public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="647f6-133">exported.cer 파일을 Azure에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-133">The exported.cer file must be uploaded to Azure.</span></span> <span data-ttu-id="647f6-134">자세한 내용은 [지점 및 사이트 간 연결 구성](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="647f6-134">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile).</span></span> <span data-ttu-id="647f6-135">신뢰할 수 있는 루트 인증서를 추가하려면 문서의 [이 섹션](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="647f6-135">To add an additional trusted root certificate, see [this section](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) of the article.</span></span>

### <a name="export-the-self-signed-certificate-and-private-key-to-store-it-optional"></a><span data-ttu-id="647f6-136">자체 서명된 인증서 및 개인 키를 내보낸 다음 저장(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="647f6-136">Export the self-signed certificate and private key to store it (optional)</span></span>

<span data-ttu-id="647f6-137">자체 서명된 루트 인증서를 내보낸 다음 안전하게 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-137">You may want to export the self-signed root certificate and store it safely.</span></span> <span data-ttu-id="647f6-138">필요한 경우 나중에 다른 컴퓨터에서 해당 인증서를 설치하고 더 많은 클라이언트 인증서를 생성하거나 다른 .cer 파일을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-138">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="647f6-139">자체 서명된 루트 인증서를 .pfx로 내보내려면 루트 인증서를 선택하고 [클라이언트 인증서 내보내기](#clientexport)에서 설명하는 것과 같은 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-139">To export the self-signed root certificate as a .pfx, select the root certificate and use the same steps as described in [Export a client certificate](#clientexport).</span></span>

## <a name="create-and-install-client-certificates"></a><span data-ttu-id="647f6-140">클라이언트 인증서 만들기 및 설치</span><span class="sxs-lookup"><span data-stu-id="647f6-140">Create and install client certificates</span></span>

<span data-ttu-id="647f6-141">자체 서명된 인증서를 클라이언트 컴퓨터에 직접 설치하지는 않으며,</span><span class="sxs-lookup"><span data-stu-id="647f6-141">You don't install the self-signed certificate directly on the client computer.</span></span> <span data-ttu-id="647f6-142">자체 서명된 인증서에서 클라이언트 인증서를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-142">You need to generate a client certificate from the self-signed certificate.</span></span> <span data-ttu-id="647f6-143">그런 다음 클라이언트 인증서를 클라이언트 컴퓨터로 내보낸 후 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-143">You then export and install the client certificate to the client computer.</span></span> <span data-ttu-id="647f6-144">이러한 단계는 배포 모델에 관계없이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-144">The following steps are not deployment-model specific.</span></span> <span data-ttu-id="647f6-145">리소스 관리자와 클래식에 대해 모두 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-145">They are valid for both Resource Manager and classic.</span></span>

### <span data-ttu-id="647f6-146"><a name="clientcert"></a>클라이언트 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="647f6-146"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="647f6-147">지점 및 사이트 간을 사용하여 VNet에 연결하는 각 클라이언트 컴퓨터에 클라이언트 인증서가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-147">Each client computer that connects to a VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="647f6-148">자체 서명된 루트 인증서에서 클라이언트 인증서를 생성한 후 클라이언트 인증서를 내보내고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-148">You generate a client certificate from the self-signed root certificate, and then export and install the client certificate.</span></span> <span data-ttu-id="647f6-149">클라이언트 인증서가 설치되어 있지 않으면 인증이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-149">If the client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="647f6-150">다음 단계는 자체 서명된 루트 인증서에서 클라이언트 인증서를 생성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-150">The following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="647f6-151">동일한 루트 인증서에서 여러 클라이언트 인증서를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-151">You may generate multiple client certificates from the same root certificate.</span></span> <span data-ttu-id="647f6-152">다음 단계를 사용하여 클라이언트 인증서를 생성하는 경우 클라이언트 인증서가 인증서를 생성하는 데 사용하는 컴퓨터에 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-152">When you generate client certificates using the steps below, the client certificate is automatically installed on the computer that you used to generate the certificate.</span></span> <span data-ttu-id="647f6-153">다른 클라이언트 컴퓨터에 클라이언트 인증서를 설치하려는 경우 인증서를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-153">If you want to install a client certificate on another client computer, you can export the certificate.</span></span>
 
1. <span data-ttu-id="647f6-154">자체 서명된 인증서를 만드는 데 사용한 동일한 컴퓨터에서 관리자로 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-154">On the same computer that you used to create the self-signed certificate, open a command prompt as administrator.</span></span>
2. <span data-ttu-id="647f6-155">샘플을 수정 및 실행하여 클라이언트 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-155">Modify and run the sample to generate a client certificate.</span></span>
  * <span data-ttu-id="647f6-156">*"P2SRootCert"*는 클라이언트 인증서를 생성 중인 자체 서명된 루트의 이름으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-156">Change *"P2SRootCert"* to the name of the self-signed root that you are generating the client certificate from.</span></span> <span data-ttu-id="647f6-157">루트 인증서의 이름을 사용하고 있는지 확인합니다. 이 경우에 'CN=' 값은 자체 서명된 루트를 만들 때 지정한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-157">Make sure you are using the name of the root certificate, which is whatever the 'CN=' value was that you specified when you created the self-signed root.</span></span>
  * <span data-ttu-id="647f6-158">*P2SChildCert*는 생성하는 클라이언트 인증서에 사용할 이름으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-158">Change *P2SChildCert* to the name you want to generate a client certificate to be.</span></span>

  <span data-ttu-id="647f6-159">다음 예제를 수정하지 않고 실행하면 루트 인증서 P2SRootCert에서 생성된 클라이언트 인증서 P2SChildcert가 개인 인증서 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-159">If you run the following example without modifying it, the result is a client certificate named P2SChildcert in your Personal certificate store that was generated from root certificate P2SRootCert.</span></span>

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <span data-ttu-id="647f6-160"><a name="clientexport"></a>클라이언트 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="647f6-160"><a name="clientexport"></a>Export a client certificate</span></span>

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <span data-ttu-id="647f6-161"><a name="install"></a>내보낸 클라이언트 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="647f6-161"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="647f6-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="647f6-162">Next steps</span></span>

<span data-ttu-id="647f6-163">지점 및 사이트 간 구성을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="647f6-163">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="647f6-164">**Resource Manager** 배포 모델 단계의 경우 [VNet에 지점 및 사이트 간 연결 구성](vpn-gateway-howto-point-to-site-resource-manager-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="647f6-164">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection to a VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span>
* <span data-ttu-id="647f6-165">**클래식** 배포 모델 단계의 경우 [VNet에 지점 및 사이트 간 VPN 연결 구성(클래식)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="647f6-165">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection to a VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
