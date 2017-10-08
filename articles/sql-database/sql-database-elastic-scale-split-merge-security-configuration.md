---
title: "aaaSplit 병합 보안 구성 | Microsoft Docs"
description: "암호화에 대한 409 인증서를 설정"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a>분할-병합 보안 구성
toouse hello 분할/병합 서비스 올바르게 보안을 구성 해야 합니다. hello 서비스는 Microsoft Azure SQL 데이터베이스의 탄력적인 크기 조정 기능은 hello의 일부입니다. 자세한 내용은 [탄력적인 확장 분할 및 병합 서비스 자습서](sql-database-elastic-scale-configure-deploy-split-and-merge.md)를 참조하세요.

## <a name="configuring-certificates"></a>인증서 구성
인증서는 두 가지 방법으로 구성합니다. 

1. [tooConfigure hello SSL 인증서](#to-configure-the-ssl-certificate)
2. [tooConfigure 클라이언트 인증서](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a>tooobtain 인증서
Hello 또는 공용 ca (인증 기관)에서 인증서를 구할 수 [Windows 인증서 서비스](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx)합니다. 이들은 기본 hello 메서드 tooobtain 인증서입니다.

이러한 옵션을 사용할 수 없는 경우 **자체 서명된 인증서**를 생성할 수 있습니다.

## <a name="tools-toogenerate-certificates"></a>도구 toogenerate 인증서
* [makecert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a>toorun hello 도구
* Visual Studio용 개발자 명령 프롬프트에서 [Visual Studio 명령 프롬프트를 참조하세요](http://msdn.microsoft.com/library/ms229859.aspx) 
  
    설치되어 있는 경우 다음으로 이동합니다.
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* 가져오기 WDK에서 hello [Windows 8.1: 키트 및 도구 다운로드](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="tooconfigure-hello-ssl-certificate"></a>tooconfigure hello SSL 인증서
SSL 인증서는 필요한 tooencrypt hello 통신 하 고 hello 서버 인증 합니다. 아래 세 가지 시나리오 hello 중 가장 적합 hello 선택한 모든 단계를 실행 합니다.

### <a name="create-a-new-self-signed-certificate"></a>자체 서명된 새로운 인증서 만들기
1. [자체 서명된 인증서 만들기](#create-a-self-signed-certificate)
2. [자체 서명된 SSL 인증서용 PFX 파일 만들기](#create-pfx-file-for-self-signed-ssl-certificate)
3. [SSL 인증서 tooCloud 서비스 업로드](#upload-ssl-certificate-to-cloud-service)
4. [서비스 구성 파일에서 SSL 인증서 업데이트](#update-ssl-certificate-in-service-configuration-file)
5. [SSL 인증 기관 가져오기](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a>toouse hello 인증서에서 기존 인증서 저장
1. [인증서 저장소에서 SSL 인증서 내보내기](#export-ssl-certificate-from-certificate-store)
2. [SSL 인증서 tooCloud 서비스 업로드](#upload-ssl-certificate-to-cloud-service)
3. [서비스 구성 파일에서 SSL 인증서 업데이트](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a>toouse PFX 파일에 기존 인증서
1. [SSL 인증서 tooCloud 서비스 업로드](#upload-ssl-certificate-to-cloud-service)
2. [서비스 구성 파일에서 SSL 인증서 업데이트](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a>tooconfigure 클라이언트 인증서
주문 tooauthenticate 요청 toohello 서비스에서 클라이언트 인증서 필요 합니다. 아래 세 가지 시나리오 hello 중 가장 적합 hello 선택한 모든 단계를 실행 합니다.

### <a name="turn-off-client-certificates"></a>클라이언트 인증서 해제
1. [클라이언트 인증서 기반 인증 해제](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>자체 서명된 새로운 클라이언트 인증서 발급
1. [자체 서명된 인증 기관 만들기](#create-a-self-signed-certification-authority)
2. [CA 인증서 tooCloud 서비스 업로드](#upload-ca-certificate-to-cloud-service)
3. [서비스 구성 파일의 CA 인증서 업데이트](#update-ca-certificate-in-service-configuration-file)
4. [클라이언트 인증서 발급](#issue-client-certificates)
5. [클라이언트 인증서용 PFX 파일 만들기](#create-pfx-files-for-client-certificates)
6. [클라이언트 인증서 가져오기](#Import-Client-Certificate)
7. [클라이언트 인증서 지문 복사](#copy-client-certificate-thumbprints)
8. [Hello 서비스 구성 파일에서에서 허용 하는 클라이언트를 구성 합니다.](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>기존 클라이언트 인증서 사용
1. [Find CA Public Key](#find-ca-public-key)
2. [CA 인증서 tooCloud 서비스 업로드](#Upload-CA-certificate-to-cloud-service)
3. [서비스 구성 파일의 CA 인증서 업데이트](#Update-CA-Certificate-in-Service-Configuration-File)
4. [클라이언트 인증서 지문 복사](#Copy-Client-Certificate-Thumbprints)
5. [Hello 서비스 구성 파일에서에서 허용 하는 클라이언트를 구성 합니다.](#configure-allowed-clients-in-the-service-configuration-file)
6. [클라이언트 인증서 해지 확인 구성](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>허용된 IP 주소
액세스 toohello 서비스 끝점의 IP 주소 범위를 제한 된 toospecific 될 수 있습니다.

## <a name="tooconfigure-encryption-for-hello-store"></a>hello 저장소에 대 한 tooconfigure 암호화
인증서는 필수 tooencrypt hello 자격 증명을 hello 메타 데이터 저장소에 저장 됩니다. 아래 세 가지 시나리오 hello 중 가장 적합 hello 선택한 모든 단계를 실행 합니다.

### <a name="use-a-new-self-signed-certificate"></a>자체 서명된 새로운 인증서 사용
1. [자체 서명된 인증서 만들기](#create-a-self-signed-certificate)
2. [자체 서명된 암호화 인증서용 PFX 파일 만들기](#create-pfx-file-for-self-signed-ssl-certificate)
3. [암호화 인증서 tooCloud 서비스 업로드](#upload-encryption-certificate-to-cloud-service)
4. [서비스 구성 파일에서 암호화 인증서 업데이트](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a>Hello 인증서 저장소에서 기존 인증서를 사용 합니다.
1. [인증서 저장소에서 암호화 인증서 내보내기](#export-encryption-certificate-from-certificate-store)
2. [암호화 인증서 tooCloud 서비스 업로드](#upload-encryption-certificate-to-cloud-service)
3. [서비스 구성 파일에서 암호화 인증서 업데이트](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>PFX 파일에서 기존 인증서 사용
1. [암호화 인증서 tooCloud 서비스 업로드](#upload-encryption-certificate-to-cloud-service)
2. [서비스 구성 파일에서 암호화 인증서 업데이트](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a>hello 기본 구성
hello 기본 구성은 모든 액세스 toohello HTTP 끝점을 거부합니다. 이 hello hello 요청 toothese 끝점 데이터베이스 자격 증명 등과 같은 기밀 정보를 전달할 수 있으므로 권장 설정 합니다.
hello 기본 구성은 모든 액세스 toohello HTTPS 끝점을 허용합니다. 이 설정을 추가로 제한할 수 있습니다.

### <a name="changing-hello-configuration"></a>Hello 구성 변경
hello tooand 끝점 적용 되는 액세스 제어 규칙의 그룹에에서 구성 된 hello  **<EndpointAcls>**  hello 섹션인 **서비스 구성 파일**합니다.

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

액세스 제어 그룹에서 hello 규칙에 구성 된는 <AccessControl name=""> hello 서비스 구성 파일의 섹션입니다. 

hello 형식 설명서 네트워크 액세스 제어 목록에 설명 되어 있습니다.
예를 들어 tooallow hello 범위 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS 끝점의 유일한 Ip hello 규칙은 다음과 같습니다.

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>서비스 거부 방지
다른 두 가지 메커니즘 toodetect 지원 및 서비스 거부 공격을 방지 합니다.

* 원격 호스트당 동시 요청 수 제한(기본적으로 해제됨)
* 원격 호스트당 액세스 속도 제한(기본적으로 설정됨)

이 기능을 기반으로 hello IIS에서 동적 IP 보안에서 설명 되어 있습니다. 때 hello 요소 뒤의 조심이 구성 변경:

* 프록시 및 네트워크 주소 변환 장치 hello 원격 호스트 정보에 대해의 hello 동작
* Hello 웹 역할에서 각 요청 tooany 리소스 (예: 스크립트, 이미지 등 로드) 것으로 간주 됩니다.

## <a name="restricting-number-of-concurrent-accesses"></a>동시 액세스 수 제한
이 동작을 구성 하는 hello 설정은 다음과 같습니다.

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

이 보호 DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable를 변경 합니다.

## <a name="restricting-rate-of-access"></a>액세스 속도 제한
이 동작을 구성 하는 hello 설정은 다음과 같습니다.

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a>Hello 응답 tooa 구성 요청을 거부 했습니다.
hello 다음 설정을 구성 합니다 hello 응답 tooa를 요청을 거부 했습니다.

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
IIS에서 동적 IP 보안에 대 한 기타 지원 되는 값에 대 한 toohello 문서를 참조 하십시오.

## <a name="operations-for-configuring-service-certificates"></a>서비스 인증서 구성 작업
이 항목은 참조용일 뿐입니다. 에 설명 된 hello 구성 단계를 수행 하십시오.

* Hello SSL 인증서 구성
* 클라이언트 인증서 구성

## <a name="create-a-self-signed-certificate"></a>자체 서명된 인증서 만들기
다음 코드를 실행합니다.

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

toocustomize:

* -n hello로 서비스 URL입니다. 와일드카드("CN=*.cloudapp.net") 및 대체 이름("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net")이 지원됩니다.
* -e hello 인증서 만료 날짜와 함께 강력한 암호를 만들고 대화 상자가 나타나면이 지정 합니다.

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>자체 서명된 SSL 인증서용 PFX 파일 만들기
다음 코드를 실행합니다.

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

암호를 입력하고 다음 옵션을 사용하여 인증서를 내보냅니다.

* 예, hello 개인 키를 내보냅니다.
* 확장된 속성 모두 내보내기

## <a name="export-ssl-certificate-from-certificate-store"></a>인증서 저장소에서 SSL 인증서 내보내기
* 인증서를 찾습니다.
* 작업-> 모든 작업 -> 내보내기를 클릭합니다.
* 다음 옵션을 사용하여 .PFX 파일로 인증서를 내보냅니다.
  * 예, hello 개인 키를 내보냅니다.
  * 가능 하면 hello 인증 경로 있는 모든 인증서를 포함 * 모든 확장된 속성을 내보내려면

## <a name="upload-ssl-certificate-toocloud-service"></a>SSL 인증서 toocloud 서비스 업로드
기존 컨트롤이 나 생성 hello로 인증서를 업로드 합니다. PFX 파일 hello SSL 키 쌍을 됩니다.

* Hello 개인 키 정보를 보호 하는 hello 암호를 입력 합니다.

## <a name="update-ssl-certificate-in-service-configuration-file"></a>서비스 구성 파일에서 SSL 인증서 업데이트
Hello 업로드 한 인증서 toohello 클라우드 서비스의 hello 문으로 hello 서비스 구성 파일의 설정에 따라 hello의 hello 지문 값을 업데이트 합니다.

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>SSL 인증 기관 가져오기
Hello 서비스와 통신 하는 모든 계정/컴퓨터에서 다음이 단계를 수행 합니다.

* Hello를 두 번 클릭 합니다. Windows 탐색기에서 CER 파일
* Hello 인증서 대화 상자에 인증서 설치를 클릭 하십시오...
* Hello 신뢰할 수 있는 루트 인증 기관 저장소로 인증서를 가져옵니다

## <a name="turn-off-client-certificate-based-authentication"></a>클라이언트 인증서 기반 인증 해제
사용 하지 않는 것을 사용 하면 공용 액세스 toohello 서비스 끝점에 대해 다른 메커니즘 (예: Microsoft Azure 가상 네트워크)에 도달 하지 못할 경우 및 클라이언트 인증서 기반 인증만 지원 됩니다.

Hello 서비스 구성 파일 tooturn hello 기능에서 이러한 설정을 toofalse 해제 변경:

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

그런 다음 CA hello 인증서 설정에 hello hello SSL로 동일한 지문이 인증서를 복사 합니다.

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>자체 서명된 인증 기관 만들기
다음 단계 toocreate 인증 기관으로 자체 서명 된 인증서 tooact hello를 실행 합니다.

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

toocustomize 것

* -e hello 인증 만료 날짜와 함께

## <a name="find-ca-public-key"></a>CA 공개 키 찾기
모든 클라이언트 인증서 hello 서비스에서 신뢰할 수 있는 인증 기관에서 발급 합니다. Hello 공개 키 toohello toobe가는 hello 클라이언트 인증서를 발급 한 인증 기관을 인증에에서 사용 되 순서 tooupload 것 toohello 클라우드 서비스를 찾습니다.

Hello 파일 hello 공개 키로 사용할 수 없는 경우 hello 인증서 저장소에서 내보냅니다.

* 인증서를 찾습니다.
  * 발급 한 클라이언트 인증서에 대 한 검색 hello 같은 인증 기관
* Hello 인증서를 두 번 클릭 합니다.
* Hello 인증서 대화 상자에서 hello 인증 경로 탭을 선택 합니다.
* Hello 경로에 hello CA 항목을 두 번 클릭 합니다.
* Hello 인증서 속성을 기록해 둡니다.
* 닫기 hello **인증서** 대화 상자.
* 인증서를 찾습니다.
  * 위에서 언급 한 CA hello에 대 한 검색입니다.
* 작업-> 모든 작업 -> 내보내기를 클릭합니다.
* 다음 옵션을 사용하여 .CER 파일로 인증서를 내보냅니다.
  * **아니요, hello 개인 키를 내보내지 않습니다**
  * 가능 하면 hello 인증 경로 있는 모든 인증서를 포함 합니다.
  * 확장된 속성 모두 내보내기

## <a name="upload-ca-certificate-toocloud-service"></a>CA 인증서 toocloud 서비스 업로드
기존 컨트롤이 나 생성 hello로 인증서를 업로드 합니다. Hello CA 공개 키로 CER 파일입니다.

## <a name="update-ca-certificate-in-service-configuration-file"></a>서비스 구성 파일의 CA 인증서 업데이트
Hello 업로드 한 인증서 toohello 클라우드 서비스의 hello 문으로 hello 서비스 구성 파일의 설정에 따라 hello의 hello 지문 값을 업데이트 합니다.

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

Hello 동일 hello로 설정한 후의 hello 값을 업데이트 지문:

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>클라이언트 인증서 발급
각 개별 권한 있는 tooaccess hello 서비스는 클라이언트에 대해 인증서 발급 his/hers 배타적 사용 하 고 강력한 암호 tooprotect를 소유 his/hers 해당 개인 키를 선택 해야 합니다. 

단계를 수행 하는 hello CA 인증서에 hello 자체 서명 된 동일한 컴퓨터에서 생성 하 고 저장 된 hello에서 실행 해야 합니다.

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

사용자 지정:

* 이 인증서로 인증할 수 toohello 클라이언트에 대 한 id-n
* -e hello 인증서 만료 날짜와 함께
* MyID.pvk 및 MyID.cer과 이 클라이언트 인증서의 고유한 파일 이름

이 명령은 만들고 한 번 사용 되는 암호 toobe 메시지가 나타납니다. 강력한 암호를 사용하세요.

## <a name="create-pfx-files-for-client-certificates"></a>클라이언트 인증서용 PFX 파일 만들기
생성된 각 클라이언트 인증서에 대해 다음을 실행합니다.

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

사용자 지정:

    MyID.pvk and MyID.cer with hello filename for hello client certificate

암호를 입력하고 다음 옵션을 사용하여 인증서를 내보냅니다.

* 예, hello 개인 키를 내보냅니다.
* 확장된 속성 모두 내보내기
* 이 인증서를 발급 하는 hello 개별 toowhom hello 내보내기 암호를 선택 해야

## <a name="import-client-certificate"></a>클라이언트 인증서 가져오기
사용자에 대 한 클라이언트 인증서가 발급 된 각 개별 hello 키 쌍을 가져와야 hello 컴퓨터 자신이 사용 하 여 toocommunicate hello 서비스:

* Hello를 두 번 클릭 합니다. Windows 탐색기에서 PFX 파일
* Hello 개인 저장소와 적어도이 옵션으로 인증서를 가져옵니다.
  * 확장된 속성 모두 포함 옵션 선택

## <a name="copy-client-certificate-thumbprints"></a>클라이언트 인증서 지문 복사
대상에 대 한 클라이언트 인증서가 발급 된 각 개별 his/hers의 순서 tooobtain hello 지문에서 다음이 단계를 수행 해야 인증서 toohello 서비스 구성 파일을 추가 합니다.

* Certmgr.exe 실행
* Hello 개인 탭 선택
* 인증에 사용 되는 toobe hello 클라이언트 인증서를 두 번 클릭
* Hello 인증서 대화 상자가 열리면 hello 세부 정보 탭 선택
* 표시가 모두를 나타내는지 확인합니다.
* Hello 목록에서 지문 라는 hello 선택 필드
* Hello 지문 안녕하세요 값 복사 * * hello 첫 번째 숫자 앞에 표시 되지 않는 유니코드 문자 삭제 * * 모든 공백 삭제

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a>Hello 서비스 구성 파일에 허용 된 클라이언트를 구성 합니다.
Hello hello toohello 서비스 액세스를 허용 하는 hello 클라이언트 인증서의 지문 안녕하세요 쉼표로 구분 된 목록이 있는 hello 서비스 구성 파일의 설정에 따라 값을 업데이트 합니다.

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>클라이언트 인증서 해지 확인 구성
클라이언트 인증서 해지 상태에 대 한 인증 기관 hello로 hello 기본 설정을 확인 하지 않습니다. hello hello 클라이언트 인증서를 발급 한 인증 기관에서 이러한 검사를 지 원하는 경우 hello에 tooturn 검사 같이 hello hello X509RevocationMode 열거형에에서 정의 된 hello 값 중 하나가 지정 된 설정에 따라 변경 합니다.

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>자체 서명된 암호화 인증서용 PFX 파일 만들기
암호화 인증서에 대해 다음을 실행합니다.

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

사용자 지정:

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

암호를 입력하고 다음 옵션을 사용하여 인증서를 내보냅니다.

* 예, hello 개인 키를 내보냅니다.
* 확장된 속성 모두 내보내기
* Hello 인증서 toohello 클라우드 서비스에 업로드할 때 hello 암호가 필요 합니다.

## <a name="export-encryption-certificate-from-certificate-store"></a>인증서 저장소에서 암호화 인증서 내보내기
* 인증서를 찾습니다.
* 작업-> 모든 작업 -> 내보내기를 클릭합니다.
* 다음 옵션을 사용하여 .PFX 파일로 인증서를 내보냅니다. 
  * 예, hello 개인 키를 내보냅니다.
  * 가능 하면 hello 인증 경로 있는 인증서 모두 포함 
* 확장된 속성 모두 내보내기

## <a name="upload-encryption-certificate-toocloud-service"></a>암호화 인증서 toocloud 서비스 업로드
기존 컨트롤이 나 생성 hello로 인증서를 업로드 합니다. PFX 파일 hello 암호화 키 쌍을 됩니다.

* Hello 개인 키 정보를 보호 하는 hello 암호를 입력 합니다.

## <a name="update-encryption-certificate-in-service-configuration-file"></a>서비스 구성 파일에서 암호화 인증서 업데이트
Hello hello 업로드 한 인증서 toohello 클라우드 서비스의 hello 문으로 hello 서비스 구성 파일의 설정은 다음의 hello 지문 값을 업데이트 합니다.

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>일반 인증서 작업
* Hello SSL 인증서 구성
* 클라이언트 인증서 구성

## <a name="find-certificate"></a>인증서를 찾습니다.
다음 단계를 수행하세요.

1. Mmc.exe를 실행합니다.
2. 파일-> 스냅인 추가/제거로 이동합니다.
3. **인증서**를 선택합니다.
4. **추가**를 클릭합니다.
5. Hello 인증서 저장소 위치를 선택 합니다.
6. **마침**을 클릭합니다.
7. **확인**을 클릭합니다.
8. **인증서**를 확장합니다.
9. Hello 인증서 저장소 노드를 확장 합니다.
10. Hello 인증서 자식 노드를 확장 합니다.
11. Hello 목록에 인증서를 선택 합니다.

## <a name="export-certificate"></a>인증서 내보내기
Hello에 **인증서 내보내기 마법사**:

1. **다음**을 누릅니다.
2. 선택 **예**, 다음 **hello 개인 키 내보내기**합니다.
3. **다음**을 누릅니다.
4. Hello 원하는 출력 파일 형식을 선택 합니다.
5. Hello 원하는 옵션을 확인 합니다.
6. **암호**를 확인합니다.
7. 강력한 암호를 입력하고 이를 확인합니다.
8. **다음**을 누릅니다.
9. 입력 하거나 위치 toostore hello 인증서 파일 이름을 찾습니다 (사용 하는 합니다. 확장명은 PFX)입니다.
10. **다음**을 누릅니다.
11. **마침**을 클릭합니다.
12. **확인**을 클릭합니다.

## <a name="import-certificate"></a>인증서 가져오기
인증서 가져오기 마법사를 hello:

1. Hello 저장소 위치를 선택 합니다.
   
   * 선택 **현재 사용자** 현재 사용자에서 실행 중인 프로세스가 hello 서비스에 액세스 하는 경우에
   * 선택 **로컬 컴퓨터** 이 컴퓨터의 다른 프로세스가 hello 서비스에 액세스 하는 경우
2. **다음**을 누릅니다.
3. 파일에서 가져올 경우 hello 파일 경로 확인 합니다.
4. .PFX 파일을 가져오는 경우:
   1. Hello 개인 키를 보호 하는 hello 암호를 입력 합니다.
   2. 가져오기 옵션을 선택합니다.
5. Hello 저장소를 다음에 "장소" 인증서를 선택 합니다.
6. **찾아보기**를 클릭합니다.
7. Hello 원하는 저장소를 선택 합니다.
8. **마침**을 클릭합니다.
   
   * 클릭 하 여 hello 신뢰할 수 있는 루트 인증 기관 저장소를 선택한 경우 **예**합니다.
9. 모든 대화 상자 창에서 **확인** 을 클릭합니다.

## <a name="upload-certificate"></a>인증서 업로드
Hello에 [Azure 포털](https://portal.azure.com/)

1. **클라우드 서비스**를 선택합니다.
2. Hello 클라우드 서비스를 선택 합니다.
3. Hello 상단 메뉴에서 클릭 **인증서**합니다.
4. Hello 아래쪽 막대에서 클릭 **업로드**합니다.
5. Hello 인증서 파일을 선택 합니다.
6. 경우에 합니다. PFX 파일에서 개인 키 hello hello 암호를 입력 합니다.
7. 완료 되 면 hello hello 목록에 새 항목에서 hello 인증서 지문을 복사 합니다.

## <a name="other-security-considerations"></a>기타 보안 고려 사항
이 문서에서 설명 하는 hello SSL 설정을 hello HTTPS 끝점에서 사용 되는 경우 hello 서비스와 클라이언트 간의 통신을 암호화 합니다. 중요 한 데이터베이스 액세스에 대 한 자격 증명 이후 며이 hello 통신에 포함 될 수 있는 다른 중요 한 정보입니다. 그러나 Note, hello 서비스 메타 데이터 저장소에 대 한 Microsoft Azure 구독에서 제공 된 hello Microsoft Azure SQL 데이터베이스에서 해당 내부 테이블에 자격 증명을 포함 하는 내부 상태를 유지 되도록 합니다. 해당 데이터베이스는 hello 다음 서비스 구성 파일의 설정의 일부분으로 정의 되었습니다 (합니다. CSCFG 파일): 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

이 데이터베이스에 저장된 자격 증명은 암호화됩니다. 그러나 모범 사례로, 웹 및 작업자 역할 모두 하면 서비스 배포의 toodate 위로 유지 되 고 안전 하 게은 둘 다 액세스 toohello 메타 데이터 데이터베이스와 hello 인증서가 저장 된 자격 증명의 암호화 / 해독에 사용 되는 확인 합니다. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

