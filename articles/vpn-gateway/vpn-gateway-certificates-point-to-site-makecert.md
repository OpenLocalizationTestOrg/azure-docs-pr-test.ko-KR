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
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a>MakeCert를 사용하여 지점 및 사이트 간 연결에 대한 인증서 생성 및 내보내기

지점 및 사이트 연결 tooauthenticate 인증서를 사용합니다. 이 문서 toocreate는 자체 서명 된 루트 인증서 방법을 보여 줍니다 고 MakeCert를 사용 하 여 클라이언트 인증서를 생성 합니다. 찾으려는 경우 지점-사이트 구성 단계에 대 한 방법을 tooupload 루트 인증서를 다음 hello 기사 hello ' 구성 지점 및 사이트 간 ' 중 하나를 선택 목록 등.

> [!div class="op_single_selector"]
> * [자체 서명된 인증서 만들기 - PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [자체 서명된 인증서 만들기 - MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [지점 및 사이트 간 구성 - Resource Manager - Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [지점 및 사이트 간 구성 - Resource Manager - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [지점 및 사이트 간 구성 - Classic - Azure Portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

Hello를 사용 하는 것이 권장 [Windows 10 PowerShell 단계](vpn-gateway-certificates-point-to-site.md) toocreate 인증서를 제공이 MakeCert 지침은 선택적 검색 방법으로 합니다. 두 방법 중 하나를 사용 하 여 생성 하는 hello 인증서에 설치할 수 있습니다 [모든 지원 되는 클라이언트 운영 체제](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)합니다. 그러나 MakeCert 제한을 따르는 hello에:

* MakeCert는 더 이상 사용되지 않습니다. 즉, 언제든지 이 도구가 제거될 수 있습니다. MakeCert를 더 이상 사용할 수 없는 경우 MakeCert를 사용하여 이미 생성한 인증서는 영향을 받지 않습니다. MakeCert 사용 되는 toogenerate hello 인증서만 아닌 경우 유효성 검사 메커니즘으로

## <a name="rootcert"></a>자체 서명된 루트 인증서 만들기

단계를 수행 하는 hello toocreate는 자체 서명 된 인증서 MakeCert를 사용 하 여 하는 방법을 보여 줍니다. 이러한 단계는 배포 모델에 한정되지 않습니다. 리소스 관리자와 클래식에 대해 모두 유효합니다.

1. [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx)를 다운로드 및 설치합니다.
2. 후 설치를 찾을 수 있습니다 일반적으로이 경로 아래의 hello makecert.exe 유틸리티: ' C:\Program Files (x86) \Windows Kits\10\bin\<arch >'입니다. 하지만 이것은 설치 된 tooanother 위치 같습니다. 관리자 권한으로 명령 프롬프트를 열고 hello MakeCert 유틸리티의 toohello 위치를 이동 합니다. 다음 예에서는, hello 적절 한 위치에 대 한 조정 hello를 사용할 수 있습니다.

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. 만들고 hello 컴퓨터 개인 인증서 저장소에 인증서를 설치 합니다. hello 다음 예제에서는 해당 *.cer* P2S 구성할 때 tooAzure를 업로드 하는 파일입니다. 'P2SRootCert' 및 'P2SRootCert.cer' hello 인증서에 대 한 toouse 되도록 hello 이름을 바꿉니다. hello 인증서는 '인증서-Current User\Personal\Certificates'에 있습니다.

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <a name="cer"></a>내보내기 hello 공개 키 (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

hello exported.cer 파일 업로드 tooAzure 이어야 합니다. 자세한 내용은 [지점 및 사이트 간 연결 구성](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile)을 참조하세요. tooadd 신뢰할 수 있는 루트 인증서가 참조 [이 섹션](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) hello 문서의 합니다.

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a>Hello 자체 서명 된 인증서와 개인 키 toostore 내보낼 것 (선택 사항)

Tooexport hello 자체 서명 된 루트 인증서를 안전 하 게 저장을 할 수 있습니다. 필요한 경우 나중에 다른 컴퓨터에서 해당 인증서를 설치하고 더 많은 클라이언트 인증서를 생성하거나 다른 .cer 파일을 내보낼 수 있습니다. tooexport hello 루트 인증서를.pfx, 루트 인증서 선택 hello 및 사용 하 여 동일한 단계에 설명 된 대로 hello로 자체 서명 된 [클라이언트 인증서 내보내기](#clientexport)합니다.

## <a name="create-and-install-client-certificates"></a>클라이언트 인증서 만들기 및 설치

Hello 클라이언트 컴퓨터에서 직접 hello 자체 서명 된 인증서를 설치 하지 마세요. Toogenerate hello 자체 서명 된 인증서에서 클라이언트 인증서 필요합니다. 그런 다음 내보낸 hello 클라이언트 인증서 toohello 클라이언트 컴퓨터를 설치 합니다. 배포 모델의 특정 단계를 수행 하는 hello가 않습니다. 리소스 관리자와 클래식에 대해 모두 유효합니다.

### <a name="clientcert"></a>클라이언트 인증서 생성

Tooa 연결 하는 각 클라이언트 컴퓨터 VNet 지점-사이트를 사용 하 여 클라이언트 인증서가 설치 되어 있어야 합니다. Hello 자체 서명 된 루트 인증서에서 클라이언트 인증서를 생성 하 고 내보낸 hello 클라이언트 인증서를 설치 합니다. Hello 클라이언트 인증서 설치 되어 있지 않으면 인증이 실패 합니다. 

hello 다음 단계에 관한 자체 서명 된 루트 인증서에서 클라이언트 인증서를 생성 합니다. Hello에서 여러 클라이언트 인증서를 생성할 수 있습니다 동일한 루트 인증서입니다. 다음 hello 단계를 사용 하 여 클라이언트 인증서를 생성할 때 hello 클라이언트 인증서가 자동으로 컴퓨터에 설치 hello toogenerate hello 인증서를 사용 하 여 합니다. Tooinstall 다른 클라이언트 컴퓨터에서 클라이언트 인증서를 사용 하도록 하려는 경우에 hello 인증서를 내보낼 수 있습니다.
 
1. Hello에 toocreate hello를 사용 하 여 동일한 컴퓨터 자체 서명 된 인증서, 관리자 권한으로 명령 프롬프트를 엽니다.
2. 수정 하 고 hello 샘플 toogenerate 클라이언트 인증서를 실행 합니다.
  * 변경 *"P2SRootCert"* toohello 이름에서 hello 클라이언트 인증서를 생성 하는 hello 자체 서명 된 루트입니다. 어떤 hello hello 루트 인증서의 hello 이름을 사용 중인지 확인 ' CN =' hello 자체 서명 된 루트를 만들 때 지정 된 값이 있습니다.
  * 변경 *P2SChildCert* toogenerate 클라이언트 인증서 toobe 원하는 toohello 이름입니다.

  다음 예에서는 수정 하지 않고 hello를 실행 하는 경우 hello 결과 P2SRootCert 루트 인증서에서 생성 된 개인 인증서 저장소에서 P2SChildcert 이라는 클라이언트 인증서입니다.

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <a name="clientexport"></a>클라이언트 인증서 내보내기

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <a name="install"></a>내보낸 클라이언트 인증서 설치

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>다음 단계

지점 및 사이트 간 구성을 계속합니다. 

* 에 대 한 **리소스 관리자** 배포 모델 단계 참조 [지점 및 사이트 연결 tooa VNet 구성](vpn-gateway-howto-point-to-site-resource-manager-portal.md)합니다.
* 에 대 한 **클래식** 배포 모델 단계 참조 [지점-사이트 VPN 연결 tooa VNet (클래식)를 구성](vpn-gateway-howto-point-to-site-classic-azure-portal.md)합니다.
