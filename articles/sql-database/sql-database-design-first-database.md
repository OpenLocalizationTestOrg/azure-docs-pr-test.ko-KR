---
title: "aaaDesign 첫 번째 Azure SQL 데이터베이스 | Microsoft Docs"
description: "Toodesign 첫 번째 Azure SQL 데이터베이스에 알아봅니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 65f0a1594cbdda7480abf32a847266a073e7560d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-sql-database"></a>첫 번째 Azure SQL Database 디자인

Azure SQL 데이터베이스는 관계형 데이터베이스-으로-a (DBaaS)의 서비스 hello Microsoft 클라우드 ("Azure"). 이 자습서에 알아봅니다 방법을 toouse hello Azure 포털 및 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)를: 

> [!div class="checklist"]
> * Hello Azure 포털에서에서 데이터베이스 만들기
> * Hello Azure 포털에서에서 서버 수준 방화벽 규칙 설정
> * SSMS를 사용 하 여 toohello 데이터베이스 연결
> * SSMS를 사용하여 테이블 만들기
> * BCP를 사용하여 데이터 대량 로드
> * SSMS를 사용하여 해당 데이터 쿼리
> * 이전 hello 데이터베이스 tooa 복원 [지정 시간 복원](sql-database-recovery-using-backups.md#point-in-time-restore) hello Azure 포털에서

Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이 자습서를 확인 되었는지 설치:
- 최신 버전의 hello [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).
- 최신 버전의 hello [BCP 및 SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433)합니다.

## <a name="log-in-toohello-azure-portal"></a>Azure 포털 toohello에 로그인

Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.

## <a name="create-a-blank-sql-database"></a>빈 SQL 데이터베이스 만들기

Azure SQL Database는 일련의 정의된 [계산 및 저장소 리소스](sql-database-service-tiers.md)를 사용하여 만들어집니다. hello 데이터베이스 내에서 만들어집니다는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) 및는 [Azure SQL 데이터베이스 논리 서버](sql-database-features.md)합니다. 

이러한 단계 toocreate 빈 SQL 데이터베이스를 따릅니다. 

1. Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.

2. 선택 **데이터베이스** hello에서 **새로** 선택한 페이지 **SQL 데이터베이스** hello에서 **데이터베이스** 페이지. 

   ![빈 데이터베이스 만들기](./media/sql-database-design-first-database/create-empty-database.png)

