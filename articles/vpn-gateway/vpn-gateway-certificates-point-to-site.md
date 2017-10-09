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
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>Windows 10에서 PowerShell을 사용하여 지점 및 사이트 간 연결에 대한 인증서 생성 및 내보내기

지점 및 사이트 연결 tooauthenticate 인증서를 사용합니다. 이 문서는 toocreate는 자체 서명 된 루트 인증서 방법을 보여 줍니다 하 고 Windows 10에서 PowerShell을 사용 하 여 클라이언트 인증서를 생성 합니다. 찾으려는 경우 지점-사이트 구성 단계에 대 한 방법을 tooupload 루트 인증서를 다음 hello 기사 hello ' 구성 지점 및 사이트 간 ' 중 하나를 선택 목록 등.

> [!div class="op_single_selector"]
> * [자체 서명된 인증서 만들기 - PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [자체 서명된 인증서 만들기 - MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [지점 및 사이트 간 구성 - Resource Manager - Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [지점 및 사이트 간 구성 - Resource Manager - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [지점 및 사이트 간 구성 - Classic - Azure Portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


Windows 10을 실행 하는 컴퓨터에이 문서의 hello 단계를 수행 해야 합니다. hello PowerShell cmdlet toogenerate 인증서를 사용 하는 hello Windows 10 운영 체제의 일부 이며 다른 버전의 Windows에서 작동 하지 않습니다. hello Windows 10 컴퓨터는 필요한 toogenerate hello 인증서만 합니다. 생성 된 hello 인증서는, 업로드 하거나 모든 지원 되는 클라이언트 운영 체제에 설치할 수 있습니다. 

액세스 tooa Windows 10 컴퓨터가 없는 경우 사용할 수 있습니다 [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate 인증서입니다. hello 두 방법 중 하나를 사용 하 여 생성 하는 수에 인증서를 설치할 모든 [지원](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) 클라이언트 운영 체제입니다.

## <a name="rootcert"></a>자체 서명된 루트 인증서 만들기

Hello New-selfsignedcertificate cmdlet toocreate 자체 서명 된 루트 인증서를 사용 합니다. 추가 매개 변수 정보는 [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)를 참조하세요.

1. Windows 10을 실행하는 컴퓨터에서 상승된 권한으로 Windows PowerShell 콘솔을 엽니다.
2. 다음 예에서는 toocreate hello 자체 서명 된 루트 인증서 hello를 사용 합니다. hello 다음 예제에서는 ' 인증서-현재 User\Personal\Certificates'에 자동으로 설치 되는 ' P2SRootCert' 라는 자체 서명 된 루트 인증서 열어 hello 인증서를 볼 수 있습니다 *certmgr.msc*, 또는 *사용자 인증서 관리*합니다.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>내보내기 hello 공개 키 (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

hello exported.cer 파일 업로드 tooAzure 이어야 합니다. 자세한 내용은 [지점 및 사이트 간 연결 구성](vpn-gateway-howto-point-to-site-rm-ps.md#upload)을 참조하세요. 신뢰할 수 있는 루트 인증서가 tooadd [이 섹션](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) hello 문서의 합니다.

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a>Hello 자체 서명 된 루트 인증서와 공개 키 toostore 내보낼 것 (선택 사항)

Tooexport hello 자체 서명 된 루트 인증서를 안전 하 게 저장을 할 수 있습니다. 필요한 경우 나중에 다른 컴퓨터에서 해당 인증서를 설치하고 더 많은 클라이언트 인증서를 생성하거나 다른 .cer 파일을 내보낼 수 있습니다. tooexport hello 루트 인증서를.pfx, 루트 인증서 선택 hello 및 사용 하 여 동일한 단계에 설명 된 대로 hello로 자체 서명 된 [클라이언트 인증서 내보내기](#clientexport)합니다.

## <a name="clientcert"></a>클라이언트 인증서 생성

Tooa 연결 하는 각 클라이언트 컴퓨터 VNet 지점-사이트를 사용 하 여 클라이언트 인증서가 설치 되어 있어야 합니다. Hello 자체 서명 된 루트 인증서에서 클라이언트 인증서를 생성 하 고 내보낸 hello 클라이언트 인증서를 설치 합니다. Hello 클라이언트 인증서 설치 되어 있지 않으면 인증이 실패 합니다. 

hello 다음 단계에 관한 자체 서명 된 루트 인증서에서 클라이언트 인증서를 생성 합니다. Hello에서 여러 클라이언트 인증서를 생성할 수 있습니다 동일한 루트 인증서입니다. 다음 hello 단계를 사용 하 여 클라이언트 인증서를 생성할 때 hello 클라이언트 인증서가 자동으로 컴퓨터에 설치 hello toogenerate hello 인증서를 사용 하 여 합니다. Tooinstall 다른 클라이언트 컴퓨터에서 클라이언트 인증서를 사용 하도록 하려는 경우에 hello 인증서를 내보낼 수 있습니다.

hello 예제 hello New-selfsignedcertificate cmdlet toogenerate 1 년이 지나면 만료 되는 클라이언트 인증서를 사용 합니다. Hello 클라이언트 인증서에 대 한 다른 만료 값을 설정 하는 등의 추가 매개 변수 정보를 참조 하십시오. [New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)합니다.

### <a name="example-1"></a>예 1

이 예제는 hello 이전 섹션에서 '$cert' 변수를 선언 하는 hello를 사용 합니다. hello 단계를 사용 하 여 hello 자체 서명 된 루트 인증서를 만들거나 추가 클라이언트 인증서에서에서 만드는 새 PowerShell 콘솔 세션 후 hello PowerShell 콘솔을 닫은 경우 [예 2](#ex2)합니다.

수정 하 고 hello 예제 toogenerate 클라이언트 인증서를 실행 합니다. 다음 예에서는 수정 하지 않고 hello를 실행 하는 경우 hello 결과 'P2SChildCert' 이라는 클라이언트 인증서입니다.  다른 값인지 tooname hello 자식 인증서 원한다 면 hello CN 값을 수정 합니다. 이 예제를 실행 하는 경우에 hello TextExtension를 변경 하지 마십시오. 자동으로 생성 하는 hello 클라이언트 인증서는 컴퓨터에 '인증서-Current User\Personal\Certificates'에 설치 됩니다.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>예 2

추가 클라이언트 인증서를 만드는 경우 또는 동일한 hello를 사용 하지는 PowerShell 세션을 사용 하 여 toocreate 자체 서명 된 루트 인증서를 사용 하 여 hello 단계를 수행 합니다.

1. Hello 컴퓨터에 설치 되어 있는 hello 자체 서명 된 루트 인증서를 식별 합니다. 이 cmdlet은 컴퓨터에 설치된 인증서 목록을 반환합니다.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. 즉, 다음 위치에 tooit tooa 텍스트 복사 hello 지문 목록에서 반환 되는 hello로 hello 주체 이름의 찾을 파일입니다. 다음 예제는 hello에 두 개의 인증서. hello CN 이름은 toogenerate 자식 인증서를 제거할 hello 자체 서명 된 루트 인증서의 hello 이름이입니다. 이 경우에는 'P2SRootCert'입니다.

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. Hello 이전 단계의 hello 지문을 사용 하 여 hello 루트 인증서에 대 한 변수를 선언 합니다. 지문을 toogenerate 자식 인증서를 제거할 hello 루트 인증서의 hello 지 문으로 바꿉니다.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  예를 들어 P2SRootCert에 대 한 hello 지문을 사용 하 여 hello 이전 단계에서 hello 변수 다음과 같습니다.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  수정 하 고 hello 예제 toogenerate 클라이언트 인증서를 실행 합니다. 다음 예에서는 수정 하지 않고 hello를 실행 하는 경우 hello 결과 'P2SChildCert' 이라는 클라이언트 인증서입니다. 다른 값인지 tooname hello 자식 인증서 원한다 면 hello CN 값을 수정 합니다. 이 예제를 실행 하는 경우에 hello TextExtension를 변경 하지 마십시오. 자동으로 생성 하는 hello 클라이언트 인증서는 컴퓨터에 '인증서-Current User\Personal\Certificates'에 설치 됩니다.

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>클라이언트 인증서 내보내기   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <a name="install"></a>내보낸 클라이언트 인증서 설치

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>다음 단계

지점 및 사이트 간 구성을 계속합니다. 

* 에 대 한 **리소스 관리자** 배포 모델 단계 참조 [지점 및 사이트 연결 tooa VNet 구성](vpn-gateway-howto-point-to-site-resource-manager-portal.md)합니다. 
* 에 대 한 **클래식** 배포 모델 단계 참조 [지점-사이트 VPN 연결 tooa VNet (클래식)를 구성](vpn-gateway-howto-point-to-site-classic-azure-portal.md)합니다.
