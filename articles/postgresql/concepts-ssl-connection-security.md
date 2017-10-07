---
title: "PostgreSQL에 대 한 Azure 데이터베이스에서 SSL 연결 aaaConfigure | Microsoft Docs"
description: "지침 및 정보 tooconfigure Azure 데이터베이스 PostgreSQL 및 tooproperly 관련된 응용 프로그램에 대 한 SSL 연결을 사용 합니다."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a>PostgreSQL용 Azure 데이터베이스에서 SSL 연결 구성
PostgreSQL에 대 한 azure 데이터베이스 연결 하는 클라이언트 응용 프로그램 toohello Secure Sockets Layer (SSL)를 사용 하 여 PostgreSQL 서비스를 선호 합니다. 데이터베이스 서버와 클라이언트 응용 프로그램 간의 SSL 연결을 강제 적용 하면 공격 으로부터 보호 "man hello 중간에" hello 서버와 응용 프로그램 간의 hello 데이터 스트림을 암호화 하 여 합니다.

Hello PostgreSQL 데이터베이스 서비스는 기본적으로 구성 된 toorequire SSL 연결입니다. 필요에 따라 클라이언트 응용 프로그램에서 SSL 연결을 지원 하지 않으면 tooyour 데이터베이스 서비스를 연결 하기 위한 SSL이 필요한 비활성화할 수 있습니다. 

## <a name="enforcing-ssl-connections"></a>SSL 연결 적용
PostgreSQL 서버 hello Azure 포털 및 CLI를 통해 프로 비전에 대 한 모든 Azure 데이터베이스에 대 한 SSL 연결의 적용은 기본적으로 사용 됩니다. 

마찬가지로, hello Azure 포털에서에서 해당 서버에서 연결 문자열을 "를" 설정 hello에에서 미리 정의 된 연결 문자열이 SSL을 사용 하 여 일반적인 언어 tooconnect tooyour 데이터베이스 서버에 대 한 필요한 hello 매개 변수를 포함 합니다. hello 매개 변수 SSL에 따라 달라 집니다 hello 커넥터 예를 들어 "ssl = true" 또는 "sslmode = 필요" 또는 "sslmode = 필요" 및 다른 변형 합니다.

## <a name="configure-enforcement-of-ssl"></a>SSL 적용 구성
필요에 따라 SSL 연결 적용을 사용하지 않도록 설정할 수 있습니다. Microsoft Azure에 tooalways 사용 하도록 설정 하는 것이 좋습니다 **적용 SSL 연결** 강화 된 보안을 설정 합니다.

### <a name="using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여
PostgreSQL용 Azure 데이터베이스 서버를 방문하여 **연결 보안**을 클릭합니다. 토글 단추 tooenable hello를 사용 하 여 hello를 사용 하지 않도록 설정 하거나 **적용 SSL 연결** 설정 합니다. 그런 다음 **Save**를 클릭합니다. 

![연결 보안 - SSL 적용 사용 안 함](./media/concepts-ssl-connection-security/1-disable-ssl.png)

Hello를 확인 하 여 hello 설정을 확인할 수 있습니다 **개요** 페이지 toosee hello **SSL 적용 상태** 표시기입니다.

### <a name="using-azure-cli"></a>Azure CLI 사용
Hello를 사용 하지 않도록 설정 하거나 설정할 수 있습니다 **ssl 적용** 매개 변수를 사용 하 여 `Enabled` 또는 `Disabled` Azure CLI 각각의 값입니다.

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a>응용 프로그램 또는 프레임워크가 SSL 연결을 지원하는지 확인합니다.
Drupal 및 Django와 같은 데이터베이스 서비스용 PostgreSQL을 사용하는 많은 일반적인 응용 프로그램 프레임워크는 기본적으로 설치하는 동안 SSL을 사용하도록 설정하지 않습니다. SSL 연결을 사용 하면 설치 후 또는 CLI 명령에 대 한 특정 toohello 응용 프로그램을 통해 수행 되어야 합니다. PostgreSQL 서버에 SSL 연결을 적용 하는 경우 연결 된 hello 응용 프로그램을 제대로 구성 되지 않았습니다 tooconnect tooyour 데이터베이스 서버 hello 응용 프로그램에 실패할 수 있습니다. 응용 프로그램의 설명서 toolearn 방법을 문의 tooenable SSL 연결 합니다.


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a>SSL 연결을 위해 인증서 확인이 필요한 응용 프로그램
경우에 따라 응용 프로그램에 안전 하 게 신뢰할 수 있는 CA (인증 기관) 인증서 (.cer) 파일 tooconnect에서 생성 된 로컬 인증서 파일을 필요 합니다. Hello 다음 단계 tooobtain hello.cer 파일을 참조 하 고 hello 인증서 디코딩 tooyour 응용 프로그램을 바인딩하십시오.

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a>Hello CA (인증 기관)에서 hello 인증서 파일을 다운로드 합니다. 
hello 인증서 toocommunicate Azure 데이터베이스와 함께 SSL을 통해에 필요한 PostgreSQL 서버가 위치한 [여기](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt)합니다. Hello 인증서 파일을 로컬에 다운로드 합니다.

### <a name="download-and-install-openssl-on-your-machine"></a>컴퓨터에 OpenSSL 다운로드 및 설치 
toodecode hello 인증서 파일을 안전 하 게 응용 프로그램 tooconnect에 필요한 tooyour 데이터베이스 서버에 로컬 컴퓨터에서 tooinstall OpenSSL 필요 합니다.

