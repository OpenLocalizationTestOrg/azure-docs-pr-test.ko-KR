---
title: "Linux VM의 PostgreSQL aaaSet | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall PostgreSQL Azure에서 Linux 가상 컴퓨터 구성"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a>Azure에서 PostgreSQL 설치 및 구성
PostgreSQL는 고급 오픈 소스 데이터베이스와 비슷한 tooOracle 및 DB2, 전체 ACID 규정 준수, 신뢰할 수 있는 트랜잭션 처리 및 다중 버전 동시성 제어와 같은 엔터프라이즈 기능이 포함됩니다. 또한 ANSI SQL 및 SQL/MED(Oracle, MySQL, MongoDB 등에 대한 외부 데이터 래퍼 포함)와 같은 표준을 지원합니다. 12개 이상의 프로시저 언어, GIN 및 GiST 인덱스, 공간 데이터 지원 및 JSON에 대한 여러 NoSQL 같은 기능 또는 키 값 기반 응용 프로그램에 대한 지원을 통해 확장성을 높일 수 있습니다.

이 문서에 설명 합니다 방법을 tooinstall PostgreSQL Linux를 실행 하는 Azure 가상 컴퓨터에 구성 합니다.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a>PostgreSQL 설치
> [!NOTE]
> 이 자습서에서 순서 toocomplete Linux를 실행 하는 Azure 가상 컴퓨터를 이미 있어야 합니다. 계속 하기 전에 Linux VM을 집합과 toocreate 참조는 [Azure Linux VM 자습서](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
> 
> 

이 경우 hello PostgreSQL 포트와 포트 1999를 사용 합니다.  

Toohello PuTTY를 통해 만든 Linux VM을 연결 합니다. 인 경우 hello Azure Linux VM을 사용 하는 처음으로 참조 [어떻게 tooUse와 Azure에서 Linux에 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toouse PuTTY 어떻게 toolearn tooconnect tooa Linux VM입니다.

1. Hello 명령 tooswitch toohello 루트 (관리자) 다음을 실행 합니다.
   
        # sudo su -
2. 일부 배포의 경우 PostgreSQL을 설치하기 전에 설치해야 하는 종속성이 있습니다. 이 목록에 프로그램 배포판에 대 한 확인 하 고 hello 적절 한 명령을 실행 합니다.
   
   * Red Hat 기반 Linux:
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * Debian 기반 Linux:
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * SUSE Linux:
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. Hello 루트 디렉터리에 PostgreSQL를 다운로드 하 여 다음의 hello 패키지 압축을 풉니다.
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    위의 hello 예입니다. Hello를 찾을 수 있습니다 hello에 주소를 다운로드 하는 자세한 내용은 [/pub/소스 / 인덱스](https://ftp.postgresql.org/pub/source/)합니다.
4. 이러한 명령을 실행 toostart hello 빌드:
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. 원하는 toobuild hello 설명서 (HTML 및 매뉴얼 페이지) 및 추가 모듈 (contrib)를 포함 하 여 작성 될 수 있는 모든 작업 하는 경우 다음 명령을 대신 hello를 실행 합니다.
   
        # gmake install-world
   
    확인 메시지를 수행 하는 hello을 받게 됩니다.
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a>PostgreSQL 구성
1. (선택 사항) 기호화 된 링크 tooshorten hello PostgreSQL 참조 만들기 toonot hello 버전 번호를 포함 합니다.
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. Hello 데이터베이스에 대 한 디렉터리를 만듭니다.
   
        # mkdir -p /opt/pgsql_data
3. 루트가 아닌 사용자를 만들고 해당 사용자의 프로필을 수정합니다. 그런 다음 toothis 새 사용자를 전환 (호출 *postgres* 예에서):
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > 보안상의 이유로 PostgreSQL 루트가 아닌 사용자 tooinitialize 사용 하 여, 시작 또는 hello 데이터베이스를 종료 합니다.
   > 
   > 
4. Hello 편집 *bash_profile* 아래 hello 명령을 입력 하 여 파일입니다. 이 줄을 추가할 hello toohello 끝 *bash_profile* 파일:
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. Hello 실행 *bash_profile* 파일:
   
        $ source .bash_profile
6. 다음 명령을 hello를 사용 하 여 설치 유효성 검사:
   
        $ which psql
   
    설치에 성공한 경우 hello 응답을 따라 표시 됩니다.
   
        /opt/pgsql/bin/psql
7. 또한 hello PostgreSQL 버전을 확인할 수 있습니다.
   
        $ psql -V
8. Hello 데이터베이스를 초기화 합니다.
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    Hello 다음 출력을 받게 됩니다.

![이미지](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a>PostgreSQL 설정
<!--    [postgres@ test ~]$ exit -->

Hello 다음 명령을 실행 합니다.

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

Hello /etc/init.d/postgresql 파일에 있는 두 개의 변수를 수정 합니다. PostgreSQL의 toohello 설치 경로 설정 하는 hello 접두사는: **/옵트인/pgsql**합니다. PGDATA PostgreSQL의 toohello 데이터 저장소 경로 설정 되어: **/옵트인/pgsql_data**합니다.

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![이미지](./media/postgresql-install/no2.png)

Hello 파일 toomake 변경 것 실행:

    # chmod +x /etc/init.d/postgresql

PostgreSQL을 시작합니다.

    # /etc/init.d/postgresql start

PostgreSQL의 hello 끝점 켜져 있는지 확인 합니다.

    # netstat -tunlp|grep 1999

다음 출력 hello를 표시 되어야 합니다.

![이미지](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a>Toohello Postgres 데이터베이스 연결
다시 한 번 toohello postgres 사용자를 전환 합니다.

    # su - postgres

Postgres 데이터베이스를 만듭니다.

    $ createdb events

방금 만든 toohello 이벤트 데이터베이스를 연결 합니다.

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a>Postgres 테이블 만들기 및 삭제
Toohello 데이터베이스에 연결 했으므로 했으므로에 테이블을 만들 수 있습니다.

예를 들어 다음 명령을 hello를 사용 하 여 새 예제 Postgres 테이블을 만듭니다.

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

이제 hello로 네 열 테이블을 설정한 다음 열 이름 및 제한 사항:

1. hello 열 "name" 제한 된 hello VARCHAR 명령 toobe 하 여 아래에서 20 자입니다.
2. hello "식량" 열 각자 중인 hello 음식 항목을 나타냅니다. VARCHAR 30 자에서이 텍스트 toobe를 제한합니다.
3. hello "확인" 열 레코드 hello 사람 toohello 집들이 주최가 여부. hello 허용 되는 값은 "Y" 및 "N"입니다.
4. hello 이벤트에 대 한 등록 hello "date" 열 보여 줍니다. Postgres에서는 날짜가 yyyy-mm-dd로 작성되도록 요구합니다.

Hello 다음 테이블에 성공적으로 생성 된 경우 표시 됩니다.

![이미지](./media/postgresql-install/no4.png)

또한 다음 명령을 hello를 사용 하 여 hello 테이블 구조를 확인할 수 있습니다.

![이미지](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a>데이터 tooa 테이블 추가
먼저, 행에 정보를 삽입합니다.

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

다음 출력이 표시됩니다.

![이미지](./media/postgresql-install/no6.png)

몇 가지 더 많은 사람들이 toohello 테이블도 추가할 수 있습니다. 다음은 몇 가지 옵션입니다. 또는 직접 만들 수도 있습니다.

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a>테이블 표시
다음 명령 tooshow 테이블 hello를 사용 합니다.

    select * from potluck;

hello 출력이 생성 됩니다.

![이미지](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a>테이블의 데이터 삭제
다음 명령은 toodelete 테이블의에서 데이터를 사용 하 여 hello:

    delete from potluck where name=’John’;

Hello "John" 행에 있는 모든 hello 정보를 삭제합니다. hello 출력이 생성 됩니다.

![이미지](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a>테이블의 데이터 업데이트
같은 테이블의 명령 tooupdate 데이터가 hello를 사용 합니다. 이 하나에 대 한 Sandy가 확인 그녀이 참석은 하므로 "n" 그녀의 RSVP 너무 변경 합니다 "Y":

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a>PostgreSQL에 대한 자세한 정보 얻기
Azure Linux VM에서 PostgreSQL hello 설치를 완료 했으므로 Azure에서 사용 하 여 즐길 수 있습니다. PostgreSQL에 대 한 자세한 toolearn 방문 hello [PostgreSQL 웹 사이트](http://www.postgresql.org/)합니다.

