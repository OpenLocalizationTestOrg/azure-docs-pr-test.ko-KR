
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a>C# 프로그램 예

이 문서의 다음 섹션에서는 hello ADO.NET toosend Transact SQL 문 toohello SQL 데이터베이스를 사용 하는 C# 프로그램을 제공 합니다. hello C# 프로그램 hello 다음 작업을 수행 합니다.

1. [ADO.NET을 사용 하 여 tooour SQL 데이터베이스 연결](#cs_1_connect)합니다.
2. [테이블을 만듭니다](#cs_2_createtables).
3. [T-SQL INSERT 문을 실행 하 여 hello 테이블에 데이터를 채우는](#cs_3_insert)합니다.
4. [조인을 사용하여 데이터를 업데이트합니다](#cs_4_updatejoin).
5. [조인을 사용하여 데이터를 삭제합니다](#cs_5_deletejoin).
6. [조인을 사용하여 데이터 행을 선택합니다](#cs_6_selectrows).
7. (Tempdb에서 임시 테이블을 삭제)는 hello 연결을 닫습니다.

hello C# 프로그램에 포함 되어 있습니다.

- C# 코드 tooconnect toohello 데이터베이스입니다.
- Hello T-SQL 소스 코드를 반환 하는 메서드.
- Hello T-SQL toohello 데이터베이스를 전송 하는 두 개의 메서드.

#### <a name="toocompile-and-run"></a>toocompile 및 실행

이 C# 프로그램은 하나의 논리적인 .cs 파일입니다. 그러나 hello 프로그램 여러 코드 블록으로 물리적으로 분할 되는 여기, toomake 쉽게 toosee 각 블록을 이해 합니다. toocompile이이 프로그램을 실행 하 고, 다음 hello지 않습니다.

1. Visual Studio에서 C# 프로젝트를 만듭니다.
    - hello 프로젝트 형식 이어야 합니다는 *콘솔* 에서 계층을 따라 hello와 같은 응용 프로그램: **템플릿** > **Visual C#** > **클래식 Windows 데스크톱** > **콘솔 응용 프로그램 (.NET Framework)**합니다.
3. Hello 파일에서 **Program.cs**, hello 작은 시작 줄의 코드를 지웁니다.
3. Program.cs에 복사 및 각 붙여넣기 hello에서 블록을 다음의 동일한 시퀀스가 여기에 제공 하는 hello 합니다.
4. Hello에 값을 편집 hello 다음 Program.cs에 **Main** 메서드:

   - **cb.DataSource**
   - **cd.UserID**
   - **cb.Password**
   - **InitialCatalog**

5. 해당 hello 어셈블리 확인 **System.Data.dll** 참조 됩니다. tooverify, hello 확장 **참조** hello에 대 한 노드 **솔루션 탐색기** 창.
6. Visual Studio에서 toobuild hello 프로그램 클릭 hello **빌드** 메뉴.
7. Visual Studio에서 toorun hello 프로그램 클릭 hello **시작** 단추입니다. hello 보고서 출력 cmd.exe 창에 표시 됩니다.

> [!NOTE]
> Hello T-SQL tooadd 앞에 오는 편집으로 인해 hello 옵션이  **#**  의 임시 테이블을 만듭니다는 toohello 테이블 이름을 **tempdb**합니다. 이는 사용할 수 있는 테스트 데이터베이스가 없는 경우 데모용으로 유용할 수 있습니다. 임시 테이블은 hello 연결을 닫을 때 자동으로 삭제 됩니다. 외래 키에 대한 모든 REFERENCES는 임시 테이블에 적용되지 않습니다.
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a>C# 블록 1: ADO.NET을 사용하여 연결

- [다음](#cs_2_createtables)


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
         Console.WriteLine("View hello report output here, then press any key tooend hello program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-toocreate-tables"></a>C# 블록 2: T-SQL toocreate 테이블

- [이전](#cs_1_connect) &nbsp; / &nbsp; [다음](#cs_3_insert)

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

#### <a name="entity-relationship-diagram-erd"></a>엔터티 관계 다이어그램(ERD)

hello 위의 CREATE TABLE 문에서 포함 hello **참조** 키워드 toocreate는 *외래 키* 두 테이블 간의 관계 (FK).  Tempdb를 사용 하는 주석으로 처리 hello `--REFERENCES` 선행 대시의 쌍을 사용 하 여 키워드입니다.

다음은 hello 두 테이블 간의 hello 관계를 표시 하는 경우에 ERD입니다. hello #tabEmployee.DepartmentCode 값 hello *자식* 열은 hello #tabDepartment.Department에 제한적된 toohello 값 *부모* 열입니다.

![외래 키를 표시하는 ERD](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a>C# 블록 3: T-SQL tooinsert 데이터

- [이전](#cs_2_createtables) &nbsp; / &nbsp; [다음](#cs_4_updatejoin)


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- hello company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- hello company has these employees, each in one department.
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
### <a name="c-block-4-t-sql-tooupdate-join"></a>C# 블록 4: T-SQL tooupdate 조인

- [이전](#cs_3_insert) &nbsp; / &nbsp; [다음](#cs_5_deletejoin)


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
### <a name="c-block-5-t-sql-toodelete-join"></a>C# 블록 5: T-SQL toodelete 조인

- [이전](#cs_4_updatejoin) &nbsp; / &nbsp; [다음](#cs_6_selectrows)


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size hello Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband hello Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-tooselect-rows"></a>C# 블록 6: T-SQL tooselect 행

- [이전](#cs_5_deletejoin) &nbsp; / &nbsp; [다음](#cs_6b_datareader)


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all hello final Employees.
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
### <a name="c-block-6b-executereader"></a>C# 블록 6b: ExecuteReader

- [이전](#cs_6_selectrows) &nbsp; / &nbsp; [다음](#cs_7_executenonquery)

이 메서드는 디자인 된 toorun hello T-SQL SELECT 문 하 여 hello 빌드된 **Build_6_Tsql_SelectEmployees** 메서드.


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
### <a name="c-block-7-executenonquery"></a>C# 블록 7: ExecuteNonQuery

- [이전](#cs_6b_datareader) &nbsp; / &nbsp; [다음](#cs_8_output)

이 메서드는 모든 데이터 행을 반환 하지 않고 테이블 hello 데이터 콘텐츠를 수정 하는 작업에 대 한 호출 됩니다.


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
         Console.WriteLine("T-SQL too{0}...", tsqlPurpose);

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
### <a name="c-block-8-actual-test-output-toohello-console"></a>C# 블록 8: 실제 테스트 출력 toohello 콘솔

- [이전](#cs_7_executenonquery)

이 섹션에 전송 하는 프로그램 toohello 콘솔 hello hello 출력을 나타납니다. 테스트 실행 간에 hello guid 값만 달라 집니다.


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