3. Hello 이미지 앞에 표시 된 대로 hello SQL 데이터베이스에 대 한 양식을 사용 hello 다음 정보를 입력 합니다.   

   | 설정       | 제안 값 | 설명 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **데이터베이스 이름** | mySampleDatabase | 유효한 데이터베이스 이름은 [데이터베이스 식별자](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)를 참조하세요. | 
   | **구독** | 사용자의 구독  | 구독에 대한 자세한 내용은 [구독](https://account.windowsazure.com/Subscriptions)을 참조하세요. |
   | **리소스 그룹** | myResourceGroup | 유효한 리소스 그룹 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요. |
   | **원본 선택** | 빈 데이터베이스 | 빈 데이터베이스를 만들도록 지정합니다. |

4. 클릭 **서버** toocreate 하 고 새 데이터베이스에 대 한 새 서버를 구성 합니다. Hello 채울 **새 폼 서버** hello 다음 정보로: 

   | 설정       | 제안 값 | 설명 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름** | 전역적으로 고유한 이름 | 유효한 서버 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요. | 
   | **서버 관리자 로그인** | 모든 유효한 이름 | 유효한 로그인 이름은 [데이터베이스 식별자](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)를 참조하세요.|
   | **암호** | 유효한 암호 | 암호가 8 자 이상 있어야 하며 hello 다음 범주 중 세 범주의 문자를 포함 해야 합니다: 대문자, 소문자, 숫자 및 영숫자가 아닌 문자. |
   | **위치**: | 모든 유효한 위치 | 지역에 대한 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요. |

   ![create database-server](./media//sql-database-design-first-database/create-database-server.png)

5. **선택**을 클릭합니다.

6. 클릭 **가격 책정 계층** toospecify hello 서비스 계층과 성능 수준을 새 데이터베이스에 대 한 합니다. 이 자습서에서는 **20 DTU** 및 **250**GB의 저장소를 선택합니다.

   ![create database-s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. **Apply**를 클릭합니다.  

8. 선택 된 **데이터 정렬** hello 빈 데이터베이스에 대 한 (이 자습서에서는 hello 기본값 사용). 데이터 정렬에 대한 자세한 내용은 [데이터 정렬](https://docs.microsoft.com/sql/t-sql/statements/collations)을 참조하세요.

9. 클릭 **만들기** tooprovision hello 데이터베이스입니다. 하나 있으며 toocomplete에 대 한 프로 비전 합니다. 

10. Hello 도구 모음에서 **알림** toomonitor hello 배포 프로세스입니다.

   ![알림](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>서버 수준 방화벽 규칙 만들기

hello SQL 데이터베이스 서비스는 hello 서버 수준 방화벽 규칙은 특정 IP 주소에 대 한 tooopen hello 방화벽을 만들지 않은 toohello 서버나 hello 서버에 있는 모든 데이터베이스를 연결 하지 못하도록 외부 응용 프로그램 및 도구를 방지 하에 방화벽을 만듭니다. 이러한 단계 toocreate에 따라 한 [SQL 데이터베이스 서버 수준 방화벽 규칙](sql-database-firewall-configure.md) 클라이언트의 IP 주소에 대 한 사용자만 IP 주소에 대 한 hello SQL 데이터베이스 방화벽을 통해 외부 연결을 사용 하도록 설정 합니다. 

> [!NOTE]
> SQL Database는 포트 1433을 통해 통신합니다. 회사 네트워크 내부에서 tooconnect을 시도 하는 포트 1433 통한 아웃 바운드 트래픽 네트워크의 방화벽에서 허용 되지 않을 수 있습니다. 이 경우에 IT 부서는 포트 1433을 엽니다 하지 않는 한 tooyour Azure SQL 데이터베이스 서버를 연결할 수 없습니다.
>

1. Hello 배포가 완료 된 후 클릭 **SQL 데이터베이스** hello 왼쪽 메뉴에서 **mySampleDatabase** hello에 **SQL 데이터베이스** 페이지. hello 완벽 하 게 hello 보여 주는 데이터베이스 열리면 프로그램에 대 한 개요 페이지에 정규화 된 서버 이름 (예: **mynewserver20170313.database.windows.net**) 하 고 더 이상의 구성에 대 한 옵션을 제공 합니다. 나중에 사용하기 위해 이 정규화된 서버 이름을 복사합니다.

   > [!IMPORTANT]
   > 이 정규화 된 서버 이름 tooconnect tooyour 서버와 데이터베이스의 후속 빠른 시작 해야합니다.
   > 

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

2. 클릭 **서버 방화벽 설정** hello 이전 그림에 나와 있는 것 처럼 hello 도구 모음입니다. hello **방화벽 설정** hello SQL 데이터베이스 서버에 대 한 페이지가 열립니다. 

   ![서버 방화벽 규칙](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. 클릭 **클라이언트 IP 추가** hello 도구 모음 tooadd에 현재 IP 주소 tooa 새 방화벽 규칙입니다. 방화벽 규칙은 단일 IP 주소 또는 IP 주소의 범위에 1433 포트를 열 수 있습니다.

4. **Save**를 클릭합니다. 서버 수준 방화벽 규칙 hello 논리 서버에 포트 1433을 열지 현재 IP 주소에 대해 만들어집니다.

   ![set server firewall rule](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. 클릭 **확인** hello 다음 닫고 **방화벽 설정** 페이지.

Toohello SQL 데이터베이스 서버와 SQL Server Management Studio 또는 이전에 만든 hello 서버 관리자 계정을 사용 하 여이 IP 주소에서 선택한 다른 도구를 사용 하 여 데이터베이스를 연결할 수 있습니다.

> [!IMPORTANT]
> 기본적으로 액세스 hello SQL 데이터베이스 방화벽을 통해 모든 Azure 서비스에 대해 사용 됩니다. 클릭 **OFF** 모든 Azure 서비스에 대 한이 페이지 toodisable에 있습니다.

## <a name="sql-server-connection-information"></a>SQL 서버 연결 정보

Hello Azure 포털에서에서 Azure SQL 데이터베이스 서버에 대 한 정규화 된 서버 이름을 hello를 가져옵니다. SQL Server Management Studio를 사용 하 여 hello 정규화 된 서버 이름 tooconnect tooyour 서버를 사용 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지. 
3. Hello에 **Essentials** hello 프로그램 데이터베이스에 대 한 Azure 포털 페이지의에서 창 찾아 다음 hello 복사 **서버 이름**합니다.

   ![연결 정보](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-toohello-database-with-ssms"></a>SSMS를 사용 하 여 toohello 데이터베이스 연결

사용 하 여 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish 연결 tooyour Azure SQL 데이터베이스 서버입니다.

1. SQL Server Management Studio를 엽니다.

2. Hello에 **tooServer 연결** 대화 상자에 hello 다음 정보를 입력 합니다.

   | 설정       | 제안 값 | 설명 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | 서버 유형 | 데이터베이스 엔진 | 이 값은 필수입니다. |
   | 서버 이름 | hello 정규화 된 서버 이름 | hello 이름은 해야 다음과 같이: **mynewserver20170313.database.windows.net**합니다. |
   | 인증 | SQL Server 인증 | SQL 인증에는이 자습서에서는 구성 hello 유일한 인증 유형입니다. |
   | 로그인 | hello 서버 관리자 계정 | Hello 서버를 만들 때 지정한 hello 계정입니다. |
   | 암호 | 서버 관리자 계정에 대 한 hello 암호 | 이 hello 암호 hello 서버를 만들 때 지정한입니다. |

   ![tooserver 연결](./media/sql-database-connect-query-ssms/connect.png)

3. 클릭 **옵션** hello에 **tooserver 연결** 대화 상자. Hello에 **toodatabase 연결** 섹션에서 입력 **mySampleDatabase** tooconnect toothis 데이터베이스입니다.

   ![toodb 서버에 연결](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. **Connect**를 클릭합니다. SSMS에서 hello 개체 탐색기 창이 열립니다. 

5. 개체 탐색기에서 확장 **데이터베이스** 펼친 다음 **mySampleDatabase** hello 샘플 데이터베이스의 tooview hello 개체입니다.

   ![데이터베이스 개체](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-hello-database"></a>Hello 데이터베이스에서 테이블 만들기 

[Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference)을 사용하여 대학의 학생 관리 시스템을 모델링하는 네 개의 테이블이 있는 데이터베이스 스키마 만들기

- 사람
- 과정
- 학생
- 대학의 학생 관리 시스템을 모델링하는 크레딧

hello 다음 그림에 어떻게 이러한 테이블은 다른 관련된 tooeach 합니다. 이러한 테이블 중 일부는 다른 테이블의 열을 참조합니다. 예를 들어 hello Student 테이블 참조 hello **PersonId** hello의 열 **사람** 테이블입니다. 이 자습서에서는 hello 테이블 어떻게 연구 hello 다이어그램 toounderstand는 관련된 tooone 다른 합니다. 방법을 자세히 배우려면 toocreate 효과적인 데이터베이스 테이블, 참조 [효과적인 데이터베이스 테이블을 만들](https://msdn.microsoft.com/library/cc505842.aspx)합니다. 데이터 형식을 선택하는 방법은 [데이터 형식](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql)을 참조하세요.

> [!NOTE]
> Hello를 사용할 수도 있습니다 [SQL Server Management Studio의 테이블 디자이너](https://msdn.microsoft.com/library/hh272695.aspx) toocreate 및 테이블을 디자인 합니다. 

![테이블 관계](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. 개체 탐색기에서 **mySampleDatabase**를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 클릭합니다. 빈 쿼리 창이 열립니다 tooyour 연결 된 데이터베이스입니다.

2. Hello 쿼리 창에서 다음 데이터베이스의 쿼리 toocreate 4 개의 표 hello를 실행 합니다. 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![테이블 만들기](./media/sql-database-design-first-database/create-tables.png)

3. 사용자가 만든 hello SQL Server Management Studio 개체 탐색기 toosee hello 테이블에서 hello '테이블' 노드를 확장 합니다.

   ![ssms 테이블 생성](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-hello-tables"></a>Hello 테이블로 데이터를 로드 합니다.

1. 라는 폴더를 만들어 **SampleTableData** 다운로드 폴더 toostore 예제 데이터가 데이터베이스에 있습니다. 

2. 마우스 오른쪽 단추로 클릭 hello 다음 연결을 hello에 저장해 **SampleTableData** 폴더입니다. 

   - [SampleCourseData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [SamplePersonData](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [SampleStudentData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [SampleCreditData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. 명령 프롬프트 창을 열고 toohello SampleTableData 폴더를 이동 합니다.

4. 같은 명령 tooinsert 샘플 데이터가 hello 값에 대 한 대체 hello 테이블로 hello 실행 **ServerName**, **DatabaseName**, **UserName**, 및 **암호** hello 값이 사용자 환경에 대 한 합니다.
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

이제 이전에 만든 hello 테이블에 샘플 데이터를 로드 해야 합니다.

## <a name="query-data"></a>쿼리 데이터

Hello 쿼리 tooretrieve 정보 hello 데이터베이스 테이블에서 다음을 실행 합니다. 참조 [SQL 쿼리 작성](https://technet.microsoft.com/library/bb264565.aspx) toolearn SQL 쿼리를 작성 하는 방법에 대 한 자세한 합니다. hello 첫 번째 쿼리는 모든 4 개의 테이블 toofind 모든 hello 학생 알게 하 여 ' Dominick 서 ' 75% 보다 높은 성적이 클래스에 있는 조인 합니다. hello 두 번째 쿼리는 모든 4 개의 테이블을 조인 하 고 ' Noe 콜맨 ' 등록 되지 않은 모든 과정을 찾습니다.

1. SQL Server Management Studio 쿼리 창에서 다음 쿼리는 hello를 실행 합니다.

   ```sql 
   -- Find hello students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. SQL Server Management Studio 쿼리 창에서 다음 쿼리를 실행합니다.

   ```sql
   -- Find all hello courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>데이터베이스 tooa 이전 시점으로 복원

실수로 테이블을 삭제한 경우를 가정해 보겠습니다. 이런 경우는 쉽게 복구할 수 없는 경우입니다. Azure SQL 데이터베이스 toogo 백 tooany 지점 hello의 지정 시간으로 마지막 too35 일을 있으며 시간 tooa 새 데이터베이스의 지정 된이 위치에 복원 합니다. 수 있습니다.이 데이터베이스 toorecover 삭제 된 데이터. hello 다음 단계 hello 샘플 데이터베이스 tooa 지점 전에 복원 hello 테이블이 추가 되었습니다.

1. 데이터베이스에 대 한 hello SQL 데이터베이스 페이지에서 클릭 **복원** hello 도구 모음입니다. hello **복원** 페이지가 열립니다.

   ![복원](./media/sql-database-design-first-database/restore.png)

2. Hello 채울 **복원** 폼 hello 필요한 정보로:
    * 데이터베이스 이름: 데이터베이스 이름을 입력합니다. 
    * 시점: 선택 hello **시점에서** hello 복원 양식에 탭 
    * 복원 지점을: hello 데이터베이스를 변경 하기 전에 발생 하는 시간을 선택 합니다.
    * 대상 서버: 데이터베이스를 복원할 때는 이 값을 변경할 수 없습니다. 
    * 탄력적 데이터베이스 풀: **없음** 선택  
    * 가격 책정 계층: **20DTU** 및 **250**GB의 저장소를 선택합니다.

   ![복원 시점](./media/sql-database-design-first-database/restore-point.png)

3. 클릭 **확인** toorestore hello 데이터베이스 너무[복원 tooa 지정 시간으로](sql-database-recovery-using-backups.md#point-in-time-restore) hello 테이블 추가 되기 전에 합니다. Hello에 중복 된 데이터베이스를 만듭니다 데이터베이스 tooa 다른 지정 시간으로 복원 하면가 지정 하는 hello 지정 시간 기준 hello 원래 데이터베이스와 같은 서버에 대 한 hello 보존 기간 내으로 프로그램 [서비스 계층](sql-database-service-tiers.md)합니다.

## <a name="next-steps"></a>다음 단계 
이 자습서에서는 기본적인 데이터베이스 작업 같은 데이터베이스와 테이블을 만들 배운, 로드 및 데이터를 쿼리하고 hello 데이터베이스 tooa 이전 지정 시간으로 복원 합니다. 다음 방법에 대해 알아보았습니다.
> [!div class="checklist"]
> * 데이터베이스 만들기
> * 방화벽 규칙 설정
> * 사용 하 여 toohello 데이터베이스 연결 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)
> * 테이블 만들기
> * 데이터 대량 로드
> * 해당 데이터 쿼리
> * SQL 데이터베이스를 사용 하 여 hello 데이터베이스 tooa 이전 특정 시점 복원 [지정 시간 복원](sql-database-recovery-using-backups.md#point-in-time-restore) 기능

Visual Studio 및 C#을 사용 하 여 데이터베이스를 디자인 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
>[Azure SQL Database 설계 및 C#과 ADO.NET에 연결T](sql-database-design-first-database-csharp.md)