#### <a name="for-linux-os-x-or-unix"></a>Linux, OS X 또는 Unix
hello OpenSSL 라이브러리 hello에서 직접 소스 코드에 제공 됩니다 [OpenSSL 소프트웨어 Foundation](http://www.openssl.org)합니다. hello 다음 지침 안내 hello 단계 필요한 tooinstall OpenSSL Linux PC에서. 이 문서에서는 toowork Ubuntu 12.04에 이상 인식 명령입니다.

터미널 세션을 열고 OpenSSL을 설치합니다.
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
Hello 다운로드 패키지에서 hello 파일을 추출 합니다.
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
Hello 파일이 추출 된 hello 디렉터리를 입력 합니다. 기본적으로 다음과 같아야 합니다.

```bash
cd openssl-1.1.0e
```
OpenSSL hello 다음 명령을 실행 하 여 구성 합니다. Hello 파일 폴더에서를 지정 하려면 /usr/local/openssl 다 확인 있는지 toochange hello 다음 적절 하 게 합니다.

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
OpenSSL 제대로 구성 되어 해야 toocompile 것 tooconvert 인증서입니다. toocompile hello 다음 명령을 실행 합니다.

```bash
make
```
컴파일 완료 되 면 수 준비 tooinstall OpenSSL 실행 파일로 hello 다음 명령을 실행 하 여:
```bash
make install
```
시스템에 OpenSSL을 성공적으로 설치 했습니다 tooconfirm, 실행된 hello 다음 명령 및 toomake hello를 얻었는지 확인 확인 동일한 출력 합니다.

```bash
/usr/local/openssl/bin/openssl version
```
성공 하는 경우에 hello 메시지의 뒤에 표시 됩니다.
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a>Windows의 경우
다음 방법으로 hello에 OpenSSL Windows PC에 설치를 수행할 수 있습니다.
1. **(권장)**  Hello 창 10에서 기본 제공 Windows 용를 이용한 적 기능을 사용 하 고 위에, OpenSSL는 기본적으로 설치 합니다. Windows 10의 Windows 용를 이용한 적 기능 tooenable 수 발견 하는 방법에 대 한 지침 [여기](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)합니다.
2. 통해 hello 커뮤니티에서 제공 하는 Win32/64 응용 프로그램을 다운로드 합니다. 사용 가능한 설치 관리자의 목록을 제공 hello OpenSSL 소프트웨어 Foundation 제공 하거나 특정 Windows installer 모든 보증 하지 않습니다, 동안 [여기](https://wiki.openssl.org/index.php/Binaries)

### <a name="decode-your-certificate-file"></a>인증서 파일 디코딩
hello는 암호화 된 형식으로 파일은 루트 CA를 다운로드 합니다. OpenSSL toodecode hello 인증서 파일을 사용 합니다. 따라서 toodo OpenSSL 명령을 실행 합니다.

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a>SSL 인증서 인증을 사용한 연결 tooAzure PostgreSQL 데이터베이스
인증서를 성공적으로 디코딩할 했으므로 SSL을 통해 데이터베이스 서버 tooyour 안전 하 게 연결할 수 있습니다. tooallow 서버 인증서 유효성 검사 hello 인증서 hello 사용자의 홈 디렉터리에서 파일 ~/.postgresql/root.crt hello에에서 배치 해야 합니다. (Microsoft Windows hello 파일에 이름이 %APPDATA%\postgresql\root.crt.). hello 다음 PostgreSQL에 대 한 tooAzure 데이터베이스를 연결 하기 위한 지침을 제공 합니다.

> [!NOTE]
> 현재는 알려진된 문제를 사용 하는 경우 "sslmode = 확인-full" hello 연결이 연결 toohello 서비스에 다음 오류가 hello로 실패 합니다: _에 대 한 서버 인증서 "&lt;지역&gt;합니다. control.database.windows.net"(및 다른 7 이름) 호스트 이름과 일치 하지 않는"&lt;servername&gt;. postgres.database.azure.com "입니다._
> 경우 "sslmode = 확인-full"는 hello 서버 명명 규칙을 사용 하십시오 필요한  **&lt;servername&gt;. database.windows.net** 연결 문자열 호스트 이름으로 합니다. Tooremove hello 나중에이 제한 사항은 예정입니다. 다른를 사용 하 여 연결 [SSL 모드](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) toouse hello 기본 호스트에 대 한 명명 규칙을 계속 해야  **&lt;servername&gt;. postgres.database.azure.com**합니다.

#### <a name="using-psql-command-line-utility"></a>psql 명령줄 유틸리티 사용
다음 예제는 hello toosuccessfully hello psql 명령줄 유틸리티를 사용 하 여 tooyour PostgreSQL 서버를 연결 하는 방법을 보여 줍니다. 사용 하 여 hello `root.crt` 만든 파일 및 hello `sslmode=verify-ca` 또는 `sslmode=verify-full` 옵션입니다.

Hello PostgreSQL 명령줄 인터페이스를 사용 하 여 hello 다음 명령을 실행 합니다.
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
성공 하면 다음 출력 hello를 나타납니다.
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a>pgAdmin GUI 도구 사용
Tooset hello SSL을 통해 안전 하 게 pgAdmin 4 tooconnect를 구성 하려면 `SSL mode = Verify-CA` 또는 `SSL mode = Verify-Full` 다음과 같습니다.

![pgAdmin - 연결 - SSL 모드 Require 스크린샷](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a>다음 단계
[용 Azure 데이터베이스를 위한 연결 라이브러리](concepts-connection-libraries.md) 후에 다양한 응용 프로그램 연결 옵션 검토
