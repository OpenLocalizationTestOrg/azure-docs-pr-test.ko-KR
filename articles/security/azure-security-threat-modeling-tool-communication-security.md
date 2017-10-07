---
title: "보안-Microsoft 위협 모델링 도구-Azure aaaCommunication | Microsoft Docs"
description: "hello 위협 모델링 도구에에서 노출 위협에 대 한 완화"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 667829c75123f4dbe0b383fdaf8cd899802f9b16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-communication-security--mitigations"></a>보안 프레임: 통신 보안 | 완화 
| 제품/서비스 | 문서 |
| --------------- | ------- |
| **Azure 이벤트 허브** | <ul><li>[보안 통신 tooEvent SSL/TLS를 사용 하 여 허브](#comm-ssltls)</li></ul> |
| **Dynamics CRM** | <ul><li>[서비스 계정 권한 및 사용자 지정 서비스 또는 ASP.NET 페이지 hello 검사 CRM의 보안 준수를 확인 합니다.](#priv-aspnet)</li></ul> |
| **Azure 데이터 팩터리** | <ul><li>[Data Factory에 연결-프레미스 SQL Server에 tooAzure 하는 동안 데이터 관리 게이트웨이 사용 하 여](#sqlserver-factory)</li></ul> |
| **Identity Server** | <ul><li>[모든 트래픽 tooIdentity 서버 인지 확인 HTTPS 연결을 통해](#identity-https)</li></ul> |
| **웹 응용 프로그램** | <ul><li>[X.509 인증서 사용 tooauthenticate, TLS, SSL 및 DTLS 연결 확인](#x509-ssltls)</li><li>[Azure App Service에서 사용자 지정 도메인에 대한 SSL 인증서 구성](#ssl-appservice)</li><li>[HTTPS 연결을 통해 모든 트래픽을 tooAzure 앱 서비스를 강제 적용](#appservice-https)</li><li>[HSTS(HTTP 엄격한 전송 보안)를 사용하도록 설정](#http-hsts)</li></ul> |
| **데이터베이스** | <ul><li>[SQL 서버 연결 암호화 및 인증서 유효성 검사 확인](#sqlserver-validation)</li><li>[암호화 된 통신 tooSQL 서버 적용](#encrypted-sqlserver)</li></ul> |
| **Azure 저장소** | <ul><li>[HTTPS를 통해 저장소는 해당 통신 tooAzure 확인](#comm-storage)</li><li>[HTTPS를 사용할 수 없는 경우 Blob을 다운로드한 후 MD5 해시 유효성 검사](#md5-https)</li><li>[사용 하 여 SMB 3.0 호환 되는 클라이언트 tooensure 전송 중인 데이터 암호화 tooAzure 파일 공유](#smb-shares)</li></ul> |
| **모바일 클라이언트** | <ul><li>[인증서 고정 구현](#cert-pinning)</li></ul> |
| **WCF** | <ul><li>[HTTPS 사용 설정 - 보안 전송 채널](#https-transport)</li><li>[WCF: 집합 메시지 보안 보호 수준 tooEncryptAndSign](#message-protection)</li><li>[WCF: 최소 권한 계정을 toorun를 WCF 서비스 사용](#least-account-wcf)</li></ul> |
| **앱 API** | <ul><li>[HTTPS 연결을 통해 모든 트래픽을 tooWeb Api 강제](#webapi-https)</li></ul> |
| **Azure Redis 캐시(영문)** | <ul><li>[Redis 캐시는 SSL을 통해 해당 통신 tooAzure 확인](#redis-ssl)</li></ul> |
| **IoT 필드 게이트웨이** | <ul><li>[보안 장치 tooField 게이트웨이 통신](#device-field)</li></ul> |
| **IoT 클라우드 게이트웨이** | <ul><li>[장치 tooCloud SSL/TLS를 사용 하 여 게이트웨이 통신 보안](#device-cloud)</li></ul> |

## <a id="comm-ssltls"></a>보안 통신 tooEvent SSL/TLS를 사용 하 여 허브

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure Event Hub | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Event Hubs 인증 및 보안 모델 개요](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **단계** | AMQP 또는 HTTP 연결 tooEvent SSL/TLS를 사용 하 여 허브 보안 |

## <a id="priv-aspnet"></a>서비스 계정 권한 및 사용자 지정 서비스 또는 ASP.NET 페이지 hello 검사 CRM의 보안 준수를 확인 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Dynamics CRM | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 서비스 계정 권한 및 사용자 지정 서비스 또는 ASP.NET 페이지 hello 검사 CRM의 보안 준수를 확인 합니다. |

## <a id="sqlserver-factory"></a>Data Factory에 연결-프레미스 SQL Server에 tooAzure 하는 동안 데이터 관리 게이트웨이 사용 하 여

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 데이터 팩터리 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 연결된 서비스 유형 - Azure 및 온-프레미스 |
| **참조**              |[온-프레미스 및 Azure Data Factory 간 데이터 이동](https://azure.microsoft.com/documentation/articles/data-factory-move-data-between-onprem-and-cloud/#create-gateway), [데이터 관리 게이트웨이](https://azure.microsoft.com/documentation/articles/data-factory-data-management-gateway/) |
| **단계** | <p>hello 데이터 관리 게이트웨이 (DMG) 도구는 회사 네트워크 또는 방화벽 뒤에 있는 보호 되는 필수 tooconnect toodata 소스입니다.</p><ol><li>Hello 컴퓨터를 잠그는 hello DMG 도구를 격리 하 고 손상 또는 스누핑 hello 데이터 원본 컴퓨터에서 작동 하지 않는 프로그램을 방지 합니다. (예: 최신 업데이트를 설치해야 하고, 필요한 최소 포트를 사용하고, 계정 프로비저닝을 제어하고, 감사를 사용하고, 디스크 암호화를 사용해야 합니다.)</li><li>잦은 간격 또는 hello DMG 서비스 계정 암호 갱신 때마다 데이터 게이트웨이 키를 회전 해야</li><li>연결 서비스를 통한 데이터 전송은 암호화되어야 합니다.</li></ol> |

## <a id="identity-https"></a>모든 트래픽 tooIdentity 서버 인지 확인 HTTPS 연결을 통해

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | ID 서버 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [IdentityServer3 - 키, 서명 및 암호화](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html)(영문), [IdentityServer3 - 배포](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html)(영문) |
| **단계** | IdentityServer는 기본적으로 HTTPS를 통한 들어오는 모든 연결 toocome가 필요 합니다. IdentityServer와의 통신은 반드시 보안 전송을 통해서만 수행되어야 합니다. 이 요구 사항을 완화할 수 있는 SSL 오프로딩과 같은 특정 배포 시나리오가 있습니다. 자세한 정보에 대 한 hello 참조의 hello Id 서버 배포 페이지를 참조 하십시오. |

## <a id="x509-ssltls"></a>X.509 인증서 사용 tooauthenticate, TLS, SSL 및 DTLS 연결 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>SSL, TLS, 또는 DTLS를 사용 하는 응용 프로그램에 연결 하는 hello 엔터티의 hello X.509 인증서 확인 완벽 하 게 해야 합니다. 에 대 한 hello 인증서 확인은 다음과 같습니다.</p><ul><li>도메인 이름</li><li>유효 날짜(시작 날짜와 만료 날짜 모두)</li><li>해지 상태</li><li>사용 현황(예: 서버에 대한 서버 인증, 클라이언트에 대한 클라이언트 인증)</li><li>신뢰 체인 - 인증서 연결 tooa 루트 CA (인증 기관)는 hello 플랫폼에 의해 신뢰 되지 않거나 hello 관리자가 명시적으로 구성 되어 있어야 합니다.</li><li>인증서 공개 키의 길이는 2,048비트보다 커야 합니다.</li><li>해싱 알고리즘은 SHA256 이상이어야 합니다. |

## <a id="ssl-appservice"></a>Azure App Service에서 사용자 지정 도메인에 대한 SSL 인증서 구성

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | EnvironmentType - Azure |
| **참조**              | [Azure App Service에서 앱에 대한 HTTPS를 사용하도록 설정](https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/) |
| **단계** | 기본적으로 Azure 이미에서는 HTTPS hello에 대 한 와일드 카드 인증서와 함께 모든 응용 프로그램에 대 한 *. azurewebsites.net 도메인입니다. 그러나 모든 와일드카드 도메인과 마찬가지로 자체 인증서로 사용자 지정 도메인을 사용하는 것만큼 안전하지 않습니다([참조](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates/)). 배포 된 hello 앱을 통해 액세스 되는 hello 사용자 지정 도메인에 대 한 SSL tooenable 것이 좋습니다.|

## <a id="appservice-https"></a>HTTPS 연결을 통해 모든 트래픽을 tooAzure 앱 서비스를 강제 적용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | EnvironmentType - Azure |
| **참조**              | [Azure App Service에 HTTPS 적용]https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/#4-enforce-https-on-your-app) |
| **단계** | <p>Azure hello 도메인에 대 한 와일드 카드 인증서로 Azure 앱 서비스에 대 한 HTTPS를 통해 이미 있지만 *.으로.azurewebsites.net, HTTPS를 적용 하지 않습니다. 방문자 hello 응용 프로그램의 보안을 손상 시킬 수는 HTTP를 사용 하 여 hello 앱에 액세스할 수 있으며 따라서 HTTPS toobe 명시적으로 적용 합니다. ASP.NET MVC 응용 프로그램 hello를 사용 해야 [RequireHttps 필터](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) HTTPS를 통해 다시 전송 하는 보안 되지 않은 HTTP 요청 toobe 강제로입니다.</p><p>또는 hello URL 재작성 모듈을 Azure 앱 서비스에 포함 되어 있는 사용된 tooenforce HTTPS 될 수 있습니다. URL 재작성 모듈에는 개발자가 toodefine 규칙을 hello 요청은 tooyour 응용 프로그램을 전달 하기 전에 적용 된 tooincoming 요청을 수 있습니다. URL 다시 쓰기 규칙이 hello hello 응용 프로그램의 루트에 저장 된 web.config 파일에 정의 되어</p>|

### <a name="example"></a>예제
hello 다음 예제에서는 포함 된 들어오는 모든 트래픽을 toouse HTTPS를 강제로 수행 하는 기본 URL 재작성 규칙
```XML
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```
이 규칙은 301 (영구적 이동), HTTP 상태 코드를 반환 하 여 작동 hello 사용자가 HTTP를 사용 하 여 페이지를 요청 하는 경우. hello 301 리디렉션을 hello 요청 toohello hello 방문자와 동일한 URL 요청 하지만 HTTPS 사용 하 여 hello 요청 부분의 hello HTTP 바꿉니다. 예를 들어 HTTP://contoso.com 리디렉션된 tooHTTPS://contoso.com 것입니다. 

## <a id="http-hsts"></a>HSTS(HTTP 엄격한 전송 보안)를 사용하도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [OWASP HSTS(HTTP 엄격한 전송 보안) 참고 자료](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet)(영문) |
| **단계** | <p>HTTP 엄격한 전송 보안 (HSTS)는 특별 한 응답 헤더의 hello 사용을 통해 웹 응용 프로그램에 의해 지정 된 옵트인 보안 향상 합니다. 지원 되는 브라우저는이 헤더를 수신 되 면 해당 브라우저에서 HTTP toohello 지정 된 도메인을 통해 전송 되는 통신 하며 수 HTTPS를 통해 모든 통신 송신할 대신 없습니다. 또한 브라우저에서 프롬프트를 통해 HTTPS를 클릭하지 않도록 방지합니다.</p><p>HSTS tooimplement hello 응답 헤더 뒤에 오는 웹 사이트에 대 한 전역적으로 구성 되며, 코드 또는 구성에서 toobe에 있습니다. 보안: Strict-전송-최대 처리 기간 = 300; includeSubDomains HSTS hello 위협 다음 해결할 수 있습니다.</p><ul><li>사용자 책갈피를 설정 하거나 수동으로 http://example.com 형식과 주체 tooa 중간자 개입 공격자가: HSTS hello 대상 도메인에 대 한 HTTP 요청 tooHTTPS를 자동으로 리디렉션하여</li><li>웹 응용 프로그램은 순수 하 게 HTTPS 실수로 HTTP 링크를 포함 또는 HTTP를 통해 콘텐츠를 사용 하는 의도 된 toobe입니다: HSTS hello 대상 도메인에 대 한 HTTP 요청 tooHTTPS를 자동으로 리디렉션하여</li><li>중간자 개입 공격자가 잘못 된 인증서를 사용 하 여 희생자 사용자 로부터 toointercept 트래픽을 시도 하 고 hello 사용자 hello 잘못 된 인증서를 수락할에서는 나중에 찾아낸: HSTS toooverride hello 유효 하지 않은 인증서 사용자 메시지를 허용 하지 않습니다</li></ul>|

## <a id="sqlserver-validation"></a>SQL 서버 연결 암호화 및 인증서 유효성 검사 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | SQL Azure  |
| **특성**              | SQL 버전 - V12 |
| **참조**              | [SQL Database의 보안 연결 문자열 작성에 대한 모범 사례](http://social.technet.microsoft.com/wiki/contents/articles/2951.windows-azure-sql-database-connection-security.aspx#best) |
| **단계** | <p>SQL Database와 클라이언트 응용 프로그램 간의 모든 통신은 항상 SSL(Secure Sockets Layer)을 사용하여 암호화됩니다. SQL Database는 암호화되지 않은 연결을 지원하지 않습니다. 명시적으로 응용 프로그램 코드 또는 도구를 사용 하 여 toovalidate 인증서는 암호화 된 연결을 요청 하 고 hello 서버 인증서를 신뢰 하지 않습니다. 응용 프로그램 코드 또는 도구가 암호화된 연결을 요청하지 않더라도 암호화된 연결을 받습니다.</p><p>그러나 Hello 서버 인증서의 유효성을 검사 하지 않을 수 있습니다 및 노출 될 너무 "hello 중간에 man" 공격입니다. ADO.NET 응용 프로그램 코드를 사용 하 여 toovalidate 인증서 설정 `Encrypt=True` 및 `TrustServerCertificate=False` hello 데이터베이스 연결 문자열에 있습니다. SQL Server Management Studio를 통해 toovalidate 인증서 hello 연결 tooServer 대화 상자를 엽니다. Hello 연결 속성 탭에서 연결 암호화를 클릭 합니다.</p>|

## <a id="encrypted-sqlserver"></a>암호화 된 통신 tooSQL 서버 적용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | OnPrem |
| **특성**              | SQL 버전 - MsSQL2016, SQL 버전 - MsSQL2012, SQL 버전 - MsSQL2014 |
| **참조**              | [암호화 연결 toohello 데이터베이스 엔진을 사용 하도록 설정](https://msdn.microsoft.com/library/ms191192)  |
| **단계** | SSL을 사용 하면 암호화는 SQL Server 인스턴스 및 응용 프로그램 간에 네트워크를 통해 전송 되는 데이터의 보안을 hello 증가 합니다. |

## <a id="comm-storage"></a>HTTPS를 통해 저장소는 해당 통신 tooAzure 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Azure Storage 전송 수준 암호화 - HTTPS 사용](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_encryption-in-transit) |
| **단계** | Azure 저장소 데이터 전송 시의 tooensure hello 보안 개체 저장소에 액세스 하거나 hello REST Api를 호출 하는 경우 항상 hello HTTPS 프로토콜을 사용 합니다. 또한 toodelegate 사용된 될 수 있는 공유 액세스 서명, tooAzure 저장소 개체에 액세스를 공유 액세스 서명, SAS 토큰으로 링크를 보내는 모든 사용자는 확인을 사용 하는 경우 HTTPS 프로토콜을 사용할 수만 해당 hello 옵션 toospecify 포함 hello 적절 한 프로토콜을 사용 합니다.|

## <a id="md5-https"></a>HTTPS를 사용할 수 없는 경우 Blob을 다운로드한 후 MD5 해시 유효성 검사

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | StorageType - Blob |
| **참조**              | [Microsoft Azure Blob의 MD5 개요](https://blogs.msdn.microsoft.com/windowsazurestorage/2011/02/17/windows-azure-blob-md5-overview/)(영문) |
| **단계** | <p>Windows Azure Blob 서비스는 hello 응용 프로그램 및 전송 계층에서 모두 메커니즘 tooensure 데이터 무결성을 제공 합니다. Toohelp 전송 되는 hello blob의 hello 무결성을 확인 toouse HTTPS 대신 HTTP 블록 blob 사용 하는 필요한 어떤 이유로 있습니다 사용할 수 있는 경우 MD5 검사</p><p>이렇게 하면 네트워크/전송 계층 오류로부터 보호되지만 항상 중간 공격을 막을 수 있는 것은 아닙니다. 전송 수준 보안을 제공하는 HTTPS를 사용할 수 있는 경우 MD5 확인을 사용하는 것은 중복된 작업으로 불필요합니다.</p>|

## <a id="smb-shares"></a>SMB 3.0 호환 되는 클라이언트 tooensure 전송 중인 데이터 암호화 tooAzure 파일 공유를 사용 하 여

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 모바일 클라이언트 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | StorageType - 파일 |
| **참조**              | [Azure File Storage](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/#comment-2529238931), [Windows 클라이언트에 대한 Azure File Storage SMB 지원](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/#_mount-the-file-share) |
| **단계** | Azure 파일 저장소 hello REST API를 사용 하는 경우 HTTPS를 지원 하지만 일반적으로 SMB 파일 공유 tooa VM 연결에 사용 합니다. SMB 2.1 암호화를 지원 하지 않으므로 연결이 허용 됩니다 hello 동일한 azure에서 지역입니다. 그러나 SMB 3.0 암호화를 지 원하는 및 Windows Server 2012 r 2와 함께 사용할 수, 액세스 및 hello 바탕 화면에 대 한 액세스를 포함 하 여 Windows 8, Windows 8.1 및 Windows 10에서 지역 간 수 있도록 합니다. |

## <a id="cert-pinning"></a>인증서 고정 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, Windows Phone |
| **특성**              | 해당 없음  |
| **참조**              | [인증서 및 공개 키 고정](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#.Net)(영문) |
| **단계** | <p>인증서 고정은 MITM(메시지 가로채기) 공격을 방어합니다. Hello 프로세스의 예상된 X509와 호스트를 연결 고정이 인증서 또는 공개 키입니다. 인증서 또는 공개 키가 알 수 없거나 호스트에 대 한 표시, 되 면 hello 인증서 또는 공개 키는 연결 또는 '고정' toohello 호스트입니다. </p><p>따라서 악의적인 사용자가 SSL MITM 공격에서는 공격자의 서버에서 SSL 핸드셰이크 hello 키 중 다르게 됩니다 toodo 시도할 때 hello 인증서의 키를 고정 하 고 hello 요청이 무시 됩니다, 그리고 MITM 인증서 하지 못하도록 차단 고정 하 여 수행할 수 있습니다. ServicePointManager의 구현 `ServerCertificateValidationCallback` 위임 합니다.</p>|

### <a name="example"></a>예제
```C#
using System;
using System.Net;
using System.Net.Security;
using System.Security.Cryptography;

namespace CertificatePinningExample
{
    class CertificatePinningExample
    {
        /* Note: In this example, we're hardcoding a hello certificate's public key and algorithm for 
           demonstration purposes. In a real-world application, this should be stored in a secure
           configuration area that can be updated as needed. */

        private static readonly string PINNED_ALGORITHM = "RSA";

        private static readonly string PINNED_PUBLIC_KEY = "3082010A0282010100B0E75B7CBE56D31658EF79B3A1" +
            "294D506A88DFCDD603F6EF15E7F5BCBDF32291EC50B2B82BA158E905FE6A83EE044A48258B07FAC3D6356AF09B2" +
            "3EDAB15D00507B70DB08DB9A20C7D1201417B3071A346D663A241061C151B6EC5B5B4ECCCDCDBEA24F051962809" +
            "FEC499BF2D093C06E3BDA7D0BB83CDC1C2C6660B8ECB2EA30A685ADE2DC83C88314010FFC7F4F0F895EDDBE5C02" +
            "ABF78E50B708E0A0EB984A9AA536BCE61A0C31DB95425C6FEE5A564B158EE7C4F0693C439AE010EF83CA8155750" +
            "09B17537C29F86071E5DD8CA50EBD8A409494F479B07574D83EDCE6F68A8F7D40447471D05BC3F5EAD7862FA748" +
            "EA3C92A60A128344B1CEF7A0B0D94E50203010001";


        public static void Main(string[] args)
        {
            HttpWebRequest request = (HttpWebRequest)WebRequest.Create("https://azure.microsoft.com");
            request.ServerCertificateValidationCallback = (sender, certificate, chain, sslPolicyErrors) =>
            {
                if (certificate == null || sslPolicyErrors != SslPolicyErrors.None)
                {
                    // Error getting certificate or hello certificate failed basic validation
                    return false;
                }

                var targetKeyAlgorithm = new Oid(certificate.GetKeyAlgorithm()).FriendlyName;
                var targetPublicKey = certificate.GetPublicKeyString();
                
                if (targetKeyAlgorithm == PINNED_ALGORITHM &&
                    targetPublicKey == PINNED_PUBLIC_KEY)
                {
                    // Success, hello certificate matches hello pinned value.
                    return true;
                }
                // Reject, either hello key or hello algorithm does not match hello expected value.
                return false;
            };

            try
            {
                var response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine($"Success, HTTP status code: {response.StatusCode}");
            }
            catch(Exception ex)
            {
                Console.WriteLine($"Failure, {ex.Message}");
            }
            Console.WriteLine("Press any key tooend.");
            Console.ReadKey();
        }
    }
}
```

## <a id="https-transport"></a>HTTPS 사용 설정 - 보안 전송 채널

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | NET Framework 3 |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | hello 응용 프로그램 구성 HTTPS 모든 액세스 toosensitive 정보에 사용 됨을 확인 해야 합니다.<ul><li>**설명:** 만 허용 하도록 toocommunicate 암호화 된 전송 채널을 통해 응용 프로그램 중요 한 정보를 처리 하 고 메시지 수준 암호화를 사용 하지 않는 경우.</li><li>**권장 사항:** HTTP 전송을 사용하지 않는 대신 HTTPS 전송을 사용하도록 설정합니다. 예를 들어 hello 대체 `<httpTransport/>` 와 `<httpsTransport/>` 태그입니다. 보안 채널을 통해만 hello 응용 프로그램에 액세스할 수 있다는 네트워크 구성 (방화벽) tooguarantee에 의존 하지 마십시오. 철학적 관점에서 hello 응용 프로그램 보안에 대 한 hello 네트워크 신뢰 하지 않아야 합니다.</li></ul><p>실제 관점에서 hello 담당자 hello 네트워크 보안에 대 한 추적 안 함 항상 hello 응용 프로그램의 보안 요구 사항을 hello 발전 하 합니다.</p>|

## <a id="message-protection"></a>WCF: 집합 메시지 보안 보호 수준 tooEncryptAndSign

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | .NET Framework 3 |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff650862.aspx) |
| **단계** | <ul><li>**설명:** 보호 수준이 설정 된 경우 너무 "none"을 메시지 보호 합니다. 적절한 수준의 설정을 통해 기밀성과 무결성을 보장합니다.</li><li>**권장 사항:**<ul><li>`Mode=None`인 경우 - 메시지 보호를 사용하지 않도록 설정</li><li>때 `Mode=Sign` -hello 메시지를 암호화 하지 않으면 데이터 무결성은 중요 한 경우 사용 해야 하지만 기호</li><li>때 `Mode=EncryptAndSign` -기호 hello 메시지를 암호화 합니다.</li></ul></li></ul><p>암호화를 해제 하 고 기밀 염려 하지 않고 hello 정보의 toovalidate hello 무결성 하기만 하면 때만 메시지를 서명 것이 좋습니다. 이 작업에 대 한 유용할 수 있습니다 또는 서비스는 계약의 계약 toovalidate hello 원래 보낸 사람이 필요 하지만 중요 한 데이터가 전송 됩니다. Hello 보호 수준을 줄일 때 해당 hello 메시지에는 개인 식별이 가능한 정보 (PII) 주의 해야 합니다.</p>|

### <a name="example"></a>예제
Hello 서비스 및 hello 작업 tooonly hello 메시지에 서명 구성 예제 따르는 hello에 표시 됩니다. 서비스 계약 예제 `ProtectionLevel.Sign`: hello 다음은 ProtectionLevel.Sign hello 서비스 계약 수준에서 사용 하는 예제: 
```
[ServiceContract(Protection Level=ProtectionLevel.Sign] 
public interface IService 
  { 
  string GetData(int value); 
  } 
```

### <a name="example"></a>예제
작업 계약 예제 `ProtectionLevel.Sign` 세부적인 제어) (에: hello 다음은 사용 하는 예제 `ProtectionLevel.Sign` hello OperationContract 수준에서:

```
[OperationContract(ProtectionLevel=ProtectionLevel.Sign] 
string GetData(int value);
``` 

## <a id="least-account-wcf"></a>WCF: 최소 권한 계정을 toorun를 WCF 서비스 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | .NET Framework 3 |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648826.aspx ) |
| **단계** | <ul><li>**설명:** 관리자 또는 권한이 높은 계정으로 WCF 서비스를 실행하면 안됩니다. 서비스가 손상된 경우 중대한 영향을 미칩니다.</li><li>**권장 작업:** 프로그램 WCF 서비스 응용 프로그램의 공격 노출을 줄일를 얻을 공격 하는 경우 hello 잠재적 피해를 줄일 수 있으므로 최소 권한 계정을 toohost를 사용 합니다. Hello 서비스 계정이 필요한 경우 MSMQ 등의 인프라 리소스에 대 한 추가 액세스 권한, hello hello 파일 시스템 이벤트 로그 및 성능 카운터를 적절 한 권한은 부여 해야 toothese 리소스 hello WCF 서비스를 실행할 수 있도록 했습니다.</li></ul><p>서비스를 특정 리소스 tooaccess hello 원래 호출자를 대신 하 여 필요한 경우 다운스트림 권한 부여를 확인 하기 위한 가장 및 위임 tooflow hello 호출자의 id를 사용 합니다. 개발 시나리오에서는 hello 로컬 네트워크 서비스 계정을 사용 권한은 제한 되어 있는 특수 기본 제공 계정입니다. 프로덕션 시나리오에서는 최소 권한의 사용자 지정 도메인 서비스 계정을 만듭니다.</p>|

## <a id="webapi-https"></a>HTTPS 연결을 통해 모든 트래픽을 tooWeb Api 강제

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC5, MVC6 |
| **특성**              | 해당 없음  |
| **참조**              | [Web API 컨트롤러에서 SSL 적용](http://www.asp.net/web-api/overview/security/working-with-ssl-in-web-api) |
| **단계** | 응용 프로그램에 HTTPS 및 HTTP 바인딩을 모두 있으면, 클라이언트 HTTP tooaccess hello 사이트 여전히 사용할 수 있습니다. tooprevent tooprotected Api를 요청 하는 작업 필터 tooensure는 항상 HTTPS를 통해이 사용 합니다.|

### <a name="example"></a>예제 
hello 다음 코드를 보여 줍니다 SSL에 대 한 확인 하는 Web API 인증 필터: 
```C#
public class RequireHttpsAttribute : AuthorizationFilterAttribute
{
    public override void OnAuthorization(HttpActionContext actionContext)
    {
        if (actionContext.Request.RequestUri.Scheme != Uri.UriSchemeHttps)
        {
            actionContext.Response = new HttpResponseMessage(System.Net.HttpStatusCode.Forbidden)
            {
                ReasonPhrase = "HTTPS Required"
            };
        }
        else
        {
            base.OnAuthorization(actionContext);
        }
    }
}
```
Ssl을 사용 하는이 필터 tooany 웹 API 작업을 추가 합니다. 
```C#
public class ValuesController : ApiController
{
    [RequireHttps]
    public HttpResponseMessage Get() { ... }
}
```
 
## <a id="redis-ssl"></a>Redis 캐시는 SSL을 통해 해당 통신 tooAzure 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure Redis 캐시(영문) | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Azure Redis SSL 지원](https://azure.microsoft.com/documentation/articles/cache-faq/#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis) |
| **단계** | Redis 서버 hello 초기 SSL을 지원 하지 않지만 Azure Redis Cache 않습니다. 클라이언트가 원하는 StackExchange.Redis, 같은 SSL tooAzure Redis Cache를 연결 하는 경우 SSL을 사용 해야 합니다. 기본적으로 비SSL 포트는 새 Azure Redis Cache 인스턴스에 대해 사용하지 않도록 설정됩니다. Redis 클라이언트에 대 한 SSL 지원에 대 한 종속성 있으면 hello 보안 기본값 변경 되지 않도록 확인 합니다. |

Redis는 신뢰할 수 있는 환경 내의 신뢰할 수 있는 클라이언트에서 액세스 하는 디자인 된 toobe note 하십시오. 즉, 일반적으로 아닌지 좋은 아이디어 tooexpose hello Redis 인스턴스 toohello 직접 인터넷 또는 신뢰할 수 없는 클라이언트가 직접 액세스할 수 있는 tooan 환경에서 Redis TCP 포트 또는 UNIX 소켓을 환영 하는 일반적으로 합니다. 

## <a id="device-field"></a>보안 장치 tooField 게이트웨이 통신

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 필드 게이트웨이 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | IP 기반 장치에 대 한 일반적으로 전송 되는 SSL/TLS 채널 tooprotect 데이터에 대 hello 통신 프로토콜 캡슐화 할 수 없습니다. SSL/TLS를 지원 하지 않는 다른 프로토콜에 대 한 보안 버전의 hello 프로토콜 전송 또는 메시지 계층에서 보안을 제공 하는 경우를 조사 합니다. |

## <a id="device-cloud"></a>장치 tooCloud SSL/TLS를 사용 하 여 게이트웨이 통신 보안

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 클라우드 게이트웨이 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [통신 프로토콜 선택](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#messaging) |
| **단계** | SSL/TLS를 사용하여 HTTP/AMQP 또는 MQTT 프로토콜 보안을 유지합니다. |
