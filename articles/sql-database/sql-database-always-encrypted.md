---
title: "상시 암호화: Azure SQL Database - Windows 인증서 저장소 | Microsoft Docs"
description: "이 문서에서는 toosecure 중요 한 데이터를 사용 하 여 데이터베이스 암호화는 SQL 데이터베이스에서 상시 암호화 마법사 SQL Server Management Studio (SSMS) hello 하는 방법을 보여 줍니다. 또한 표시 방법을 toostore hello Windows 인증서에 암호화 키를 저장 합니다."
keywords: "데이터 암호화, sql 암호화, 데이터베이스 암호화, 중요한 데이터 암호화, 상시 암호화"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a>SQL 데이터베이스의 중요 한 데이터를 보호 하 고 hello Windows 인증서 저장소에 암호화 키 저장 항상 암호화:

이 문서에서는 hello를 사용 하 여 데이터베이스 암호화 된 데이터베이스 SQL의 중요 한 데이터 toosecure 방법 [상시 암호화 마법사](https://msdn.microsoft.com/library/mt459280.aspx) 에 [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx)합니다. 또한 표시 방법을 toostore hello Windows 인증서에 암호화 키를 저장 합니다.

상시 암호화는 Azure SQL 데이터베이스에서 새 데이터 암호화 기술을 도움이 되는 SQL Server 클라이언트와 서버 간에 이동 하는 동안 중요 한 hello 서버에 저장 된 상태의 데이터를 보호 하 고 hello 데이터 사용 중으로 표시 하지 않고도 중요 한 데이터 확인 hello 데이터베이스 시스템 내부 일반 텍스트입니다. 데이터를 암호화 한 후 클라이언트 응용 프로그램 또는 응용 프로그램 키가 서버를 액세스 toohello 일반 텍스트 데이터에 액세스할 수 있습니다. 자세한 내용은 [상시 암호화(데이터베이스 엔진)](https://msdn.microsoft.com/library/mt163865.aspx)를 참조하세요.

Hello 데이터베이스 toouse 상시 암호화를 구성 했으면 C#으로 Visual Studio toowork hello 암호화 된 데이터와 클라이언트 응용 프로그램이 만들어집니다.

에서 다음과 같이 hello이 문서 toolearn 어떻게 Azure SQL 데이터베이스에 대 한 상시 암호화를 tooset 합니다. 이 문서에서는 tooperform hello 다음 작업 방법을 배웁니다.

* SSMS toocreate에서 사용 하 여 hello 상시 암호화 마법사 [상시 암호화 키](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3)합니다.
  * [CMK(열 마스터 키)](https://msdn.microsoft.com/library/mt146393.aspx)를 만듭니다.
  * [CEK(열 암호화 키)](https://msdn.microsoft.com/library/mt146372.aspx)를 만듭니다.
* 데이터베이스 테이블을 만들고 열을 암호화합니다.
* 삽입 선택한 hello 암호화 된 열에서 데이터를 표시 하는 응용 프로그램을 만듭니다.

## <a name="prerequisites"></a>필수 조건
이 자습서에는 다음이 필요합니다.

* Azure 계정 및 구독 없는 경우 지금 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록하세요.
* [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 버전 13.0.700.242 이상.
* [.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) hello 클라이언트 컴퓨터에 이상.
* [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).

## <a name="create-a-blank-sql-database"></a>빈 SQL 데이터베이스 만들기
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. **새로 만들기** > **데이터 + 저장소** > **SQL Database**를 클릭합니다.
3. 새 서버 또는 기존 서버에 **클리닉**이라는 **빈** 데이터베이스를 만듭니다. Hello Azure 포털에서에서 데이터베이스를 만드는 방법에 대 한 자세한 지침을 참조 하십시오. [첫 번째 Azure SQL 데이터베이스](sql-database-get-started-portal.md)합니다.
   
    ![빈 데이터베이스 만들기](./media/sql-database-always-encrypted/create-database.png)

Hello 자습서의 뒷부분에 나오는 hello 연결 문자열이 필요 합니다. Hello 데이터베이스를 만든 후 toohello 새 Clinic 데이터베이스와 복사본 hello 연결 문자열을 이동 합니다. 언제 든 지 hello 연결 문자열을 가져올 수 있지만 간편한 toocopy hello Azure 포털에에서 있는 경우.

1. **SQL Databases** > **Clinic** > **데이터베이스 연결 문자열 표시**를 클릭합니다.
2. 에 대 한 연결 문자열 hello 복사 **ADO.NET**합니다.
   
    ![Hello 연결 문자열 복사](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>SSMS를 사용 하 여 toohello 데이터베이스 연결
SSMS를 열고 toohello 서버 hello Clinic 데이터베이스와 연결 합니다.

1. SSMS를 엽니다. (클릭 **연결** > **데이터베이스 엔진** tooopen hello **tooServer 연결** 창이 열려 있지 않은 경우).
2. 서버 이름 및 자격 증명을 입력합니다. hello 연결 문자열에 앞에서 복사한을 hello 서버 이름을 hello SQL 데이터베이스 블레이드에서 찾을 수 있습니다. 형식 hello 서버 전체 이름을 포함 하 여 *database.windows.net*합니다.
   
    ![Hello 연결 문자열 복사](./media/sql-database-always-encrypted/ssms-connect.png)

경우 hello **새 방화벽 규칙** 창이 열리고 tooAzure에 로그인 하 고 SSMS를 통해 사용자에 대 한 새 방화벽 규칙을 만듭니다.

## <a name="create-a-table"></a>테이블 만들기
이 섹션에서는 테이블 toohold 환자 데이터를 만듭니다. 됩니다 일반 테이블 처음-hello 다음 섹션에서 암호화를 구성 합니다.

1. **데이터베이스**를 확장합니다.
2. 마우스 오른쪽 단추로 클릭 hello **클리닉** 클릭 하 고 데이터베이스 **새 쿼리**합니다.
3. TRANSACT-SQL (T-SQL) hello 새 쿼리 창에 다음 붙여넣기 hello 및 **Execute** 것입니다.

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a>열 암호화(상시 암호화 구성)
마법사를 제공 하는 SSMS tooeasily 상시 암호화를 구성 하면 한 hello CMK, CEK를 암호화 된 열을 설정 합니다.

1. **데이터베이스** > **빈** > **테이블**를 사용하여 데이터베이스 암호화로 SQL 데이터베이스의 중요한 데이터를 보호하는 방법을 보여 줍니다.
2. 마우스 오른쪽 단추로 클릭 hello **환자** 테이블을 선택한 **열 암호화** tooopen hello 상시 암호화 마법사:
   
    ![열 암호화](./media/sql-database-always-encrypted/encrypt-columns.png)

hello 상시 암호화 마법사에는 다음 섹션 hello: **열 선택 영역**, **마스터 키 구성** (CMK) **유효성 검사**, 및  **요약**합니다.

### <a name="column-selection"></a>열 선택
클릭 **다음** hello에 **소개** 페이지 tooopen hello **열 선택 영역** 페이지. 이 페이지에서 열을 선택 합니다 tooencrypt, 원하는 [유형의 암호화를 hello 및 어떤 열 암호화 키 (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse 합니다.

각 환자에 대해 **SSN** 및 **BirthDate** 정보를 암호화합니다. hello **SSN** 열에서 같음 조회, 조인 및 그룹화를 지 원하는 결정적 암호화를 사용 합니다. hello **BirthDate** 열 작업을 지원 하지 않는 임의 암호화를 사용 합니다.

집합 hello **암호화 유형** hello에 대 한 **SSN** 열 너무**결정적** 및 hello **BirthDate** 열 너무 **임의**합니다. **다음**을 누릅니다.

![열 암호화](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a>마스터 키 구성
hello **마스터 키 구성** 설정한 CMK 및 선택 hello 키 저장소 공급자를 hello CMK를 저장할 페이지는 합니다. 현재 hello Windows 인증서 저장소, Azure 주요 자격 증명 모음 또는 하드웨어 보안 모듈 (HSM)는 CMK를 저장할 수 있습니다. 이 자습서에서는 어떻게 toostore hello Windows 인증서에 키에 저장 합니다.

**Windows 인증서 저장소**가 선택되었는지 확인하고 **다음**을 클릭합니다.

![마스터 키 구성](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a>유효성 검사
이제 hello 열을 암호화 하거나 PowerShell 스크립트 toorun를 나중에 저장할 수 있습니다. 이 자습서에 대 한 선택 **지금 toofinish 진행** 클릭 **다음**합니다.

### <a name="summary"></a>요약
Hello 설정이 모두 정확 하 고 클릭 확인 **마침** 상시 암호화를 위한 toocomplete hello 설치 합니다.

![요약](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a>Hello 마법사 작업 확인
Hello 마법사가 완료 되 면 데이터베이스에 상시 암호화에 대해 설정 됩니다. hello 수행 하는 마법사 hello 동작을 수행 합니다.

* CMK를 만들었습니다.
* CEK를 만들었습니다.
* 구성 된 hello 암호화에 대 한 열을 선택 합니다. 프로그램 **환자** 테이블에 현재 데이터가 없는 하지만 모든 열의 기존 데이터를 선택 하는 hello 이제 암호화 합니다.

SSMS의 hello 키의 hello 생성 너무 이동 하 여 확인할 수 있습니다**클리닉** > **보안** > **상시 암호화 키**합니다. 이제 자동으로 생성 하는 마법사를 hello hello 새 키를 확인할 수 있습니다.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Hello 암호화 된 데이터를 사용 하는 클라이언트 응용 프로그램 만들기
상시 암호화를 설정 했으므로 수행 하는 응용 프로그램을 빌드할 수 있습니다 *삽입* 및 *선택* hello에 암호화 된 열입니다. toosuccessfully hello 샘플 응용 프로그램 실행을 실행 해야 hello에 같은 컴퓨터 hello 상시 암호화 마법사를 실행 합니다. 다른 컴퓨터에서 toorun hello 응용 프로그램을 항상 암호화 인증서 toohello 실행 하는 컴퓨터 hello 클라이언트 응용 프로그램을 배포 해야 합니다.  

> [!IMPORTANT]
> 응용 프로그램 사용 해야 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) 상시 암호화 열이 있는 일반 텍스트 데이터 toohello 서버를 전달 하는 경우 개체입니다. SqlParameter 개체를 사용하지 않고 리터럴 값을 전달하면 예외가 발생합니다.
> 
> 

1. Visual Studio를 열고 새 C# 콘솔 응용 프로그램을 만듭니다. 프로젝트가 너무 설정 되어 있는지 확인**.NET Framework 4.6** 이상.
2. 이름 hello 프로젝트 **AlwaysEncryptedConsoleApp** 클릭 **확인**합니다.

![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>항상 암호화 하 여 연결 문자열 tooenable 수정
이 섹션에서는 데이터베이스 연결 문자열에서 tooenable 항상 암호화 하는 방법입니다. "항상 암호화 샘플 콘솔 응용 프로그램." hello 다음 섹션에서 방금 만든 hello 콘솔 응용 프로그램을 수정 합니다.

항상 암호화 tooenable, 해야 tooadd hello **열 암호화 설정** 키워드 tooyour 연결 문자열을 너무 설정**Enabled**합니다.

Hello 연결 문자열에서 직접 설정할 수 있습니다 또는 사용 하 여 설정할 수 있습니다는 [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx)합니다. hello 예제 응용 프로그램 hello에 다음 섹션에서는 어떻게 toouse **SqlConnectionStringBuilder**합니다.

> [!NOTE]
> 이 hello 작업만 실행 하는 클라이언트 응용 프로그램 특정 tooAlways 암호화에에서 필요 합니다. 외부에서 연결 문자열을 저장 하는 기존 응용 프로그램의 경우 (즉, 구성 파일에), 모든 코드를 변경 하지 않고 항상 암호화 하는 수 tooenable 될 수도 있습니다.
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Hello 연결 문자열에서 상시 암호화를 사용 하도록 설정
Hello tooyour 연결 문자열 키워드에 다음을 추가 합니다.

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a>SqlConnectionStringBuilder로 상시 암호화 사용
hello 다음 코드를 보여 줍니다 방법을 설정 하 여 상시 암호화는 tooenable hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) 너무[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx)합니다.

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a>상시 암호화 샘플 콘솔 응용 프로그램
이 샘플에서는 다음 방법을 설명합니다.

* 항상 암호화 하 여 연결 문자열 tooenable를 수정 합니다.
* Hello 암호화 된 열에 데이터를 삽입 합니다.
* 암호화된 열에서 특정 값에 필터링하여 레코드 선택.

Hello 내용 바꾸기 **Program.cs** 코드 다음 hello로 합니다. 유효한 연결 문자열 hello Azure 포털에서에서 hello Main 메서드에 바로 위의 hello 줄에서 전역 connectionString 변수 hello에 대 한 연결 문자열을 hello를 바꿉니다. 이 hello 작업만 toomake toothis 코드가 필요 합니다.

작업에서 항상 암호화 hello 앱 toosee를 실행 합니다.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-hello-data-is-encrypted"></a>Hello 데이터의 암호화를 확인 하십시오.
Hello를 쿼리하여 서버 hello에 hello 실제 데이터의 암호화를 신속 하 게 확인할 수 있습니다 **환자** SSMS 사용 하 여 데이터입니다. (사용 하 여 현재 연결에 hello 열 암호화 설정 해제 되어 있는 아직.)

Hello hello Clinic 데이터베이스에서 다음 쿼리를 실행 합니다.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Hello 암호화 열 일반 텍스트 데이터가 포함 되지 않은 것을 볼 수 있습니다.

   ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/ssms-encrypted.png)

toouse SSMS tooaccess hello 일반 텍스트 데이터를 hello를 추가할 수 있습니다 **열 암호화 설정 = 사용** toohello 연결 매개 변수입니다.

1. SSMS에서 **개체 탐색기**에 있는 서버를 마우스 오른쪽 단추로 클릭하고 **연결 끊기**를 클릭합니다.
2. 클릭 **연결** > **데이터베이스 엔진** tooopen hello **tooServer 연결** 창과 클릭 **옵션**합니다.
3. **추가 연결 매개 변수**를 클릭하고 **열 암호화 설정=활성화**를 입력합니다.
   
    ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. 실행 hello hello에 대 한 쿼리 다음 **Clinic** 데이터베이스입니다.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     이제 hello 암호화 된 열에 hello 일반 텍스트 데이터를 볼 수 있습니다.

    ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> SSMS (클라이언트)와 다른 컴퓨터에서 연결 하는 경우 액세스 toohello 암호화 키 체계가 없습니다 및 수 toodecrypt hello 데이터 됩니다.
> 
> 

## <a name="next-steps"></a>다음 단계
상시 암호화를 사용 하는 데이터베이스를 만든 후에 toodo hello 다음을 사용할 수 있습니다.

* 다른 컴퓨터에서 이 샘플을 실행합니다. 하므로 체계가 없습니다 toohello 일반 텍스트 데이터에 액세스 하 고 성공적으로 실행 되지 않습니다 액세스 toohello 암호화 키를 없을 있습니다.
* [키 회전 및 정리](https://msdn.microsoft.com/library/mt607048.aspx).
* [상시 암호화로 이미 암호화된 데이터 마이그레이션](https://msdn.microsoft.com/library/mt621539.aspx)
* [항상 암호화 인증서 tooother 클라이언트 컴퓨터를 배포](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (hello "사용 가능한 tooApplications 인증서 및 사용자 만들기" 섹션 참조).

## <a name="related-information"></a>관련 정보
* [상시 암호화(클라이언트 개발)](https://msdn.microsoft.com/library/mt147923.aspx)
* [투명한 데이터 암호화](https://msdn.microsoft.com/library/bb934049.aspx)
* [SQL Server 암호화](https://msdn.microsoft.com/library/bb510663.aspx)
* [상시 암호화 마법사](https://msdn.microsoft.com/library/mt459280.aspx)
* [상시 암호화 블로그](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

