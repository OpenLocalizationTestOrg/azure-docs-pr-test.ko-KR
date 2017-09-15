
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-the-connection-string-from-the-azure-portal"></a><span data-ttu-id="8ec43-101">Azure 포털에서 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="8ec43-101">Obtain the connection string from the Azure portal</span></span>
<span data-ttu-id="8ec43-102">[Azure 포털](https://portal.azure.com/) 에서 클라이언트 프로그램이 Azure SQL 데이터베이스와 상호 작용하는 데 필요한 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec43-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span></span> 

1. <span data-ttu-id="8ec43-103">**찾아보기** > **SQL 데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec43-103">Click **BROWSE** > **SQL databases**.</span></span>
2. <span data-ttu-id="8ec43-104">**SQL 데이터베이스** 블레이드 왼쪽 위에 있는 필터 텍스트 상자에 데이터베이스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec43-104">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span></span>
3. <span data-ttu-id="8ec43-105">해당 데이터베이스에 대한 행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec43-105">Click the row for your database.</span></span>
4. <span data-ttu-id="8ec43-106">데이터베이스 블레이드가 표시된 후 시각적 편의를 위해 표준 최소화 컨트롤을 클릭하여 검색 및 데이터베이스 필터링에 사용한 블레이드를 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec43-106">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span></span> 
   
    ![필터링을 통해 데이터베이스 격리][10-FilterDatabase]
5. <span data-ttu-id="8ec43-108">데이터베이스 블레이드에서 **데이터베이스 연결 문자열 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec43-108">On the blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="8ec43-109">ADO.NET 연결 라이브러리를 사용하려는 경우 **ADO**라는 레이블이 지정된 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec43-109">If you intend to use the ADO.NET connection library, copy the string labeled **ADO**.</span></span> 
   
    ![데이터베이스에 대한 ADO 연결 문자열 복사][20-CopyAdoConnectionString]
7. <span data-ttu-id="8ec43-111">한 가지 형식이나 다른 형식으로 연결 문자열 정보를 클라이언트 프로그램 코드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec43-111">In one format or another, paste the connection string information into your client program code.</span></span>

<span data-ttu-id="8ec43-112">자세한 내용은 </span><span class="sxs-lookup"><span data-stu-id="8ec43-112">For more information, see:</span></span><br/><span data-ttu-id="8ec43-113">[연결 문자열 및 구성 파일](http://msdn.microsoft.com/library/ms254494.aspx)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec43-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
