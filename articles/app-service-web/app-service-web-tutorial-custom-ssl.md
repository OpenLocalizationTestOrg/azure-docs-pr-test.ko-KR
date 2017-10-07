---
title: "aaaBind 기존 사용자 지정 SSL 인증서 tooAzure 웹 응용 프로그램 | Microsoft Docs"
description: "사용자 지정 SSL 인증서 tooyour 웹 앱, 모바일 앱 백 엔드, 또는 Azure 앱 서비스에서 API 앱 tootoobind에 알아봅니다."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a>기존 사용자 지정 SSL 인증서 tooAzure 웹 응용 프로그램 바인딩

Azure Web Apps는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다. 이 자습서에서는 어떻게 toobind 사용자 지정 SSL 인증서 너무 신뢰할 수 있는 인증 기관에서 구입한[Azure 웹 앱](app-service-web-overview.md)합니다. 완료 되 면 수 수 tooaccess 웹 앱에서 사용자 지정 DNS 도메인의 hello HTTPS 끝점입니다.

![사용자 지정 SSL 인증서가 포함된 웹앱](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * 앱의 가격 책정 계층 업그레이드
> * 사용자 지정 SSL 인증서 tooApp 서비스 바인딩
> * 앱에 대해 HTTPS 적용
> * 스크립트로 SSL 인증서 바인딩 자동화

> [!NOTE]
> Tooget 사용자 지정 SSL 인증서가 필요한 경우 hello Azure 포털에서에서 직접 얻을 수 있으며 tooyour 웹 응용 프로그램을 바인딩합니다. Hello에 따라 [앱 서비스 인증서 자습서](web-sites-purchase-ssl-web-site.md)합니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서:

- [App Service 앱 만들기](/azure/app-service/)
- [사용자 지정 DNS 이름 tooyour 웹 응용 프로그램 맵](app-service-web-tutorial-custom-domain.md)
- 신뢰할 수 있는 인증 기관에서 SSL 인증서 구매

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a>SSL 인증서에 대한 요구 사항

앱 서비스에서 인증서 toouse hello 인증서 요구 사항을 준수 하는 모든 hello를 충족 해야 합니다.

* 신뢰할 수 있는 인증 기관에서 서명됨
* 암호로 보호된 PFX 파일로 내보냄
* 길이가 2048비트 이상인 개인 키를 포함함
* Hello 인증서 체인에 모든 중간 인증서를 포함합니다.

> [!NOTE]
> **ECC(타원 곡선 암호화) 인증서**는 App Service에서 사용할 수 있지만 이 문서에서는 다루지 않습니다. 인증 기관 hello 정확한 단계 toocreate ECC 인증서에 사용 합니다.

## <a name="prepare-your-web-app"></a>웹앱 준비

toobind 사용자 지정 SSL 인증서 tooyour 웹 응용 프로그램 프로그램 [앱 서비스 계획](https://azure.microsoft.com/pricing/details/app-service/) hello에 있어야 **기본**, **표준**, 또는 **프리미엄** 계층입니다. 이 단계에서는 있습니다 지원 되는지 확인을 웹 앱 hello에 가격 책정 계층입니다.

### <a name="log-in-tooazure"></a>TooAzure 로그인

열기 hello [Azure 포털](https://portal.azure.com)합니다.

### <a name="navigate-tooyour-web-app"></a>Tooyour 웹 응용 프로그램 이동

Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, 웹 응용 프로그램의 hello 이름을 클릭 하 고 있습니다.

![웹앱 선택](./media/app-service-web-tutorial-custom-ssl/select-app.png)

웹 응용 프로그램의 hello 관리 페이지에 연결 되었습니다.  

### <a name="check-hello-pricing-tier"></a>가격 책정 계층 hello를 확인 합니다.

웹 응용 프로그램 페이지의 왼쪽 탐색 hello 스크롤하여 toohello **설정** 선택한 섹션 **(앱 서비스 계획) 수직**합니다.

![강화 메뉴](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

Toomake 있는지 웹 앱 hello에 있지 않은지 확인 **무료** 또는 **Shared** 계층입니다. 웹앱의 현재 계층이 진한 파란색 상자로 강조 표시됩니다.

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

사용자 지정 SSL hello에서 지원 되지 않습니다 **무료** 또는 **Shared** 계층입니다. tooscale 해야 할 경우 hello 다음 섹션의 hello 단계를 수행 합니다. Hello를 닫습니다 **가격 책정 계층 선택** 페이지 및 너무 건너뛸[업로드 하 고 SSL 인증서에 바인딩할](#upload)합니다.

### <a name="scale-up-your-app-service-plan"></a>App Service 계획 강화

Hello 중 하나를 선택 **기본**, **표준**, 또는 **프리미엄** 계층입니다.

**선택**을 클릭합니다.

![가격 책정 계층 선택](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

Hello 알림을 다음 표시 되 면 hello 크기 조정 작업이 완료 되었습니다.

![강화 알림](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a>SSL 인증서 바인딩

사용자는 준비 tooupload SSL 인증서 tooyour 웹 앱입니다.

### <a name="merge-intermediate-certificates"></a>중간 인증서 병합

인증 기관에 인증서가 여러 개 hello 인증서 체인을 제공 하는 경우 순서 대로 toomerge hello 인증서가 필요 합니다. 

toodo 각 열기가 인증서를 텍스트 편집기에서 받은 합니다. 

라는 hello 병합 된 인증서에 대 한 파일을 만들 _mergedcertificate.crt_합니다. 텍스트 편집기에서이 파일에 각 인증서의 hello 콘텐츠를 복사 합니다. 인증서의 hello 순서는 서식 파일을 다음 hello 같이 표시 됩니다.

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a>인증서 tooPFX 내보내기

병합 된 SSL 인증서를 사용 하 여 인증서 요청 생성 hello 개인 키로 내보냅니다.

OpenSSL을 사용하여 인증서 요청을 생성한 경우 개인 키 파일을 만든 것입니다. tooexport hello 다음 명령을 실행 하 여 인증서 tooPFX 합니다. Hello 자리 표시자를 대체  _&lt;개인 키 파일 >_ 및  _&lt;병합-인증서-파일 >_합니다.

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

메시지가 표시되면 내보내기 암호를 정의합니다. 프로그램 SSL 인증서 tooApp 서비스 나중에 업로드할 때이 암호를 사용 합니다.

IIS를 사용 하는 경우 또는 _Certreq.exe_ toogenerate 인증서 요청, 설치 hello 인증서 tooyour 로컬 컴퓨터 즉, 한 다음 [hello 인증서 tooPFX 내보내기](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx)합니다.

### <a name="upload-your-ssl-certificate"></a>SSL 인증서 업로드

tooupload SSL 인증서를 클릭 하 여 **SSL 인증서** hello 왼쪽 탐색의 웹 앱에에서 있습니다.

**인증서 업로드**를 클릭합니다.

**PFX 인증서 파일**에서 PFX 파일을 선택합니다. **인증서 암호**, hello PFX 파일을 내보낼 때 만든 hello 암호를 입력 합니다.

**업로드**를 클릭합니다.

![인증서 업로드](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

Hello에 표시 하는 앱 서비스 인증서를 업로드 완료 되 면 **SSL 인증서** 페이지.

![업로드된 인증서](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a>SSL 인증서 바인딩

Hello에 **SSL 바인딩을** 섹션에서 클릭 **바인딩을 추가**합니다.

Hello에 **SSL 바인딩 추가** 페이지 hello 드롭다운 tooselect hello 도메인 이름 toosecure 및 인증서 toouse hello 사용 합니다.

> [!NOTE]
> 인증서를 업로드 한 해도 hello에 hello 도메인 이름에 표시 되지 않는 경우 **Hostname** 드롭다운에서 hello 브라우저 페이지를 새로 고 치세요.
>
>

**SSL 유형**을 선택 하는지 여부를 toouse  **[SNI 서버 이름 표시 ()](http://en.wikipedia.org/wiki/Server_Name_Indication)**  또는 IP 기반 SSL 합니다.

- **SNI 기반 SSL** - 여러 개의 SNI 기반 SSL 바인딩을 추가할 수 있습니다. 이 옵션을 사용 하면 여러 SSL 인증서 toosecure hello에 여러 도메인이 동일한 IP 주소입니다. 대부분의 최신 브라우저(Internet Explorer, Chrome, Firefox 및 Opera 포함)는 SNI를 지원합니다. [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)(서버 이름 표시)에서 더 포괄적인 브라우저 지원 정보를 찾을 수 있습니다.
- **IP 기반 SSL** - IP 기반 SSL 바인딩 하나만 추가할 수 있습니다. 이 옵션을 사용 하면 하나의 SSL 인증서 toosecure 전용된 공용 IP 주소입니다. toosecure 여러 도메인에 보안을 설정 해야을 사용 하 여 모든 hello 같은 SSL 인증서입니다. SSL 바인딩에 대 한 hello 기존의 옵션입니다.

**바인딩 추가**를 클릭합니다.

![SSL 인증서 바인딩](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

Hello에 표시 하는 앱 서비스 인증서를 업로드 완료 되 면 **SSL 바인딩을** 섹션.

![바인딩된 tooweb 응용 프로그램 인증서](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a>IP SSL에 대한 A 레코드 다시 매핑

웹 앱에서 IP 기반 SSL를 사용 하지 않는 경우 너무 건너뜁니다[사용자 지정 도메인에 대 한 테스트 HTTPS](#test)합니다.

기본적으로 웹앱에서는 공유 공용 IP 주소를 사용합니다. IP 기반 SSL을 사용하여 인증서를 바인딩하면 App Service에서 웹앱에 대한 새로운 전용 IP 주소를 만듭니다.

A 레코드 tooyour 웹 응용 프로그램을 매핑한 경우이 새, 전용 IP 주소로 도메인 레지스트리를 업데이트 합니다.

웹 앱의 **사용자 지정 도메인** 페이지 hello 새 전용된 IP 주소를 업데이트 합니다. [이 IP 주소를 복사](app-service-web-tutorial-custom-domain.md#info), 다음 [다시 매핑 hello 레코드](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis 새 IP 주소입니다.

<a name="test"></a>

## <a name="test-https"></a>HTTPS 테스트

이제 toodo 없어진을 사용자 지정 도메인에 대 한 HTTPS 작동 하는지 toomake 됩니다. 다양 한 브라우저에서 찾은 너무`https://<your.custom.domain>` toosee 웹 앱을 처리 하 합니다.

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> 웹앱에서 인증서 유효성 검사 오류가 발생한 경우 자체 서명된 인증서를 사용하고 있을 수도 있습니다.
>
> 않은 hello 경우, 있습니다 수 생략 되었으므로 중간 인증서 toohello PFX 인증서 파일을 내보낼 때.

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a>HTTPS 적용

App Service에서는 HTTPS를 적용하지 *않으므로* 방문자는 HTTP를 사용하여 웹앱에 계속 액세스할 수 있습니다. hello에 다시 쓰기 규칙을 정의 하는 웹 앱에 대 한 HTTPS tooenforce _web.config_ 웹 앱에 대 한 파일입니다. 앱 서비스 웹 앱의 hello 언어 프레임 워크에 관계 없이이 파일을 사용합니다.

> [!NOTE]
> 언어별 요청 리디렉션이 있습니다. ASP.NET MVC hello צ ְ ײ [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) hello 다시 쓰기 규칙에서 대신 필터 _web.config_합니다.

.NET 개발자는 이 파일에 친숙해야 합니다. 솔루션의 hello 루트입니다.

또는 PHP, Node.js, Python 또는 Java로 개발할 경우 사용자 대신 App Service에서 이 파일을 생성했을 수 있습니다.

Hello 지침에 따라 tooyour 웹 앱의 FTP 끝점 연결 [프로그램 응용 프로그램 tooAzure FTP/S를 사용 하 여 응용 프로그램 서비스를 배포할](app-service-deploy-ftp.md)합니다.

이 파일은 _/home/site/wwwroot_에 있어야 합니다. 그렇지 않은 경우 만들기는 _web.config_ hello 다음과 같은 XML이이 폴더에서:

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

기존 _web.config_ 파일, hello 전체 복사 `<rule>` 요소에 프로그램 _web.config_의 `configuration/system.webServer/rewrite/rules` 요소입니다. 다른 경우 `<rule>` 요소에 프로그램 _web.config_, 복사 위치 hello `<rule>` hello 다른 하기 전에 요소 `<rule>` 요소입니다.

이 규칙 hello 사용자가 HTTP 요청 tooyour 웹 앱 때마다 301 (영구적 이동) toohello HTTPS 프로토콜을 반환 합니다. 예를 들어에서 리디렉션합니다 `http://contoso.com` 너무`https://contoso.com`합니다.

IIS URL 재작성 모듈 hello에 대 한 자세한 내용은 참조 hello [URL 재작성](http://www.iis.net/downloads/microsoft/url-rewrite) 설명서입니다.

## <a name="enforce-https-for-web-apps-on-linux"></a>Linux의 Web Apps에 HTTPS 적용

Linux의 App Service에서는 HTTPS를 적용하지 *않으므로* 누구든지 여전히 HTTP를 사용하여 웹앱에 액세스할 수 있습니다. hello에 다시 쓰기 규칙을 정의 하는 웹 앱에 대 한 HTTPS tooenforce _.htaccess_ 웹 앱에 대 한 파일입니다. 

Hello 지침에 따라 tooyour 웹 앱의 FTP 끝점 연결 [프로그램 응용 프로그램 tooAzure FTP/S를 사용 하 여 응용 프로그램 서비스를 배포할](app-service-deploy-ftp.md)합니다.

_/home/site/wwwroot_을 만듭니다는 _.htaccess_ 코드 다음 hello로 파일:

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

이 규칙 hello 사용자가 HTTP 요청 tooyour 웹 앱 때마다 301 (영구적 이동) toohello HTTPS 프로토콜을 반환 합니다. 예를 들어에서 리디렉션합니다 `http://contoso.com` 너무`https://contoso.com`합니다.

## <a name="automate-with-scripts"></a>스크립트를 사용하여 자동화

Hello를 사용 하 여 스크립트를 사용 하 여 웹 앱에 대 한 SSL 바인딩의 자동화할 수 있습니다 [Azure CLI](/cli/azure/install-azure-cli) 또는 [Azure PowerShell](/powershell/azure/overview)합니다.

### <a name="azure-cli"></a>Azure CLI

다음 명령을 hello는 내보낸된 PFX 파일을 업로드 하 고 hello 지문을 가져옵니다.

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

hello 다음 명령을 한 SNI 기반 SSL 바인딩을 추가, hello 이전 명령에서 hello 지문을 사용 하 여 합니다.

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a>Azure PowerShell

hello 다음 명령은 내보낸된 PFX 파일을 업로드 하 고 SNI 기반 SSL 바인딩을 추가 합니다.

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a>다음 단계

이 자습서에서 학습한 방법은 다음과 같습니다.

> [!div class="checklist"]
> * 앱의 가격 책정 계층 업그레이드
> * 사용자 지정 SSL 인증서 tooApp 서비스 바인딩
> * 앱에 대해 HTTPS 적용
> * 스크립트로 SSL 인증서 바인딩 자동화

다음 자습서 toolearn toohello 어떻게 발전 toouse Azure 콘텐츠 배달 네트워크입니다.

> [!div class="nextstepaction"]
> [추가 네트워크 CDN (콘텐츠 배달) tooan Azure 앱 서비스](app-service-web-tutorial-content-delivery-network.md)
