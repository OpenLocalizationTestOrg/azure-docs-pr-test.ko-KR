---
title: "aaaAdd SSL 인증서 tooyour Azure 앱 서비스 앱 | Microsoft Docs"
description: "어떻게 tooadd SSL 인증서 tooyour 앱 서비스 앱에 알아봅니다."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a>Azure 앱 서비스에 대한 SSL 인증서 구입 및 구성

이 자습서에서는 **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**에 대한 SSL 인증서를 구매하여 [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)에 안전하게 저장하고 사용자 지정 도메인과 연결하여 Web App의 보안을 유지합니다.

## <a name="step-1---log-in-tooazure"></a>1 단계-tooAzure 로그인

Toohello http://portal.azure.com에서 Azure 포털 로그인

## <a name="step-2---place-an-ssl-certificate-order"></a>2단계 - SSL 인증서 주문하기

새 SSL 인증서 주문을 입력 하기 [앱 서비스 인증서](https://portal.azure.com/#create/Microsoft.SSL) hello에 **Azure 포털**합니다.

![인증서 만들기](./media/app-service-web-purchase-ssl-web-site/createssl.png)

친숙 한 입력 **이름** 및 SSL 인증서 및 hello 입력 **도메인 이름**

> [!NOTE]
> Hello hello 구매 프로세스의 가장 중요 한 부분 중 하나입니다. 호스트 이름 (사용자 지정 도메인)이이 인증서와 함께 tooprotect 원하는 해결 되었는지 tooenter를 확인 합니다. **없는** WWW와 hello 호스트 이름을 추가 합니다. 
>

**구독**, **리소스 그룹** 및 **인증서 SKU**를 선택합니다.

> [!WARNING]
> 앱 서비스 인증서 hello 내에서 다른 앱 서비스에서 사용할 수 있습니다만 동일한 구독 합니다.  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a>3 단계-Azure 키 자격 증명 모음에 hello 인증서 저장

> [!NOTE]
> [Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)는 클라우드 응용 프로그램 및 서비스에서 사용되는 암호화 키 및 비밀을 보호하는데 도움이 되는 Azure 서비스입니다.
>

Tooopen 필요한 SSL 인증서 구매 hello 완료 되 면 [앱 서비스 인증서](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) 리소스 블레이드입니다.

![KV에 준비 toostore의 이미지를 삽입 합니다.](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

인증서 상태 임을 알게 될 **"보류 중인 발급"** 몇 가지 단계가 더 많으면 있어야만 toocomplete이이 인증서를 사용 하 여 시작할 수 있습니다.

클릭 **인증서 구성** 내부를 클릭 하 고 인증서 속성 블레이드 **1 단계: 저장소** toostore Azure 키 자격 증명 모음에이 인증서입니다.

**키 자격 증명 모음의 상태** 블레이드에서 클릭 **키 자격 증명 모음 저장소** toochoose는 기존 키 자격 증명 모음 toostore이이 인증서 **또는 새 키 자격 증명 모음 만들기** toocreate 새 키 자격 증명 모음 동일한 구독 및 리소스 그룹의 내부 합니다.

> [!NOTE]
> Azure Key Vault의 경우 이 인증서를 저장하는 데 약간의 요금이 부과됩니다.
> 자세한 내용은 **[Azure Key Vault 가격 책정 정보](https://azure.microsoft.com/pricing/details/key-vault/)**를 참조하세요.
>

키 자격 증명 모음 저장소 toostore hello에이 인증서 선택 하면 hello **저장소** 옵션 성공을 표시 해야 합니다.

![KV의 저장 성공 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a>4 단계-hello 도메인 소유권 확인

> [!NOTE]
> App Service Certificate에서는 도메인 확인 방법으로 도메인 확인, 메일 확인 및 수동 확인을 지원합니다. Hello에 자세히 설명 되어 이러한 [고급 절](#advanced)합니다.

동일한 hello **인증서 구성** 3 단계에서에서 사용 되는 블레이드, 클릭 **2 단계: 확인**합니다.

**도메인 확인** hello 가장 편리 하 게 프로세스 **경우에만** 있는  **[Azure 앱 서비스에서 사용자 지정 도메인을 구입 합니다.](custom-dns-web-site-buydomains-web-app.md)**
클릭 **확인** toocomplete이이 단계를 단추입니다.

![도메인 확인 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

클릭 한 후 **확인**, hello를 사용 하 여 **새로 고침** hello 때까지 단추 **확인** 옵션 성공을 표시 해야 합니다.

![KV의 확인 성공 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a>5 단계-인증서 tooApp 서비스 응용 프로그램 할당

> [!NOTE]
> 이 섹션의 hello 단계를 수행 하기 전에 먼저 연결 해야 사용자 지정 도메인 이름을 앱을 사용 합니다. 자세한 내용은 **[웹앱에 대한 사용자 지정 도메인 이름 구성](app-service-web-tutorial-custom-domain.md)**을 참조하세요.
>

Hello에  **[Azure 포털](https://portal.azure.com/)**, hello 클릭 **앱 서비스** hello 창의 hello 왼쪽의 옵션입니다.

Hello 이름을 클릭 앱 toowhich의 원하는 tooassign이이 인증서입니다.

Hello에 **설정**, 클릭 **SSL 인증서**합니다.

클릭 **앱 서비스 인증서 가져오기** 및 선택 hello 구입한 인증서를 방금 합니다.

![인증서 가져오기 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

Hello에 **ssl 바인딩을** 섹션에서 클릭 **바인딩을 추가할**, 인증서 toouse hello 및 hello 드롭다운 tooselect 도메인 이름 toosecure hello를 사용 하 여 SSL을 사용 합니다. 선택할 수 있습니다 여부 toouse  **[SNI 서버 이름 표시 ()](http://en.wikipedia.org/wiki/Server_Name_Indication)**  IP 기반 SSL 또는 합니다.

![SSL 바인딩 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

클릭 **바인딩 추가** toosave hello 변경 하 고 SSL을 사용 합니다.

> [!NOTE]
> 선택한 경우 **IP 기반 SSL** 및 사용자 지정 도메인이 A 레코드를 사용 하 여 구성 된 추가 단계를 수행 하는 hello를 수행 해야 합니다. Hello에 자세히 설명 되어 이러한 [고급 절](#Advanced)합니다.

이 시점에서 있습니다 있어야 수 toovisit 사용 하 여 앱 `HTTPS://` 대신 `HTTP://` 인증서 hello tooverify가 올바르게 구성 되어 있습니다.

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a>6단계 - 관리 작업

### <a name="azure-cli"></a>Azure CLI

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a>PowerShell

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a>고급

### <a name="verifying-domain-ownership"></a>도메인 소유권 확인

App Service Certificate에서는 도메인 확인 방법으로 메일 확인 및 수동 확인도 지원합니다.

#### <a name="mail-verification"></a>메일 확인

확인 전자 메일에 이미이 사용자 지정 도메인과 관련 된 전자 메일 주소 toohello를 전송 되었습니다.
toocomplete hello 전자 메일 확인 단계 hello 전자 메일을 열고 hello 확인 링크를 클릭 합니다.

![메일 확인 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

Tooresend hello 확인 전자 메일을 해야 하는 경우 클릭 hello **전자 메일 다시 보내기** 단추입니다.

#### <a name="manual-verification"></a>수동 확인

> [!IMPORTANT]
> HTML 웹 페이지 확인(표준 인증서 SKU로만 작동)
>

1. **"starfield.html"**이라는 HTML 파일 만들기

1. 콘텐츠이 파일의 이름 이어야 합니다 hello 정확한 hello 도메인 확인 토큰입니다. (도메인 확인 상태 블레이드 hello에서 hello 토큰 복사할 수)

1. 도메인 호스팅 hello 웹 서버의 hello 루트에이 파일을 업로드`/.well-known/pki-validation/starfield.html`

1. 클릭 **새로 고침** tooupdate hello 인증서 상태 후 확인이 완료 되었습니다. 확인 toocomplete 몇 분 정도 걸릴 수 있습니다.

> [!TIP]
> 사용 하 여 터미널 확인 `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello 응답 hello 있어야 `<verification-token>`합니다.

#### <a name="dns-txt-record-verification"></a>DNS TXT 레코드 확인

1. Hello에 TXT 레코드를 만드는 DNS 관리자를 사용 하 여 `@` 하위 도메인 값 같은 toohello 도메인 확인 토큰을 합니다.
1. 클릭 **"새로 고침"** tooupdate hello 인증서 상태 후 확인이 완료 되었습니다.

> [!TIP]
> TXT 레코드 toocreate가 필요한 `@.<domain>` 값을 가진 `<verification-token>`합니다.

### <a name="assign-certificate-tooapp-service-app"></a>인증서 tooApp 서비스 응용 프로그램 할당

선택한 경우 **IP 기반 SSL** 및 사용자 지정 도메인이 A 레코드를 사용 하 여 구성 된 추가 단계를 수행 하는 hello를 수행 해야 합니다.

구성 하 고 나면 IP 기반 SSL 바인딩에, tooyour 앱 전용된 IP 주소를 할당 합니다. Hello에이 IP 주소를 찾을 수 있습니다 **사용자 지정 도메인** hello 오른쪽 위에서 응용 프로그램의 설정에서 페이지 **Hostnames** 섹션. **외부 IP 주소**로 나열됩니다.

![IP SSL 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

이 IP 주소는 hello 가상 IP 주소 사용 보다 이전에 tooconfigure hello A 레코드가 도메인에 대 한 다른 참고 합니다. 구성 된 경우 toouse SNI 기반 SSL을 이나 없는 toouse SSL을 구성, 주소가 없습니다.이 항목에 대해 나열 됩니다.

도메인 이름 등록 기관에서 제공 하는 hello 도구를 사용 하 여 hello hello 이전 단계에서 사용자 지정 도메인 이름 toopoint toohello IP 주소에 대 한 레코드를 수정 합니다.

## <a name="rekey-and-sync-hello-certificate"></a>키 다시 생성 하 고 hello 인증서를 동기화 합니다.

필요한 경우 tooRekey 인증서를 선택 **키 다시 생성 하 고 동기화** 옵션에서 **인증서 속성** 블레이드입니다.

클릭 **키 다시 생성** tooinitiate hello 프로세스 단추입니다. 1-10 분 toocomplete를 걸릴 수 있습니다.

![SSL 키 다시 생성 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

인증서 재입력 hello 인증서 hello 인증 기관에서 발급 한 새 인증서를 롤업 합니다.

## <a name="next-steps"></a>다음 단계

* [Content Delivery Network 추가](app-service-web-tutorial-content-delivery-network.md)