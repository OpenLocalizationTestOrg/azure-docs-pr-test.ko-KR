### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a>Hello Azure 포털에서에서 새 논리 SQL server 만들기

1. **새로 만들기**를 클릭하고 **논리 서버**를 검색한 다음 **Enter** 키를 누릅니다.

    ![논리 서버 검색](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. **SQL 서버(논리 서버)**를 선택합니다. 

    ![논리 서버 선택](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. 클릭 **만들기** tooopen hello 새 SQL Server (논리 서버) 블레이드입니다.

   <kbd>![논리 서버 블레이드를 여세요](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![논리 서버 블레이드](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd>
  
3. Hello SQL Server (논리 서버) 블레이드에서 서버 이름 텍스트 상자에 새 논리 서버 hello에 대 한 올바른 이름을 지정 합니다. 녹색 확인 표시가 유효한 이름을 제공한 것을 나타냅니다.
    
    ![새 서버 이름](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > hello 새 서버의 정규화 된 이름이 됩니다 < your_server_name >. database.windows.net 합니다.
    >
    
4. Hello 서버 관리자 로그인 텍스트 상자에이 서버에 대 한 hello SQL 인증 로그인에 대 한 사용자 이름을 입력 합니다. 이 로그인을 서버 보안 주체 로그인 hello 라고 합니다. 녹색 확인 표시가 유효한 이름을 제공한 것을 나타냅니다.
    
    ![SQL 관리자 로그인](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. Hello에 **암호** 및 **암호 확인** 텍스트 상자 hello 서버 보안 주체 로그인 계정의 암호를 제공 합니다. 녹색 확인 표시가 유효한 암호를 제공한 것을 나타냅니다.
    
    ![SQL 관리자 암호](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. 사용 권한 toocreate 개체에 구독을 선택 합니다.

    ![subscription](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. Hello 리소스 그룹 텍스트 상자에서 선택 **새로 만들기** 다음 hello 리소스 그룹 텍스트 상자에 hello (있습니다 에서도 사용할 수 있는 기존 리소스 그룹 이미 만든 경우 자신에 대 한 하나)는 새 리소스 그룹에 대 한 올바른 이름을 제공 합니다. 녹색 확인 표시가 유효한 이름을 제공한 것을 나타냅니다.

    ![새 리소스 그룹](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. Hello에 **위치** 텍스트 상자를 선택한 데이터 센터 "오스트레일리아 동부"와 같은 적절 한 tooyour 위치-합니다.
    
    ![서버 위치](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > 에 대 한 확인란 hello **허용 azure 서비스 tooaccess 서버** 이 블레이드를 변경할 수 없습니다. Hello 서버 방화벽 블레이드에서이 설정을 변경할 수 있습니다. 자세한 내용은 [보안 시작](../articles/sql-database/sql-database-manage-servers-portal.md)을 참조하세요.
    >
    
9. **만들기**를 클릭합니다.

    ![만들기 단추](./media/sql-data-warehouse-create-logical-server/create.png)

