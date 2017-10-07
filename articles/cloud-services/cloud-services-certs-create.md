---
title: "서비스 및 관리 인증서를 aaaCloud | Microsoft Docs"
description: "Microsoft Azure를 사용한 인증서 toocreate 및 사용에 알아봅니다"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 69cb5467ece58a91dae06b4120954aeb2826bde1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a>Azure 클라우드 서비스 인증서 개요
인증서는 Azure에서 클라우드 서비스에 사용 됩니다 ([서비스 인증서](#what-are-service-certificates)) 및 hello 관리 API에 인증 하기 위해 ([관리 인증서](#what-are-management-certificates) 때 Azure 클래식 포털을 사용 하 여 hello 및 not hello 비 클래식 Azure 포털)입니다. 이 항목에서는 두 인증서 종류에 대 한 일반적인 개요를 어떻게 너무 제공[만들](#create) 및 [배포](#deploy) 해당 tooAzure 합니다.

Azure에서 사용되는 인증서는 x.509 v3 인증서이며 다른 신뢰할 수 있는 인증서에 의해 서명되거나 자체 서명될 수 있습니다. 자체 서명된 인증서는 해당 작성자에 의해 서명되므로 기본적으로 신뢰할 수 없습니다. 대부분의 브라우저는 이러한 문제를 무시할 수 있습니다. Cloud Services를 개발하고 테스트하는 경우에만 자체 서명된 인증서를 사용해야 합니다. 

Azure에서 사용하는 인증서에는 개인 또는 공개 키가 포함될 수 있습니다. 수단 tooidentify 제공 하는 지문이 인증서를 사용할 명확한 방식으로 합니다. Hello Azure에서에서이 지문을 사용 하는 [구성 파일](cloud-services-configure-ssl-certificate.md) tooidentify 클라우드 서비스 인증서를 사용 해야 합니다. 

## <a name="what-are-service-certificates"></a>서비스 인증서란 무엇인가요?
서비스 인증서는 연결 된 toocloud 서비스와 보안 통신 tooand hello 서비스에서 사용 하도록 설정 합니다. 예를 들어 웹 역할을 배포한 경우 원할 toosupply 노출 된 HTTPS 끝점을 인증할 수 있는 인증서. 서비스 인증서를 서비스 정의에 정의 된 toohello 자동으로 배포 된 가상 컴퓨터 역할의 인스턴스를 실행 하는 합니다. 

서비스 인증서 tooAzure 클래식을 업로드할 수 포털 중 하나를 사용 하 여 Azure 클래식 포털 또는 hello 클래식 배포 모델을 사용 하 여 hello 합니다. 서비스 인증서는 특정 클라우드 서비스와 연관됩니다. Tooa 배포 hello 서비스 정의 파일에 할당 됩니다.

서비스 인증서는 서비스와 별도로 관리할 수 있으며 다른 개인이 관리할 수도 있습니다. 예를 들어 개발자 tooa 인증서는 IT 관리자가 tooAzure 업로드 이전에 참조 하는 서비스 패키지를 업로드할 수 있습니다. IT 관리자가 관리 하 고 새 서비스 패키지 tooupload 필요 없이 (hello 서비스의 hello 구성 변경) 해당 인증서를 갱신 수 있습니다. 새 서비스 패키지 않고 업데이트 hello 서비스 정의 파일에는 hello 논리적 이름, 저장소 이름 및 hello 인증서의 위치와 hello 인증서 지문 안녕하세요 서비스 구성 파일에 지정 된 하는 동안 불가능 합니다. tooupdate hello 인증서 것만 필요한 tooupload hello 서비스 구성 파일에서 값을 새 인증서와 hello 지문을 변경 합니다.

>[!Note]
>hello [클라우드 서비스 FAQ](cloud-services-faq.md) 기술 자료 문서에 인증서에 대 한 몇 가지 유용한 정보입니다.

## <a name="what-are-management-certificates"></a>관리 인증서란 무엇인가요?
관리 인증서를 사용 하면 tooauthenticate hello 클래식 배포 모델에 있습니다. 많은 프로그램 및 도구 (예: Visual Studio 또는 Azure SDK hello) 이러한 인증서 tooautomate 구성 및 다양 한 Azure 서비스의 배포를 사용 합니다. 이들은 실제로 관련된 toocloud 서비스입니다. 

> [!WARNING]
> 주의가 필요합니다! 모든 사용자가 사용 하 여 인증을 허용 하는 이러한 종류의 인증서는 연결 된 toomanage hello 구독 합니다. 
> 
> 

### <a name="limitations"></a>제한 사항
관리 인증서는 구독당 100개로 제한됩니다. 특정 서비스 관리자의 사용자 ID에서 모든 구독에 대한 관리 인증서가 100개로 제한되기도 합니다. Hello 계정 관리자에 대 한 hello 사용자 ID가 100 tooadd를 사용 하는 관리 인증서가 이미가 더 많은 인증서에 대 한 필요한 경우 공동 관리자 tooadd hello 추가 인증서를 추가할 수 있습니다. 

100개가 넘는 인증서를 추가하기 전에 기존 인증서를 다시 사용할 수 있는지 확인해보세요. 공동 관리자를 사용 하 여 잠재적으로 불필요 한 복잡성 tooyour 인증서 관리 프로세스를 추가 합니다.

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a>자체 서명된 새로운 인증서 만들기
Toothese 설정을 준수으로 모든 도구가 사용 가능한 toocreate 자체 서명 된 인증서를 사용할 수 있습니다.

* X.509 인증서여야 합니다.
* 개인 키가 포함되어 있어야 합니다.
* 키 교환용으로 만들어졌어야 합니다(.pfx 파일).
* 주체 이름에는 hello 사용 되는 도메인 tooaccess hello 클라우드 서비스를 일치 해야 합니다.

    > Hello cloudapp.net에 대 한 SSL 인증서를 가져올 수 없습니다 (또는 Azure와 관련 된) 도메인입니다. hello 인증서의 주체 이름은 hello 사용자 지정 도메인 이름 사용 tooaccess 응용 프로그램 일치 해야 합니다. 예를 들어, **contoso.cloudapp.net**이 아니라**contoso.net**입니다.

* 최소한 2048비트 암호화를 사용해야 합니다.
* **서비스 인증서만**: hello에 클라이언트 쪽 인증서 있어야 *개인* 인증서 저장소입니다.

두 개의 간단한 방법으로 toocreate 인증서에 없는 Windows hello로 `makecert.exe` 유틸리티 또는 IIS 합니다.

### <a name="makecertexe"></a>Makecert.exe
이 유틸리티는 사용되지 않으므로 여기에 더 이상 설명되지 않습니다. 자세한 내용은 [이 MSDN 문서](https://msdn.microsoft.com/library/windows/desktop/aa386968)를 참조하세요.

### <a name="powershell"></a>PowerShell
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> 도메인 대신 IP 주소와 toouse hello 인증서 hello-DnsName 매개 변수에서 hello IP 주소를 사용 합니다.


이 toouse 하려면 [hello 관리 포털에 인증서](../azure-api-management-certs.md), tooa 내보내기 **.cer** 파일:

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a>IIS(인터넷 정보 서비스)
여러 페이지에 있는 hello 포괄 하는 인터넷 어떻게 toodo이 IIS와 합니다. [여기](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) 에서 볼 수 있습니다. 

### <a name="java"></a>Java
Java도 사용할 수 있습니다[인증서를 만들](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate)합니다.

### <a name="linux"></a>Linux
[이](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) SSH와 함께 toocreate 인증서 하는 방법에 대해 설명 합니다.

## <a name="next-steps"></a>다음 단계
[서비스 인증서 toohello Azure 클래식 포털을 업로드](cloud-services-configure-ssl-certificate.md) (또는 hello [Azure 포털](cloud-services-configure-ssl-certificate-portal.md)).

업로드 한 [관리 API 인증서](../azure-api-management-certs.md) toohello Azure 클래식 포털입니다. Azure 포털 hello 인증에 대 한 관리 인증서를 사용 하지 않습니다.

