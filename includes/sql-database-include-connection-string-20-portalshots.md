
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-hello-connection-string-from-hello-azure-portal"></a>Hello Azure 포털에서에서 hello 연결 문자열을 가져옵니다
사용 하 여 hello [Azure 포털](https://portal.azure.com/) 프로그램 클라이언트 프로그램 toointeract Azure SQL 데이터베이스에 대 한 필요한 tooobtain hello 연결 문자열: 

1. **찾아보기** > **SQL 데이터베이스**를 클릭합니다.
2. 데이터베이스의 이름을 hello hello 필터 텍스트 상자에 입력 hello 왼쪽 위 근처의 hello **SQL 데이터베이스** 블레이드입니다.
3. 데이터베이스에 대 한 hello 행을 클릭 합니다.
4. 데이터베이스에 대 한 hello 블레이드가 나타나면 편하게 클릭할 수 있는 표준 hello 컨트롤 toocollapse hello 블레이드 찾아보고 데이터베이스 필터링에 사용을 최소화 합니다. 
   
    ![데이터베이스 tooisolate 필터링][10-FilterDatabase]
5. 데이터베이스에 대 한 hello 블레이드에서 클릭 **데이터베이스 연결 문자열 표시**합니다.
6. Toouse hello ADO.NET 연결 라이브러리를 가져오려는 경우 레이블이 지정 된 hello 문자열을 복사 합니다. **ADO**합니다. 
   
    ![데이터베이스에 대 한 hello ADO 연결 문자열 복사][20-CopyAdoConnectionString]
7. 한 형식이 나 다른 hello 연결 문자열 정보를 클라이언트 프로그램 코드에 붙여 넣습니다.

자세한 내용은 다음을 참조하세요.<br/>[연결 문자열 및 구성 파일](http://msdn.microsoft.com/library/ms254494.aspx)를 클릭합니다.

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
