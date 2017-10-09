
1. 형식 tooescalate 권한:
   
        sudo -s
   
    암호를 입력합니다.
2. MySQL Community 서버 에디션 tooinstall 입력 합니다.
   
        zypper install mysql-community-server
   
    MySQL이 다운로드되어 설치될 때까지 기다립니다.
3. hello 시스템을 부팅할 때 tooset MySQL toostart, 유형:
   
        insserv mysql
4. 이 명령을 사용 하 여 hello MySQL 디먼 (mysqld)를 수동으로 시작 합니다.
   
        rcmysql start
   
    toocheck hello 상태 hello MySQL 데몬을 입력 합니다.
   
        rcmysql status
   
    toostop hello MySQL 데몬 입력 합니다.
   
        rcmysql stop
   
   > [!IMPORTANT]
   > 설치가 끝나면 hello MySQL 루트 암호는 기본적으로 비어 있습니다. MySQL 보안에 도움이 되는 **mysql\_secure\_installation** 스크립트를 실행하는 것이 좋습니다. hello 스크립트 묻는 toochange hello MySQL 루트 암호, 익명 사용자 계정을 제거, 원격 루트 로그인을 사용 하지 않도록 설정, 테스트 데이터베이스를 제거 및 hello 권한 테이블을 다시 로드 합니다. 이러한 옵션의 예 tooall 대답 hello 루트 암호를 변경 하는 것이 좋습니다.
   > 
   > 
5. 이 toorun hello 스크립트 MySQL 설치 스크립트를 입력 합니다.
   
        mysql_secure_installation
6. TooMySQL 로그인:
   
        mysql -u root -p
   
    Hello MySQL 루트 암호 (hello 이전 단계에서 변경 됨)을 입력 하 고 제공 됩니다는 메시지로 hello 데이터베이스와 SQL 문을 toointeract 실행할 수 있습니다.
7. hello에 hello 다음 실행 하는 새 MySQL 사용자 toocreate **mysql >** 프롬프트:
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Hello 세미콜론 (;)으로 설명 하면 hello의 hello 끝에 줄은 보류 된 hello 명령에 대 한 매우 중요 합니다.
8. 데이터베이스 및 부여 hello toocreate `mysqluser` 것 문제 hello 명령 다음에 대 한 사용자 권한을:
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    사용 되는 데이터베이스 사용자 이름 및 암호는 스크립트 toohello 데이터베이스를 연결 합니다.  데이터베이스 사용자 계정 이름은 반드시 hello 시스템에서 실제 사용자 계정을 나타내지는지 않습니다.
9. 다른 컴퓨터 종류에서에서에서 toolog:
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    여기서 `ip-address` tooMySQL 연결 될 있는 hello 컴퓨터의 hello IP 주소입니다.
10. tooexit hello MySQL 데이터베이스 관리 유틸리티를 입력 합니다.
    
        quit

## <a name="add-an-endpoint"></a>끝점 추가
1. MySQL 설치 된 후 원격 끝점 tooaccess MySQL tooconfigure가 필요 합니다. Toohello 로그인 [Azure 클래식 포털][AzurePortal]합니다. 클릭 **가상 컴퓨터**새 가상 컴퓨터의 hello 이름을 클릭 하 고 클릭 **끝점**합니다.
2. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
3. 끝점 프로토콜 "MySQL" 라는 추가 **TCP**, 및 **공용** 및 **개인** 포트 집합 너무 "3306" 합니다.
4. tooremotely는 컴퓨터 종류에서에서 toohello 가상 컴퓨터를 연결 합니다.
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    예를 들어이 자습서에서 만든 hello 가상 컴퓨터를 사용 하 여이 명령을 입력 합니다.
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
