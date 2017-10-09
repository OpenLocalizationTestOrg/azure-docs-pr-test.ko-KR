이러한 단계 tooinstall 따르고 MongoDB Windows Server를 실행 하는 가상 컴퓨터에서 실행 합니다.

> [!IMPORTANT]
> 인증 및 IP 주소 바인딩과 같은 MongoDB 보안 기능은 기본적으로 사용하도록 설정되어 있지 않습니다. MongoDB tooa 프로덕션 환경에 배포 하기 전에 보안 기능을 활성화 되어야 합니다.  자세한 내용은 [보안 및 인증](http://www.mongodb.org/display/DOCS/Security+and+Authentication)을 참조하세요.
>
>

1. 원격 데스크톱을 사용 하 여 toohello 가상 컴퓨터를 연결한 후 hello에서 Internet Explorer를 열고 **시작** hello 가상 컴퓨터에 대 한 메뉴입니다.
2. 선택 hello **도구** hello 오른쪽 위 모퉁이의 단추입니다.  **인터넷 옵션**선택, hello **보안** 탭을 선택한 후 hello **신뢰할 수 있는 사이트** 아이콘을 마지막으로 hello를 클릭 하 고 **사이트** 단추입니다. 추가 *https://\*. mongodb.org* toohello 신뢰할 수 있는 사이트 목록입니다.
3. 너무 이동[다운로드-MongoDB](https://www.mongodb.com/download-center#community)합니다.
4. Hello **현재 안정판** 의 **Community 서버**선택, 최신 hello **64 비트** hello Windows 열에는 버전입니다. 를 다운로드 한 다음 hello MSI 설치 관리자를 실행 합니다.
5. 일반적으로 MongoDB는 C:\Program Files\MongoDB에 설치됩니다. Hello 바탕 화면에서 환경 변수를 검색 하 고 hello MongoDB 이진 파일 경로 toohello 경로 변수를 추가 합니다. 예를 들어 컴퓨터에 C:\Program Files\MongoDB\Server\3.4\bin에 hello 이진 파일을 찾을 수 있습니다.
6. Hello 데이터 디스크의 MongoDB 데이터 및 로그 디렉터리를 만듭니다 (예: 드라이브 **f:**) hello 이전 단계에서에서 만든 합니다. **시작**선택, **명령 프롬프트** tooopen 명령 프롬프트 창 합니다.  형식:

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. toorun hello 데이터베이스를 실행 합니다.

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    모든 로그 메시지는 방향이 지정 된 toohello *F:\MongoLogs\mongolog.log* mongod.exe 서버 시작 및 preallocates 저널 파일의 파일입니다. Hello 저널 파일 MongoDB toopreallocate 분이 걸릴 하 고 연결에 대 한 수신을 시작할 수 있습니다. 명령 프롬프트 hello MongoDB 인스턴스가 실행 되는 동안이 작업에 초점을 맞추고 유지 됩니다.
8. toostart hello MongoDB 관리 셸을 열고 다른 명령 창에서 **시작** 형식 hello 명령에 따라:

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    hello 데이터베이스 hello 삽입을 통해 생성 됩니다.
9. 또는 mongod.exe를 서비스로 설치할 수 있습니다.

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    이렇게 하면 "Mongo DB"에 대한 설명이 포함된 MongoDB라는 서비스가 설치됩니다. hello `--logpath` hello 이후 서비스 실행에 없는 명령 창 toodisplay 출력, 옵션은 로그 파일을 사용 하는 toospecify 여야 합니다.  hello `--logappend` hello 서비스를 다시 시작 하면 출력 tooappend toohello 기존 로그 파일이 옵션을 지정 합니다.  hello `--dbpath` 옵션 hello 데이터 디렉터리의 hello 위치를 지정 합니다. 서비스 관련 명령줄 옵션에 대한 자세한 내용은 [서비스 관련 명령줄 옵션][MongoWindowsSvcOptions](영문)을 참조하세요.

    이 명령을 실행 toostart hello 서비스:

        C:\> net start MongoDB
10. MongoDB가 설치 되어 있고 실행 되 고 필요한 tooopen Windows 방화벽에서 포트를 원격으로 할 수 있도록 했으므로 tooMongoDB 연결 합니다.  Hello에서 **시작** 메뉴 선택 **관리 도구** 차례로 **고급 보안이 포함 된 Windows 방화벽**합니다.
11. a) hello 왼쪽된 창에서에서 선택 **인바운드 규칙**합니다.  Hello에 **동작** 창 오른쪽, hello에 선택 **새 규칙...** .

    ![Windows 방화벽][Image1]

    b)에서 hello **새 인바운드 규칙 마법사**선택, **포트** 클릭 하 고 **다음**합니다.

    ![Windows 방화벽][Image2]

    c) **TCP**를 선택한 후 **특정 로컬 포트**를 선택합니다.  "27017" (hello 기본 포트에서 수신 대기 MongoDB)의 포트를 지정 하 고 클릭 **다음**합니다.

    ![Windows 방화벽][Image3]

    d) 선택 **hello 연결 허용** 클릭 **다음**합니다.

    ![Windows 방화벽][Image4]

    e) 다시 **다음**을 클릭합니다.

    ![Windows 방화벽][Image5]

    f) "MongoPort"와 같은 hello 규칙의 이름을 지정 하 고 클릭 **마침**합니다.

    ![Windows 방화벽][Image6]

12. Hello 가상 컴퓨터를 만들 때 MongoDB에 대 한 끝점을 구성 하지 않은 지금 수행할 수 있습니다. Hello 방화벽 규칙 및 hello 끝점 toobe 수 tooconnect tooMongoDB 모두 원격으로 필요.

  Hello Azure 포털에서에서 클릭 **가상 컴퓨터 (클래식)**새 가상 컴퓨터의 hello 이름을 클릭 하 고 클릭 **끝점**합니다.

    ![끝점][Image7]

13. **추가**를 클릭합니다.

14. 프로토콜 "Mongo" 이름 가진 끝점을 추가 **TCP**, 둘 다 고 **공용** 및 **개인** 집합 포트 너무 "27017"입니다. 이 포트를 여 MongoDB toobe를 원격으로 액세스할 수 있습니다.

    ![끝점][Image9]

> [!NOTE]
> hello 27017 포트가 MongoDB 사용 하는 hello 기본 포트입니다. Hello를 지정 하 여이 기본 포트를 변경할 수 있습니다 `--port` hello mongod.exe 서버를 시작할 때 매개 변수입니다. 있는지 toogive hello 방화벽에서 동일한 포트 번호를 hello 및 hello hello 지침 앞에 "Mongo" 끝점을 확인 합니다.
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
