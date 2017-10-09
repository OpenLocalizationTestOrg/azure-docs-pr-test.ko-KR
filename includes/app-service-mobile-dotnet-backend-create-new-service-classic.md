1. Hello에 로그인 [Azure 포털]합니다.
2. **+새로 만들기** > **웹 + 모바일** > **모바일 앱**을 클릭한 다음 모바일 앱 백 엔드에 대한 이름을 제공합니다.
3. Hello에 대 한 **리소스 그룹**기존 리소스 그룹을 선택 하거나 새로 만듭니다 (앱 이름이 같은 hello를 사용 하 여.) 
   
    다른 앱 서비스 계획을 선택하거나 새 앱 서비스 계획을 만들 수 있습니다. 앱 서비스 계획 및 toocreate 새 계획에 다른 가격 책정 계층 하 고 원하는 위치에서 참조 하는 방법에 대 한 자세한 [Azure 앱 서비스 계획 심도 깊은 개요](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다.
4. Hello에 대 한 **앱 서비스 계획**, hello 기본 계획 (hello에 [표준 계층](https://azure.microsoft.com/pricing/details/app-service/))을 선택 합니다. 또한 다른 계획을 선택하거나 [새 계획을 만들 수 있습니다](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). hello 앱 서비스 계획의 설정에 따라 결정 hello [위치, 기능, 비용 및 계산 리소스](https://azure.microsoft.com/pricing/details/app-service/) 연결 된 앱입니다. 
   
    Hello 계획을 결정 한 다음 클릭 **만들기**합니다. Hello 모바일 앱 백 엔드를 만듭니다. 
5. Hello에 **설정** 블레이드 새로운 모바일 앱 백 hello에 대 한 클릭 **퀵 스타트** > 클라이언트 응용 프로그램 플랫폼 > **데이터베이스 연결**합니다. 
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-data-connection.png)
6. Hello에 **데이터 연결 추가** 블레이드에서 클릭 **SQL 데이터베이스** > **새 데이터베이스를 만들**, hello 데이터베이스가 **이름**, 가격 책정 계층을 선택한 다음 클릭 **서버**합니다.  이 새 데이터베이스를 다시 사용할 수 있습니다. Hello에 데이터베이스를 이미 만든 경우 같은 위치를 선택할 수 있습니다 대신 **기존 데이터베이스를 사용 하 여**합니다. 데이터베이스를 다른 위치에서 사용 하 여 hello 기한 toobandwidth 비용 및 긴 대기 시간이 권장 되지 않습니다.
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-db.png)
7. Hello에 **새 서버** 블레이드에서 hello에 고유한 서버 이름을 입력 **서버 이름** 필드에서 제공 된 로그인과 암호를 확인 **허용 azure 서비스 tooaccess 서버**를 클릭 하 고 **확인**합니다. Hello 새 데이터베이스를 만듭니다.
8. Hello에 다시 **데이터 연결 추가** 블레이드에서 클릭 **연결 문자열**프로그램 데이터베이스에 대 한 hello 로그인 및 암호 값을 입력 하 고 **확인**합니다. 계속 하기 전에 성공적으로 배포 된 hello 데이터베이스 toobe 몇 분 동안 기다립니다.

<!-- URLs. -->
[Azure 포털]: https://portal.azure.com/
