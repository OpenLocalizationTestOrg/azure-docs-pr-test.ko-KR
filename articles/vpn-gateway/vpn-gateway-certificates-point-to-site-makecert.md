---
title: "지점 및 사이트 간에 대한 인증서 생성 및 내보내기: MakeCert: Azure | Microsoft Docs"
description: "이 문서의 단계 toocreate 자체 서명 된 루트 인증서를 포함 하 고 hello 공개 키를 내보내고 MakeCert를 사용 하 여 클라이언트 인증서를 생성 합니다."
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
ms.openlocfilehash: 0b795ccf74f1f97fbd3de8a0dc339f9cb0b48183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a><span data-ttu-id="ca48d-103">MakeCert를 사용하여 지점 및 사이트 간 연결에 대한 인증서 생성 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="ca48d-103">Generate and export certificates for Point-to-Site connections using MakeCert</span></span>

<span data-ttu-id="ca48d-104">지점 및 사이트 연결 tooauthenticate 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="ca48d-105">이 문서 toocreate는 자체 서명 된 루트 인증서 방법을 보여 줍니다 고 MakeCert를 사용 하 여 클라이언트 인증서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using MakeCert.</span></span> <span data-ttu-id="ca48d-106">찾으려는 경우 지점-사이트 구성 단계에 대 한 방법을 tooupload 루트 인증서를 다음 hello 기사 hello ' 구성 지점 및 사이트 간 ' 중 하나를 선택 목록 등.</span><span class="sxs-lookup"><span data-stu-id="ca48d-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca48d-107">자체 서명된 인증서 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca48d-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="ca48d-108">자체 서명된 인증서 만들기 - MakeCert</span><span class="sxs-lookup"><span data-stu-id="ca48d-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="ca48d-109">지점 및 사이트 간 구성 - Resource Manager - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ca48d-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="ca48d-110">지점 및 사이트 간 구성 - Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca48d-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="ca48d-111">지점 및 사이트 간 구성 - Classic - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ca48d-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

<span data-ttu-id="ca48d-112">Hello를 사용 하는 것이 권장 [Windows 10 PowerShell 단계](vpn-gateway-certificates-point-to-site.md) toocreate 인증서를 제공이 MakeCert 지침은 선택적 검색 방법으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-112">While we recommend using hello [Windows 10 PowerShell steps](vpn-gateway-certificates-point-to-site.md) toocreate your certificates, we provide these MakeCert instructions as an optional method.</span></span> <span data-ttu-id="ca48d-113">두 방법 중 하나를 사용 하 여 생성 하는 hello 인증서에 설치할 수 있습니다 [모든 지원 되는 클라이언트 운영 체제](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-113">hello certificates that you generate using either method can be installed on [any supported client operating system](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq).</span></span> <span data-ttu-id="ca48d-114">그러나 MakeCert 제한을 따르는 hello에:</span><span class="sxs-lookup"><span data-stu-id="ca48d-114">However, MakeCert has hello following limitation:</span></span>

* <span data-ttu-id="ca48d-115">MakeCert는 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-115">MakeCert is deprecated.</span></span> <span data-ttu-id="ca48d-116">즉, 언제든지 이 도구가 제거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-116">This means that this tool could be removed at any point.</span></span> <span data-ttu-id="ca48d-117">MakeCert를 더 이상 사용할 수 없는 경우 MakeCert를 사용하여 이미 생성한 인증서는 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-117">Any certificates that you already generated using MakeCert won't be affected when MakeCert is no longer available.</span></span> <span data-ttu-id="ca48d-118">MakeCert 사용 되는 toogenerate hello 인증서만 아닌 경우 유효성 검사 메커니즘으로</span><span class="sxs-lookup"><span data-stu-id="ca48d-118">MakeCert is only used toogenerate hello certificates, not as a validating mechanism.</span></span>

## <span data-ttu-id="ca48d-119"><a name="rootcert"></a>자체 서명된 루트 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="ca48d-119"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="ca48d-120">단계를 수행 하는 hello toocreate는 자체 서명 된 인증서 MakeCert를 사용 하 여 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-120">hello following steps show you how toocreate a self-signed certificate using MakeCert.</span></span> <span data-ttu-id="ca48d-121">이러한 단계는 배포 모델에 한정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-121">These steps are not deployment-model specific.</span></span> <span data-ttu-id="ca48d-122">리소스 관리자와 클래식에 대해 모두 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-122">They are valid for both Resource Manager and classic.</span></span>

