
1. Hello 클릭 **응용 프로그램 서비스** 단추 백 엔드 모바일 앱을 선택 **퀵 스타트**, 한 다음 클라이언트 플랫폼 (iOS, Android, Xamarin, Cordova)를 선택 합니다.

    ![Mobile Apps 빠른 시작이 강조 표시된 Azure Portal][quickstart]

2. 데이터베이스 연결 구성 되지 않은 경우 hello 다음을 수행 하 여 새로 만듭니다.

    ![Azure 포털과 toodatabase 모바일 앱 연결][connect]

    a. 새 SQL Database 및 서버를 만듭니다.

    ![Mobile Apps가 있는 Azure Portal 새 데이터베이스 및 서버 만들기][server]

    b. Hello 데이터 연결을 성공적으로 만들 때까지 기다립니다.

    ![데이터 연결을 성공적으로 만들는 경우 Azure Portal 알림][notification]

    c. 데이터 연결이 성공해야 합니다.

    ![Azure Portal 알림, "이미 데이터가 연결되었습니다."][already-connection]

3. **2. 테이블 API 만들기** 아래에서 **백 엔드 언어**를 Node.js로 선택합니다. 
 
4. Hello 승인에 동의 하 고 다음 선택 **만들 TodoItem 테이블**합니다.  
    이 작업을 통해 데이터베이스의 테이블에 새 할 일 목록을 만듭니다. 

    >[!IMPORTANT]
    > 기존 백 엔드 tooNode.js 전환 모든 내용을 덮어씁니다. .NET 백 엔드 대신 참조 toocreate [모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK와 함께 작동][instructions]합니다.

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
