### <a name="prerequisites"></a>필수 조건
* Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)
* [Azure SQL 데이터베이스](../articles/sql-database/sql-database-get-started.md) 비롯 한 hello 서버 이름, 데이터베이스 이름 및 사용자 이름/암호의 연결 정보를 포함 합니다. 이 정보는 hello SQL 데이터베이스 연결 문자열에에서 포함 됩니다.
  
    Server=tcp:*yoursqlservername*.database.windows.net,1433;Initial Catalog=*yourqldbname*;Persist Security Info=False;User ID={your_username};Password={your_password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
  
    [Azure SQL Databases](https://azure.microsoft.com/services/sql-database)에 대해 자세히 알아봅니다.

> [!NOTE]
> Azure SQL 데이터베이스를 만들 때 SQL에 포함 된 hello 예제 데이터베이스를 만들 수도 있습니다. 
> 
> 

논리 앱을 통해 Azure SQL 데이터베이스를 사용 하기 전에 tooyour SQL 데이터베이스를 연결 합니다. Hello Azure 포털에서 논리 앱 내에서이 작업을 쉽게 수행할 수 있습니다.  

Tooyour 단계를 수행 하는 hello를 사용 하 여 Azure SQL 데이터베이스를 연결 합니다.  

1. 논리 앱을 만듭니다. Hello 논리 앱 디자이너에서 트리거를 추가 하 고 작업을 추가 합니다. 선택 **표시 Microsoft 관리 되는 Api** hello에 드롭다운 목록에서 선택한 다음 hello 검색 상자에 "sql"을 입력 합니다. Hello 작업 중 하나를 선택 합니다.  
   
    ![SQL Azure 연결 만들기 단계](./media/connectors-create-api-sqlazure/sql-actions.png)
2. 모든 연결 tooSQL 데이터베이스를 이전에 만든 하지 않은 hello 연결 세부 정보에 대 한 메시지가 표시 됩니다.  
   
    ![SQL Azure 연결 만들기 단계](./media/connectors-create-api-sqlazure/connection-details.png) 
3. Hello SQL 데이터베이스 세부 정보를 입력 합니다. 별표가 있는 속성은 필수 사항입니다.
   
   | 속성 | 세부 정보 |
   | --- | --- |
   | 게이트웨이를 통해 연결 |선택 취소된 상태로 둡니다. 이 때 tooan 연결 온-프레미스 SQL Server에 사용 됩니다. |
   | 연결 이름 * |연결의 이름을 입력합니다. |
   | SQL Server 이름 * |Hello 서버 이름을; 입력 이 같은 *servername.database.windows.net 인*합니다. hello 서버 이름이 hello Azure 포털의에서 hello SQL 데이터베이스 속성에 표시 하 고 hello 연결 문자열에도 표시 됩니다. |
   | SQL 데이터베이스 이름 * |SQL 데이터베이스에 지정한 hello 이름을 입력 합니다. 이 테이블은 표시 hello SQL 데이터베이스 속성에서 hello 연결 문자열: 초기 카탈로그 =*yoursqldbname*합니다. |
   | 사용자 이름 * |Hello SQL 데이터베이스를 만들 때 만든 hello 사용자 이름을 입력 합니다. 이 hello Azure 포털의에서 hello SQL 데이터베이스 속성에 나열 됩니다. |
   | 암호 * |Hello SQL 데이터베이스를 만들 때 만든 hello 암호를 입력 합니다. |
   
    이러한 자격 증명 사용 되는 tooauthorize 여 논리 앱 tooconnect 되며 SQL 데이터에 액세스 합니다. 완료 되 면 연결 정보가 비슷한 toohello 다음을 확인 합니다.  
   
    ![SQL Azure 연결 만들기 단계](./media/connectors-create-api-sqlazure/sample-connection.png) 
4. **만들기**를 선택합니다. 
5. 공지 hello 연결이 만들어졌습니다. 이제 진행할 논리 앱의 단계를 다른 hello: 
   
    ![SQL Azure 연결 만들기 단계](./media/connectors-create-api-sqlazure/table.png)

