
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="e96d0-101">C# 프로그램 예</span><span class="sxs-lookup"><span data-stu-id="e96d0-101">C# program example</span></span>

<span data-ttu-id="e96d0-102">이 문서의 다음 섹션에는 Transact-SQL 문을 SQL 데이터베이스로 보내기 위해 ADO.NET를 사용하는 C# 프로그램이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-102">The next sections of this article present a C# program that uses ADO.NET to send Transact-SQL statements to the SQL database.</span></span> <span data-ttu-id="e96d0-103">C# 프로그램은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-103">The C# program performs the following actions:</span></span>

1. <span data-ttu-id="e96d0-104">[ADO.NET을 사용하여 SQL 데이터베이스에 연결합니다](#cs_1_connect).</span><span class="sxs-lookup"><span data-stu-id="e96d0-104">[Connects to our SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="e96d0-105">[테이블을 만듭니다](#cs_2_createtables).</span><span class="sxs-lookup"><span data-stu-id="e96d0-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="e96d0-106">[T-SQL INSERT 문을 발행하여 데이터로 테이블을 채웁니다](#cs_3_insert).</span><span class="sxs-lookup"><span data-stu-id="e96d0-106">[Populates the tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="e96d0-107">[조인을 사용하여 데이터를 업데이트합니다](#cs_4_updatejoin).</span><span class="sxs-lookup"><span data-stu-id="e96d0-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="e96d0-108">[조인을 사용하여 데이터를 삭제합니다](#cs_5_deletejoin).</span><span class="sxs-lookup"><span data-stu-id="e96d0-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="e96d0-109">[조인을 사용하여 데이터 행을 선택합니다](#cs_6_selectrows).</span><span class="sxs-lookup"><span data-stu-id="e96d0-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="e96d0-110">연결을 닫습니다(tempdb에서 임시 테이블 삭제).</span><span class="sxs-lookup"><span data-stu-id="e96d0-110">Closes the connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="e96d0-111">C# 프로그램은 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-111">The C# program contains:</span></span>

- <span data-ttu-id="e96d0-112">데이터베이스에 연결하기 위한 C# 코드.</span><span class="sxs-lookup"><span data-stu-id="e96d0-112">C# code to connect to the database.</span></span>
- <span data-ttu-id="e96d0-113">T-SQL 소스 코드를 반환하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="e96d0-113">Methods that return the T-SQL source code.</span></span>
- <span data-ttu-id="e96d0-114">T-SQL을 데이터베이스에 제출하는 두 가지 메서드.</span><span class="sxs-lookup"><span data-stu-id="e96d0-114">Two methods that submit the T-SQL to the database.</span></span>

#### <a name="to-compile-and-run"></a><span data-ttu-id="e96d0-115">컴파일 및 실행</span><span class="sxs-lookup"><span data-stu-id="e96d0-115">To compile and run</span></span>

<span data-ttu-id="e96d0-116">이 C# 프로그램은 하나의 논리적인 .cs 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="e96d0-117">하지만 여기서 프로그램은 물리적으로 여러 코드 블록으로 분할되어 각 블록을 보다 쉽게 보고 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-117">But here the program is physically divided into several code blocks, to make each block easier to see and understand.</span></span> <span data-ttu-id="e96d0-118">이 프로그램을 컴파일하고 실행하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-118">To compile and run this program, do the following:</span></span>

1. <span data-ttu-id="e96d0-119">Visual Studio에서 C# 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="e96d0-120">프로젝트 형식 이어야 합니다는 *콘솔* 에서 다음과 같은 계층 구조와 같은 응용 프로그램: **템플릿** > **Visual C#** >  **클래식 Windows 데스크톱** > **콘솔 응용 프로그램 (.NET Framework)**합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-120">The project type should be a *console* application, from something like the following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="e96d0-121">**Program.cs** 파일에서 코드의 작은 시작 줄을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-121">In the file **Program.cs**, erase the small starter lines of code.</span></span>
3. <span data-ttu-id="e96d0-122">여기에 제시된 것과 동일한 순서대로 Program.cs에 다음과 같은 블록을 복사하여 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-122">Into Program.cs, copy and paste each of the following blocks, in the same sequence they are presented here.</span></span>
4. <span data-ttu-id="e96d0-123">Program.cs에서 **Main** 메서드의 다음 값을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-123">In Program.cs, edit the following values in the **Main** method:</span></span>

   - <span data-ttu-id="e96d0-124">**cb.DataSource**</span><span class="sxs-lookup"><span data-stu-id="e96d0-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="e96d0-125">**cd.UserID**</span><span class="sxs-lookup"><span data-stu-id="e96d0-125">**cd.UserID**</span></span>
   - <span data-ttu-id="e96d0-126">**cb.Password**</span><span class="sxs-lookup"><span data-stu-id="e96d0-126">**cb.Password**</span></span>
   - <span data-ttu-id="e96d0-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="e96d0-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="e96d0-128">**System.Data.dll** 어셈블리가 참조되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-128">Verify that the assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="e96d0-129">확인하려면 **솔루션 탐색기** 창에서 **참조** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-129">To verify, expand the **References** node in the **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="e96d0-130">Visual Studio에서 프로그램을 빌드하려면 **빌드** 메뉴를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-130">To build the program in Visual Studio, click the **Build** menu.</span></span>
7. <span data-ttu-id="e96d0-131">Visual Studio의 프로그램을 실행하려면 **시작** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-131">To run the program from Visual Studio, click the **Start** button.</span></span> <span data-ttu-id="e96d0-132">cmd.exe 창에 보고서 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-132">The report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="e96d0-133">**tempdb**에서 **#**를 테이블 이름 앞에 추가하여 임시 테이블로 만드는 T-SQL 편집 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-133">You have the option of editing the T-SQL to add a leading **#** to the table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="e96d0-134">이는 사용할 수 있는 테스트 데이터베이스가 없는 경우 데모용으로 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="e96d0-135">연결을 닫으면 임시 테이블은 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-135">Temporary tables are deleted automatically when the connection closes.</span></span> <span data-ttu-id="e96d0-136">외래 키에 대한 모든 REFERENCES는 임시 테이블에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="e96d0-137">C# 블록 1: ADO.NET을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="e96d0-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="e96d0-138">다음</span><span class="sxs-lookup"><span data-stu-id="e96d0-138">Next</span></span>](#cs_2_createtables)


```csharp
using System;
using System.Data.SqlClient;   // System.Data.dll 
//using System.Data;           // For:  SqlDbType , ParameterDirection

namespace csharp_db_test
{
   class Program
   {
      static void Main(string[] args)
      {
         try
         {
            var cb = new SqlConnectionStringBuilder();
            cb.DataSource = "your_server.database.windows.net";
            cb.UserID = "your_user";
            cb.Password = "your_password";
            cb.InitialCatalog = "your_database";

            using (var connection = new SqlConnection(cb.ConnectionString))
            {
               connection.Open();

               Submit_Tsql_NonQuery(connection, "2 - Create-Tables",
                  Build_2_Tsql_CreateTables());

               Submit_Tsql_NonQuery(connection, "3 - Inserts",
                  Build_3_Tsql_Inserts());

               Submit_Tsql_NonQuery(connection, "4 - Update-Join",
                  Build_4_Tsql_UpdateJoin(),
                  "@csharpParmDepartmentName", "Accounting");

               Submit_Tsql_NonQuery(connection, "5 - Delete-Join",
                  Build_5_Tsql_DeleteJoin(),
                  "@csharpParmDepartmentName", "Legal");

               Submit_6_Tsql_SelectEmployees(connection);
            }
         }
         catch (SqlException e)
         {
            Console.WriteLine(e.ToString());
         }
         Console.WriteLine("View the report output here, then press any key to end the program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-to-create-tables"></a><span data-ttu-id="e96d0-139">C# 블록 2: 테이블을 만드는 T-SQL</span><span class="sxs-lookup"><span data-stu-id="e96d0-139">C# block 2: T-SQL to create tables</span></span>

- <span data-ttu-id="e96d0-140">[이전](#cs_1_connect) &nbsp; / &nbsp; [다음](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="e96d0-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

```csharp
      static string Build_2_Tsql_CreateTables()
      {
         return @"
DROP TABLE IF EXISTS tabEmployee;
DROP TABLE IF EXISTS tabDepartment;  -- Drop parent table last.


CREATE TABLE tabDepartment
(
   DepartmentCode  nchar(4)          not null
      PRIMARY KEY,
   DepartmentName  nvarchar(128)     not null
);

CREATE TABLE tabEmployee
(
   EmployeeGuid    uniqueIdentifier  not null  default NewId()
      PRIMARY KEY,
   EmployeeName    nvarchar(128)     not null,
   EmployeeLevel   int               not null,
   DepartmentCode  nchar(4)              null
      REFERENCES tabDepartment (DepartmentCode)  -- (REFERENCES would be disallowed on temporary tables.)
);
";
      }
```

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="e96d0-141">엔터티 관계 다이어그램(ERD)</span><span class="sxs-lookup"><span data-stu-id="e96d0-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="e96d0-142">이전 CREATE TABLE 문에는 두 테이블 간의 *외래 키*(FK) 관계를 만들기 위해 **REFERENCES** 키워드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-142">The preceding CREATE TABLE statements involve the **REFERENCES** keyword to create a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="e96d0-143">tempdb를 사용하는 경우 선행 대시의 쌍을 사용하여 `--REFERENCES` 키워드를 주석으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-143">If you are using tempdb, comment out the `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="e96d0-144">다음은 두 테이블 간의 관계를 표시하는 ERD입니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-144">Next is an ERD that displays the relationship between the two tables.</span></span> <span data-ttu-id="e96d0-145">#tabEmployee.DepartmentCode *자식* 열의 값은 #tabDepartment.Department *부모* 열에 있는 값으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-145">The values in the #tabEmployee.DepartmentCode *child* column are limited to the values present in the #tabDepartment.Department *parent* column.</span></span>

![외래 키를 표시하는 ERD](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-to-insert-data"></a><span data-ttu-id="e96d0-147">C# 블록 3: 데이터를 삽입하는 T-SQL</span><span class="sxs-lookup"><span data-stu-id="e96d0-147">C# block 3: T-SQL to insert data</span></span>

- <span data-ttu-id="e96d0-148">[이전](#cs_2_createtables) &nbsp; / &nbsp; [다음](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="e96d0-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- The company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- The company has these employees, each in one department.
INSERT INTO tabEmployee
   (EmployeeName, EmployeeLevel, DepartmentCode)
      VALUES
   ('Alison'  , 19, 'acct'),
   ('Barbara' , 17, 'hres'),
   ('Carol'   , 21, 'acct'),
   ('Deborah' , 24, 'legl'),
   ('Elle'    , 15, null);
";
      }
```


<a name="cs_4_updatejoin"/>
### <a name="c-block-4-t-sql-to-update-join"></a><span data-ttu-id="e96d0-149">C# 블록 4: 업데이트 조인하는 T-SQL</span><span class="sxs-lookup"><span data-stu-id="e96d0-149">C# block 4: T-SQL to update-join</span></span>

- <span data-ttu-id="e96d0-150">[이전](#cs_3_insert) &nbsp; / &nbsp; [다음](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="e96d0-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


```csharp
      static string Build_4_Tsql_UpdateJoin()
      {
         return @"
DECLARE @DName1  nvarchar(128) = @csharpParmDepartmentName;  --'Accounting';


-- Promote everyone in one department (see @parm...).
UPDATE empl
   SET
      empl.EmployeeLevel += 1
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName1;
";
      }
```


<a name="cs_5_deletejoin"/>
### <a name="c-block-5-t-sql-to-delete-join"></a><span data-ttu-id="e96d0-151">C# 블록 5: 삭제 조인하는 T-SQL</span><span class="sxs-lookup"><span data-stu-id="e96d0-151">C# block 5: T-SQL to delete-join</span></span>

- <span data-ttu-id="e96d0-152">[이전](#cs_4_updatejoin) &nbsp; / &nbsp; [다음](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="e96d0-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size the Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband the Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-to-select-rows"></a><span data-ttu-id="e96d0-153">C# 블록 6: 행을 선택하는 T-SQL</span><span class="sxs-lookup"><span data-stu-id="e96d0-153">C# block 6: T-SQL to select rows</span></span>

- <span data-ttu-id="e96d0-154">[이전](#cs_5_deletejoin) &nbsp; / &nbsp; [다음](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="e96d0-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all the final Employees.
SELECT
      empl.EmployeeGuid,
      empl.EmployeeName,
      empl.EmployeeLevel,
      empl.DepartmentCode,
      dept.DepartmentName
   FROM
      tabEmployee   as empl
      LEFT OUTER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   ORDER BY
      EmployeeName;
";
      }
```


<a name="cs_6b_datareader"/>
### <a name="c-block-6b-executereader"></a><span data-ttu-id="e96d0-155">C# 블록 6b: ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="e96d0-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="e96d0-156">[이전](#cs_6_selectrows) &nbsp; / &nbsp; [다음](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="e96d0-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="e96d0-157">이 메서드는 **Build_6_Tsql_SelectEmployees** 메서드에 의해 빌드된 T-SQL SELECT 문을 실행하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-157">This method is designed to run the T-SQL SELECT statement that is built by the **Build_6_Tsql_SelectEmployees** method.</span></span>


```csharp
      static void Submit_6_Tsql_SelectEmployees(SqlConnection connection)
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("Now, SelectEmployees (6)...");

         string tsql = Build_6_Tsql_SelectEmployees();

         using (var command = new SqlCommand(tsql, connection))
         {
            using (SqlDataReader reader = command.ExecuteReader())
            {
               while (reader.Read())
               {
                  Console.WriteLine("{0} , {1} , {2} , {3} , {4}",
                     reader.GetGuid(0),
                     reader.GetString(1),
                     reader.GetInt32(2),
                     (reader.IsDBNull(3)) ? "NULL" : reader.GetString(3),
                     (reader.IsDBNull(4)) ? "NULL" : reader.GetString(4));
               }
            }
         }
      }
```


<a name="cs_7_executenonquery"/>
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="e96d0-158">C# 블록 7: ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="e96d0-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="e96d0-159">[이전](#cs_6b_datareader) &nbsp; / &nbsp; [다음](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="e96d0-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="e96d0-160">이 메서드는 어떠한 데이터 행도 반환하지 않고 테이블의 데이터 콘텐츠를 수정하는 작업에 대해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-160">This method is called for operations that modify the data content of tables without returning any data rows.</span></span>


```csharp
      static void Submit_Tsql_NonQuery(
         SqlConnection connection,
         string tsqlPurpose,
         string tsqlSourceCode,
         string parameterName = null,
         string parameterValue = null
         )
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("T-SQL to {0}...", tsqlPurpose);

         using (var command = new SqlCommand(tsqlSourceCode, connection))
         {
            if (parameterName != null)
            {
               command.Parameters.AddWithValue(  // Or, use SqlParameter class.
                  parameterName,
                  parameterValue);
            }
            int rowsAffected = command.ExecuteNonQuery();
            Console.WriteLine(rowsAffected + " = rows affected.");
         }
      }
   } // EndOfClass
}
```


<a name="cs_8_output"/>
### <a name="c-block-8-actual-test-output-to-the-console"></a><span data-ttu-id="e96d0-161">C# 블록 8: 콘솔에 대한 실제 테스트 출력</span><span class="sxs-lookup"><span data-stu-id="e96d0-161">C# block 8: Actual test output to the console</span></span>

- [<span data-ttu-id="e96d0-162">이전</span><span class="sxs-lookup"><span data-stu-id="e96d0-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="e96d0-163">이 섹션에는 프로그램이 콘솔에 전송한 출력을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-163">This section captures the output that the program sent to the console.</span></span> <span data-ttu-id="e96d0-164">guid 값만 테스트를 실행할 때마다 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="e96d0-164">Only the guid values vary between test runs.</span></span>


```text
[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>> csharp_db_test.exe

=================================
Now, CreateTables (10)...

=================================
Now, Inserts (20)...

=================================
Now, UpdateJoin (30)...
2 rows affected, by UpdateJoin.

=================================
Now, DeleteJoin (40)...

=================================
Now, SelectEmployees (50)...
0199be49-a2ed-4e35-94b7-e936acf1cd75 , Alison , 20 , acct , Accounting
f0d3d147-64cf-4420-b9f9-76e6e0a32567 , Barbara , 17 , hres , Human Resources
cf4caede-e237-42d2-b61d-72114c7e3afa , Carol , 22 , acct , Accounting
cdde7727-bcfd-4f72-a665-87199c415f8b , Elle , 15 , NULL , NULL

[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>>
```
