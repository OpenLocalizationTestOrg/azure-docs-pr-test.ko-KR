
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-hello-connection-string-from-hello-azure-portal"></a><span data-ttu-id="2702d-101">Hello Azure 포털에서에서 hello 연결 문자열을 가져옵니다</span><span class="sxs-lookup"><span data-stu-id="2702d-101">Obtain hello connection string from hello Azure portal</span></span>
<span data-ttu-id="2702d-102">사용 하 여 hello [Azure 포털](https://portal.azure.com/) 프로그램 클라이언트 프로그램 toointeract Azure SQL 데이터베이스에 대 한 필요한 tooobtain hello 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="2702d-102">Use hello [Azure portal](https://portal.azure.com/) tooobtain hello connection string necessary for your client program toointeract with Azure SQL Database:</span></span> 

1. <span data-ttu-id="2702d-103">**찾아보기** > **SQL 데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2702d-103">Click **BROWSE** > **SQL databases**.</span></span>
2. <span data-ttu-id="2702d-104">데이터베이스의 이름을 hello hello 필터 텍스트 상자에 입력 hello 왼쪽 위 근처의 hello **SQL 데이터베이스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="2702d-104">Enter hello name of your database into hello filter text box near hello upper-left of hello **SQL databases** blade.</span></span>
3. <span data-ttu-id="2702d-105">데이터베이스에 대 한 hello 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2702d-105">Click hello row for your database.</span></span>
4. <span data-ttu-id="2702d-106">데이터베이스에 대 한 hello 블레이드가 나타나면 편하게 클릭할 수 있는 표준 hello 컨트롤 toocollapse hello 블레이드 찾아보고 데이터베이스 필터링에 사용을 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2702d-106">After hello blade appears for your database, for visual convenience you can click hello standard minimize controls toocollapse hello blades  you used for browsing and database filtering.</span></span> 
   
    ![데이터베이스 tooisolate 필터링][10-FilterDatabase]
5. <span data-ttu-id="2702d-108">데이터베이스에 대 한 hello 블레이드에서 클릭 **데이터베이스 연결 문자열 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2702d-108">On hello blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="2702d-109">Toouse hello ADO.NET 연결 라이브러리를 가져오려는 경우 레이블이 지정 된 hello 문자열을 복사 합니다. **ADO**합니다.</span><span class="sxs-lookup"><span data-stu-id="2702d-109">If you intend toouse hello ADO.NET connection library, copy hello string labeled **ADO**.</span></span> 
   
    ![데이터베이스에 대 한 hello ADO 연결 문자열 복사][20-CopyAdoConnectionString]
7. <span data-ttu-id="2702d-111">한 형식이 나 다른 hello 연결 문자열 정보를 클라이언트 프로그램 코드에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2702d-111">In one format or another, paste hello connection string information into your client program code.</span></span>

<span data-ttu-id="2702d-112">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2702d-112">For more information, see:</span></span><br/><span data-ttu-id="2702d-113">[연결 문자열 및 구성 파일](http://msdn.microsoft.com/library/ms254494.aspx)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2702d-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