1. <span data-ttu-id="ca48d-123">[MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx)를 다운로드 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-123">Download and install [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).</span></span>
2. <span data-ttu-id="ca48d-124">후 설치를 찾을 수 있습니다 일반적으로이 경로 아래의 hello makecert.exe 유틸리티: ' C:\Program Files (x86) \Windows Kits\10\bin\<arch >'입니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-124">After installation, you can typically find hello makecert.exe utility under this path: 'C:\Program Files (x86)\Windows Kits\10\bin\<arch>'.</span></span> <span data-ttu-id="ca48d-125">하지만 이것은 설치 된 tooanother 위치 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-125">Although, it's possible that it was installed tooanother location.</span></span> <span data-ttu-id="ca48d-126">관리자 권한으로 명령 프롬프트를 열고 hello MakeCert 유틸리티의 toohello 위치를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-126">Open a command prompt as administrator and navigate toohello location of hello MakeCert utility.</span></span> <span data-ttu-id="ca48d-127">다음 예에서는, hello 적절 한 위치에 대 한 조정 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-127">You can use hello following example, adjusting for hello proper location:</span></span>

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. <span data-ttu-id="ca48d-128">만들고 hello 컴퓨터 개인 인증서 저장소에 인증서를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-128">Create and install a certificate in hello Personal certificate store on your computer.</span></span> <span data-ttu-id="ca48d-129">hello 다음 예제에서는 해당 *.cer* P2S 구성할 때 tooAzure를 업로드 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-129">hello following example creates a corresponding *.cer* file that you upload tooAzure when configuring P2S.</span></span> <span data-ttu-id="ca48d-130">'P2SRootCert' 및 'P2SRootCert.cer' hello 인증서에 대 한 toouse 되도록 hello 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-130">Replace 'P2SRootCert' and 'P2SRootCert.cer' with hello name that you want toouse for hello certificate.</span></span> <span data-ttu-id="ca48d-131">hello 인증서는 '인증서-Current User\Personal\Certificates'에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-131">hello certificate is located in your 'Certificates - Current User\Personal\Certificates'.</span></span>

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <span data-ttu-id="ca48d-132"><a name="cer"></a>내보내기 hello 공개 키 (.cer)</span><span class="sxs-lookup"><span data-stu-id="ca48d-132"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="ca48d-133">hello exported.cer 파일 업로드 tooAzure 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-133">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="ca48d-134">자세한 내용은 [지점 및 사이트 간 연결 구성](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca48d-134">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile).</span></span> <span data-ttu-id="ca48d-135">tooadd 신뢰할 수 있는 루트 인증서가 참조 [이 섹션](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) hello 문서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-135">tooadd an additional trusted root certificate, see [this section](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) of hello article.</span></span>

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a><span data-ttu-id="ca48d-136">Hello 자체 서명 된 인증서와 개인 키 toostore 내보낼 것 (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="ca48d-136">Export hello self-signed certificate and private key toostore it (optional)</span></span>

<span data-ttu-id="ca48d-137">Tooexport hello 자체 서명 된 루트 인증서를 안전 하 게 저장을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-137">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="ca48d-138">필요한 경우 나중에 다른 컴퓨터에서 해당 인증서를 설치하고 더 많은 클라이언트 인증서를 생성하거나 다른 .cer 파일을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-138">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="ca48d-139">tooexport hello 루트 인증서를.pfx, 루트 인증서 선택 hello 및 사용 하 여 동일한 단계에 설명 된 대로 hello로 자체 서명 된 [클라이언트 인증서 내보내기](#clientexport)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-139">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <a name="create-and-install-client-certificates"></a><span data-ttu-id="ca48d-140">클라이언트 인증서 만들기 및 설치</span><span class="sxs-lookup"><span data-stu-id="ca48d-140">Create and install client certificates</span></span>

<span data-ttu-id="ca48d-141">Hello 클라이언트 컴퓨터에서 직접 hello 자체 서명 된 인증서를 설치 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ca48d-141">You don't install hello self-signed certificate directly on hello client computer.</span></span> <span data-ttu-id="ca48d-142">Toogenerate hello 자체 서명 된 인증서에서 클라이언트 인증서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-142">You need toogenerate a client certificate from hello self-signed certificate.</span></span> <span data-ttu-id="ca48d-143">그런 다음 내보낸 hello 클라이언트 인증서 toohello 클라이언트 컴퓨터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-143">You then export and install hello client certificate toohello client computer.</span></span> <span data-ttu-id="ca48d-144">배포 모델의 특정 단계를 수행 하는 hello가 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-144">hello following steps are not deployment-model specific.</span></span> <span data-ttu-id="ca48d-145">리소스 관리자와 클래식에 대해 모두 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-145">They are valid for both Resource Manager and classic.</span></span>

### <span data-ttu-id="ca48d-146"><a name="clientcert"></a>클라이언트 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="ca48d-146"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="ca48d-147">Tooa 연결 하는 각 클라이언트 컴퓨터 VNet 지점-사이트를 사용 하 여 클라이언트 인증서가 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-147">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="ca48d-148">Hello 자체 서명 된 루트 인증서에서 클라이언트 인증서를 생성 하 고 내보낸 hello 클라이언트 인증서를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-148">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="ca48d-149">Hello 클라이언트 인증서 설치 되어 있지 않으면 인증이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-149">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="ca48d-150">hello 다음 단계에 관한 자체 서명 된 루트 인증서에서 클라이언트 인증서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-150">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="ca48d-151">Hello에서 여러 클라이언트 인증서를 생성할 수 있습니다 동일한 루트 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-151">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="ca48d-152">다음 hello 단계를 사용 하 여 클라이언트 인증서를 생성할 때 hello 클라이언트 인증서가 자동으로 컴퓨터에 설치 hello toogenerate hello 인증서를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-152">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="ca48d-153">Tooinstall 다른 클라이언트 컴퓨터에서 클라이언트 인증서를 사용 하도록 하려는 경우에 hello 인증서를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-153">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>
 
1. <span data-ttu-id="ca48d-154">Hello에 toocreate hello를 사용 하 여 동일한 컴퓨터 자체 서명 된 인증서, 관리자 권한으로 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-154">On hello same computer that you used toocreate hello self-signed certificate, open a command prompt as administrator.</span></span>
2. <span data-ttu-id="ca48d-155">수정 하 고 hello 샘플 toogenerate 클라이언트 인증서를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-155">Modify and run hello sample toogenerate a client certificate.</span></span>
  * <span data-ttu-id="ca48d-156">변경 *"P2SRootCert"* toohello 이름에서 hello 클라이언트 인증서를 생성 하는 hello 자체 서명 된 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-156">Change *"P2SRootCert"* toohello name of hello self-signed root that you are generating hello client certificate from.</span></span> <span data-ttu-id="ca48d-157">어떤 hello hello 루트 인증서의 hello 이름을 사용 중인지 확인 ' CN =' hello 자체 서명 된 루트를 만들 때 지정 된 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-157">Make sure you are using hello name of hello root certificate, which is whatever hello 'CN=' value was that you specified when you created hello self-signed root.</span></span>
  * <span data-ttu-id="ca48d-158">변경 *P2SChildCert* toogenerate 클라이언트 인증서 toobe 원하는 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-158">Change *P2SChildCert* toohello name you want toogenerate a client certificate toobe.</span></span>

  <span data-ttu-id="ca48d-159">다음 예에서는 수정 하지 않고 hello를 실행 하는 경우 hello 결과 P2SRootCert 루트 인증서에서 생성 된 개인 인증서 저장소에서 P2SChildcert 이라는 클라이언트 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-159">If you run hello following example without modifying it, hello result is a client certificate named P2SChildcert in your Personal certificate store that was generated from root certificate P2SRootCert.</span></span>

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <span data-ttu-id="ca48d-160"><a name="clientexport"></a>클라이언트 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="ca48d-160"><a name="clientexport"></a>Export a client certificate</span></span>

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <span data-ttu-id="ca48d-161"><a name="install"></a>내보낸 클라이언트 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="ca48d-161"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ca48d-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ca48d-162">Next steps</span></span>

<span data-ttu-id="ca48d-163">지점 및 사이트 간 구성을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-163">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="ca48d-164">에 대 한 **리소스 관리자** 배포 모델 단계 참조 [지점 및 사이트 연결 tooa VNet 구성](vpn-gateway-howto-point-to-site-resource-manager-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-164">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span>
* <span data-ttu-id="ca48d-165">에 대 한 **클래식** 배포 모델 단계 참조 [지점-사이트 VPN 연결 tooa VNet (클래식)를 구성](vpn-gateway-howto-point-to-site-classic-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca48d-165">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
