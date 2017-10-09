---
title: "OMS 로그 분석의 Linux 응용 프로그램 성능 aaaCollect | Microsoft Docs"
description: "이 문서 Apache HTTP Server 및 MySQL에 대 한 Linux toocollect 성능 카운터에 대 한 hello OMS 에이전트를 구성 하는 세부 정보를 제공 합니다."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 51105c6add5c7941a004570a76a4d94c02fc8a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a>Log Analytics에서 Linux 응용 프로그램에 대한 성능 카운터 수집 
이 문서에서는 hello 구성에 대 한 세부 정보를 제공 [Linux 용 OMS 에이전트](https://github.com/Microsoft/OMS-Agent-for-Linux) 특정 응용 프로그램에 대 한 toocollect 성능 카운터입니다.  이 문서에 포함 하는 hello 응용 프로그램은:  

- [MySQL](#MySQL)
- [Apache HTTP 서버](#apache-http-server)

## <a name="mysql"></a>MySQL
Hello OMS 에이전트를 설치할 때 hello 컴퓨터에서 MySQL Server 또는 MariaDB 서버가 검색 되 면 한 성능 모니터링 공급자 MySQL Server에 대 한 자동으로 설치 됩니다. 이 공급자는 toohello 로컬 MySQL/MariaDB 서버 tooexpose 성능 통계를 연결합니다. MySQL 사용자 자격 증명 hello 공급자 액세스할 수 있도록 MySQL 서버 hello 구성 되어야 합니다.

### <a name="configure-mysql-credentials"></a>MySQL 자격 증명 구성
hello MySQL OMI 공급자는 미리 구성 된 MySQL 사용자가 수행 해야 하 고 MySQL 클라이언트 라이브러리가 순서 tooquery hello 성능 및 상태 정보 hello MySQL 인스턴스를 설치 합니다.  이러한 자격 증명 hello Linux 에이전트에 저장 되는 인증 파일에 저장 됩니다.  hello 인증 파일에 바인딩 주소 지정 하 고 포트 hello MySQL 인스턴스가 수신 중인 toouse toogather 메트릭을 자격 증명.  

MySQL OMI Linux hello에 대 한 hello OMS 에이전트를 설치 하는 동안 공급자가 바인딩 주소 및 포트와 집합 hello MySQL OMI 인증 파일을 부분적으로 한 MySQL my.cnf 구성 파일 (기본 위치)을 검사 합니다.

hello MySQL 인증 파일에 저장 된 `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`합니다.


### <a name="authentication-file-format"></a>인증 파일 형식
다음은 hello MySQL OMI 인증 파일에 대 한 hello 형식

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

다음 표에 hello hello 인증 파일의 hello 항목을 설명 합니다.

| 속성 | 설명 |
|:--|:--|
| 포트 | Hello 현재 포트 hello를 MySQL 인스턴스가 수신 중인를 나타냅니다. 포트 0 다음 hello 속성이 기본 인스턴스에 대해 사용 되도록 지정 합니다. |
| 바인딩 주소| 현재 MySQL 바인딩-주소입니다. |
| username| MySQL 사용자 toouse toomonitor hello MySQL server 인스턴스를 사용 합니다. |
| Base64로 인코딩된 암호| Base 64로 인코드된 hello MySQL 모니터링 사용자의 암호입니다. |
| AutoUpdate| 에 대 한 toorescan hello my.cnf 파일에서 변경 되는지 여부를 지정 하 고 hello MySQL OMI 공급자가 업그레이드 hello MySQL OMI 인증 파일을 덮어씁니다. |

### <a name="default-instance"></a>기본 인스턴스
기본 인스턴스 및 보다 쉽게 한 Linux 호스트에서 여러 MySQL 인스턴스를 관리 하는 포트 번호 toomake hello MySQL OMI 인증 파일 정의할 수 있습니다.  hello 기본 인스턴스가 포트 0 인스턴스에 의해 표시 됩니다. 모든 추가 인스턴스는 서로 다른 값을 지정 하지 않은 경우 hello 기본 인스턴스에서 설정 하는 속성을 상속 합니다. 예를 들어 포트 '3308'에서 수신 대기 중인 MySQL 인스턴스가 추가 되 면 hello 기본 인스턴스의 바인딩 주소, username 및 password Base64 인코딩 tootry 사용된 되며 3308에서 수신 대기 하는 hello 인스턴스를 모니터링 합니다. 사용 하 여 3308 hello 인스턴스가 바인딩된 tooanother 주소인 경우 hello 동일한 MySQL 사용자 이름 및 암호 쌍만 hello 바인딩 주소의 필요 정도와 hello 다른 속성은 상속 됩니다.

다음 표에 hello에 인스턴스 설정 예 

| 설명 | 파일 |
|:--|:--|
| 기본 인스턴스 및 포트 3308의 인스턴스입니다. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| 기본 인스턴스 및 포트 3308의 인스턴스, 다른 사용자 이름 및 암호입니다. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a>MySQL OMI 인증 파일 프로그램
에 포함 되어 hello 설치 hello MySQL OMI 공급자 MySQL OMI 인증 파일 프로그램 사용된 tooedit hello MySQL OMI 인증 파일 일 수 있습니다. hello 인증 파일 프로그램 hello 수정할 수 있는 위치에서 찾을 수 있습니다.

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> hello 자격 증명 파일 hello omsagent 계정이 읽을 수 있어야 합니다. 로 hello mycimprovauth 명령을 실행 하는 것이 좋습니다.

hello 다음 표에서 자세히 설명 hello 구문 mycimprovauth 사용에 대 한 합니다.

| 작업 | 예제 | 설명
|:--|:--|:--|
| autoupdate *false\|true* | mycimprovauth autoupdate false | 여부 hello 인증 파일은 자동으로 업데이트 하는 집합에 다시 시작 하거나 업데이트 합니다. |
| default *bind-address username password* | mycimprovauth default 127.0.0.1 root pwd | 집합 hello hello MySQL OMI 인증 파일의에서 기본 인스턴스.<br>일반 텍스트에 hello 암호 필드를 입력할 수-hello MySQL OMI 인증 파일에에서 hello 암호 Base 64로 인코딩된 됩니다. |
| delete *default\|port_num* | mycimprovauth 3308 | 중 하나가 기본적으로 또는 포트 번호로 hello 지정 된 인스턴스를 삭제합니다. |
| help | mycimprov help | 명령 toouse 목록 인쇄 합니다. |
| print | mycimprov print | MySQL OMI 인증 파일 프로그램 쉽게 tooread 인쇄 합니다. |
| update port_num *bind-address username password* | mycimprov update 3307 127.0.0.1 root pwd | Hello 지정 된 인스턴스를 업데이트 하거나 존재 하지 않는 경우 hello 인스턴스를 추가 합니다. |

hello 다음 예제 명령은 hello MySQL server에 대 한 기본 사용자 계정을 localhost에 정의 합니다.  일반 텍스트에 hello 암호 필드를 입력할 수-hello MySQL OMI 인증 파일에에서 hello 암호 Base 64로 인코딩된 됩니다.

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a>MySQL 성능 카운터에 필요한 데이터베이스 권한
MySQL 사용자 hello 쿼리 toocollect MySQL Server 성능 데이터를 다음 액세스 toohello가 필요 합니다. 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


hello MySQL 사용자에 대 한 SELECT 권한도 toohello 다음 기본 표 필요 합니다.

- information_schema
- mysql. 

Hello 다음 grant 명령을 실행 하 여 이러한 권한은 부여할 수 있습니다.

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> toogrant 권한 tooa 부여할 hello 권한 뿐만 아니라 ' GRANT option ' hello MySQL 모니터링 사용자 권한을 부여 하는 사용자 hello 있어야 합니다.

### <a name="define-performance-counters"></a>성능 카운터 정의

Linux toosend 데이터 tooLog 분석에 대 한 hello OMS 에이전트를 구성 하 고 나면 hello 성능 카운터 toocollect를 구성 해야 합니다.  hello 절차를 사용 하 여 [로그 분석에서 Windows 및 Linux 성능 데이터 원본](log-analytics-data-sources-windows-events.md) 다음 표에 hello에 hello 카운터와 함께 합니다.

| 개체 이름 | 카운터 이름 |
|:--|:--|
| MySQL 데이터베이스 | 디스크 공간(바이트) |
| MySQL 데이터베이스 | 테이블 |
| MySQL Server | 중단된 연결 Pct |
| MySQL Server | 연결 사용 Pct |
| MySQL Server | 디스크 공간 사용(바이트) |
| MySQL Server | 전체 테이블 검색 Pct |
| MySQL Server | InnoDB 버퍼 풀 적중 Pct |
| MySQL Server | InnoDB 버퍼 풀 사용 Pct |
| MySQL Server | InnoDB 버퍼 풀 사용 Pct |
| MySQL Server | 키 캐시 적중 Pct |
| MySQL Server | 키 캐시 사용 Pct |
| MySQL Server | 키 캐시 쓰기 Pct |
| MySQL Server | 쿼리 캐시 적중 Pct |
| MySQL Server | 쿼리 캐시 잘라내기 Pct |
| MySQL Server | 쿼리 캐시 사용 Pct |
| MySQL Server | 테이블 캐시 적중 Pct |
| MySQL Server | 테이블 캐시 사용 Pct |
| MySQL Server | 테이블 잠금 경합 Pct |

## <a name="apache-http-server"></a>Apache HTTP 서버 
Apache HTTP Server hello omsagent 번들을 설치할 때 hello 컴퓨터에서 검색 되 면 한 성능 모니터링 공급자 Apache HTTP Server에 대 한 자동으로 설치 됩니다. 이 공급자는 순서 tooaccess 성능 데이터에 hello Apache HTTP Server에 로드 해야 하는 Apache 모듈을 사용 합니다. 다음 명령을 hello로 hello 모듈을 로드할 수 있습니다.
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache 모니터링 모듈을 hello 다음 명령을 실행 합니다.
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a>성능 카운터 정의

Linux toosend 데이터 tooLog 분석에 대 한 hello OMS 에이전트를 구성 하 고 나면 hello 성능 카운터 toocollect를 구성 해야 합니다.  hello 절차를 사용 하 여 [로그 분석에서 Windows 및 Linux 성능 데이터 원본](log-analytics-data-sources-windows-events.md) 다음 표에 hello에 hello 카운터와 함께 합니다.

| 개체 이름 | 카운터 이름 |
|:--|:--|
| Apache HTTP 서버 | 근무 중인 작업자 |
| Apache HTTP 서버 | 유휴 작업자 |
| Apache HTTP 서버 | Pct 근무 중인 작업자 |
| Apache HTTP 서버 | 총 Pct CPU |
| Apache 가상 호스트 | 분당 오류 - 클라이언트 |
| Apache 가상 호스트 | 분당 오류 - 서버 |
| Apache 가상 호스트 | 요청당 KB |
| Apache 가상 호스트 | 초당 요청 KB |
| Apache 가상 호스트 | 초당 요청 |



## <a name="next-steps"></a>다음 단계
* Linux 에이전트에서 [성능 카운터를 수집합니다](log-analytics-data-sources-performance-counters.md).
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다. 
