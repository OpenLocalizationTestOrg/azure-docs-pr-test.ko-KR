---
title: "aaaConnect tooAzure Ruby를 사용 하 여 PostgreSQL 데이터베이스 | Microsoft Docs"
description: "이 퀵 스타트의 tooconnect를 사용 하 고 PostgreSQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수 Ruby 코드 예제를 제공 합니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 06/30/2017
ms.openlocfilehash: 7a0c8c92023452b40ca19d76fa659744f3e9a236
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a>Azure 데이터베이스에 대 한 PostgreSQL: 사용 하 여 Ruby tooconnect 및 쿼리 데이터
이 빠른 시작에서는 방법을 tooconnect tooan Azure PostgreSQL 사용에 대 한 데이터베이스는 [Ruby](https://www.ruby-lang.org) 응용 프로그램입니다. Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다. 이 문서에서는 익숙한 Ruby를 사용 하 여 개발 하지만 새 tooworking PostgreSQL에 대 한 Azure 데이터베이스는 가정 합니다.

## <a name="prerequisites"></a>필수 조건
이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.
- [DB 만들기 - 포털](quickstart-create-server-database-portal.md)
- [DB 만들기 - Azure CLI](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a>Ruby 설치
사용자의 컴퓨터에 Ruby를 설치합니다. 

### <a name="windows"></a>Windows
- 다운로드 및 설치 최신 버전의 hello [Ruby](http://rubyinstaller.org/downloads/)합니다.
- Hello 마침 화면 hello MSI 설치 프로그램을 "실행 ridk 설치 tooinstall MSYS2 및 개발 도구 체인." hello 확인란 클릭 **마침** toolaunch hello 다음 설치 관리자입니다.
- hello RubyInstaller2에 대 한 Windows installer가 시작 됩니다. 2 tooinstall hello MSYS2 리포지토리 업데이트를 입력 합니다. 완료 되 고 toohello 설치 프롬프트 반환, 후 hello 명령 창을 닫습니다.
- Hello 시작 메뉴에서 새 명령 프롬프트 (cmd)를 시작 합니다.
- 테스트 hello Ruby 설치 `ruby -v` toosee hello 버전이 설치 되어 있습니다.
- Hello 보석 설치 테스트 `gem -v` toosee hello 버전이 설치 되어 있습니다.
- Hello PostgreSQL 모듈 보석을 사용 하 여 hello 명령을 실행 하 여 Ruby 용 빌드 `gem install pg`합니다.

### <a name="macos"></a>MacOS
- Homebrew를 사용 하 여 hello 명령을 실행 하 여 Ruby 설치 `brew install ruby`합니다. 자세한 설치 옵션에 대 한 참조 hello Ruby [설치 설명서](https://www.ruby-lang.org/en/documentation/installation/#homebrew)
- 테스트 hello Ruby 설치 `ruby -v` toosee hello 버전이 설치 되어 있습니다.
- Hello 보석 설치 테스트 `gem -v` toosee hello 버전이 설치 되어 있습니다.
- Hello PostgreSQL 모듈 보석을 사용 하 여 hello 명령을 실행 하 여 Ruby 용 빌드 `gem install pg`합니다.

### <a name="linux-ubuntu"></a>Linux(Ubuntu)
- Ruby hello 명령을 실행 하 여 설치 `sudo apt-get install ruby-full`합니다. 자세한 설치 옵션에 대 한 참조 hello Ruby [설치 설명서](https://www.ruby-lang.org/en/documentation/installation/)합니다.
- 테스트 hello Ruby 설치 `ruby -v` toosee hello 버전이 설치 되어 있습니다.
- Hello 명령을 실행 하 여 보석에 대 한 hello 최신 업데이트를 설치 `sudo gem update --system`합니다.
- Hello 보석 설치 테스트 `gem -v` toosee hello 버전이 설치 되어 있습니다.
- Hello 명령을 실행 하 여 hello gcc, 작성, 및 기타 빌드 도구가 설치 `sudo apt-get install build-essential`합니다.
- Hello 명령을 실행 하 여 hello PostgreSQL 라이브러리 설치 `sudo apt-get install libpq-dev`합니다.
- 빌드 보석을 사용 하 여 hello 명령을 실행 하 여 hello Ruby pg 모듈 `sudo gem install pg`합니다.

## <a name="run-ruby-code"></a>Ruby 코드 실행 
- 텍스트 파일에 hello 코드를 저장 하 고 같은 파일 확장명이.rb와 프로젝트 폴더에 hello 파일을 저장 `C:\rubypostgres\read.rb` 또는`/home/username/rubypostgres/read.rb`
- toorun hello 코드 hello 명령 프롬프트를 시작 또는 bash 셸은 합니다. 프로젝트 폴더에 디렉터리를 변경 `cd rubypostgres`, hello 명령을 입력 `ruby read.rb` toorun hello 응용 프로그램입니다.

## <a name="get-connection-information"></a>연결 정보 가져오기
PostgreSQL를 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다. 정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 등 생성 한 hello 서버에 대 한 검색 **mypgserver 20170401**합니다.
3. Hello 서버 이름을 클릭 **mypgserver 20170401**합니다.
4. 선택 hello 서버 **개요** 페이지. Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.
 ![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-ruby/1-connection-string.png)
5. 서버 로그인 정보를 잊은 경우 탐색 toohello **개요** 페이지 tooview hello 서버 관리자 로그인 이름입니다. 필요한 경우 hello 암호를 재설정 합니다.

## <a name="connect-and-create-a-table"></a>테이블 연결 및 생성
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 테이블을 만들 **CREATE TABLE** SQL 문 다음에 **INSERT INTO** hello 테이블에 SQL 문 tooadd 행입니다.

hello 코드 사용 하 여 한 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 생성자와 함께 개체 [new ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 데이터베이스. 메서드를 호출 하는 다음 [exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello 놓기, CREATE TABLE 및 INSERT INTO 명령입니다. hello 코드 확인 hello를 사용 하 여 오류에 대 한 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 클래스입니다. 메서드를 호출 하는 다음 [close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 종료 하기 전에 tooclose hello 연결 합니다.

Hello 대체 `host`, `database`, `user`, 및 `password` 고유한 값이 포함 된 문자열입니다. 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a>데이터 읽기
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다. 

hello 코드 사용 하 여 한 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 생성자와 함께 개체 [new ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 데이터베이스. 메서드를 호출 하는 다음 [exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT 명령의 경우 결과 집합의 hello 결과 유지 합니다. hello 결과 집합 컬렉션을 반복 hello를 사용 하 여 위에 `resultSet.each do` hello에 hello 현재 행 값을 유지 하는 루프 `row` 변수입니다. hello 코드 확인 hello를 사용 하 여 오류에 대 한 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 클래스입니다. 메서드를 호출 하는 다음 [close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 종료 하기 전에 tooclose hello 연결 합니다.

Hello 대체 `host`, `database`, `user`, 및 `password` 고유한 값이 포함 된 문자열입니다. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a>데이터 업데이트
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 업데이트는 **업데이트** SQL 문입니다.

hello 코드 사용 하 여 한 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 생성자와 함께 개체 [new ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 데이터베이스. 메서드를 호출 하는 다음 [exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE 명령입니다. hello 코드 확인 hello를 사용 하 여 오류에 대 한 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 클래스입니다. 메서드를 호출 하는 다음 [close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 종료 하기 전에 tooclose hello 연결 합니다.

Hello 대체 `host`, `database`, `user`, 및 `password` 고유한 값이 포함 된 문자열입니다. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a>데이터 삭제
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다. 

hello 코드 사용 하 여 한 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 생성자와 함께 개체 [new ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL 데이터베이스. 메서드를 호출 하는 다음 [exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE 명령입니다. hello 코드 확인 hello를 사용 하 여 오류에 대 한 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 클래스입니다. 메서드를 호출 하는 다음 [close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 종료 하기 전에 tooclose hello 연결 합니다.

Hello 대체 `host`, `database`, `user`, 및 `password` 고유한 값이 포함 된 문자열입니다. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a>다음 단계
> [!div class="nextstepaction"]
> [내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션](./howto-migrate-using-export-and-import.md)
