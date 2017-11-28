---
title: "aaaConnect tooAzure SQL 데이터 웨어하우스 sqlcmd | Microsoft Docs"
description: "[Sqlcmd] [sqlcmd] 명령줄 유틸리티 tooconnect tooand 쿼리 Azure SQL 데이터 웨어하우스를 사용 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="a8d0e-103">Sqlcmd를 사용 하 여 데이터 웨어하우스 tooSQL 연결</span><span class="sxs-lookup"><span data-stu-id="a8d0e-103">Connect tooSQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8d0e-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="a8d0e-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="a8d0e-105">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="a8d0e-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="a8d0e-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a8d0e-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="a8d0e-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="a8d0e-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="a8d0e-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="a8d0e-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="a8d0e-109">사용 하 여 [sqlcmd] [ sqlcmd] 명령줄 유틸리티 tooconnect tooand Azure SQL 데이터 웨어하우스를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-109">Use [sqlcmd][sqlcmd] command-line utility tooconnect tooand query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="a8d0e-110">1. 연결</span><span class="sxs-lookup"><span data-stu-id="a8d0e-110">1. Connect</span></span>
<span data-ttu-id="a8d0e-111">tooget 시작 [sqlcmd][sqlcmd]hello 명령 프롬프트를 열고을 입력 **sqlcmd** 다음 SQL 데이터 웨어하우스 데이터베이스에 대 한 hello 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-111">tooget started with [sqlcmd][sqlcmd], open hello command prompt and enter **sqlcmd** followed by hello connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="a8d0e-112">hello 연결 문자열 hello 매개 변수 뒤에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-112">hello connection string requires hello following parameters:</span></span>

* <span data-ttu-id="a8d0e-113">**서버 (-S):** 서버 hello 형태로 `<`서버 이름`>`. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="a8d0e-113">**Server (-S):** Server in hello form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="a8d0e-114">**데이터베이스(-D):** 데이터베이스 이름</span><span class="sxs-lookup"><span data-stu-id="a8d0e-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="a8d0e-115">**따옴표 붙은 식별자를 사용 하도록 설정 (-I):** 따옴표 붙은 식별자 사용된 tooconnect tooa SQL 데이터 웨어하우스 인스턴스에 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled tooconnect tooa SQL Data Warehouse instance.</span></span>

<span data-ttu-id="a8d0e-116">SQL Server 인증 toouse tooadd hello에 대 한 사용자 이름/암호 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-116">toouse SQL Server Authentication, you need tooadd hello username/password parameters:</span></span>

* <span data-ttu-id="a8d0e-117">**사용자 (-U):** hello 형태로 서버 사용자 `<`사용자`>`</span><span class="sxs-lookup"><span data-stu-id="a8d0e-117">**User (-U):** Server user in hello form `<`User`>`</span></span>
* <span data-ttu-id="a8d0e-118">**암호 (-P):** hello 사용자와 연결 된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-118">**Password (-P):** Password associated with hello user.</span></span>

<span data-ttu-id="a8d0e-119">예를 들어 연결 문자열 hello 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-119">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="a8d0e-120">toouse Azure Active Directory 통합 인증을 tooadd hello Azure Active Directory 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-120">toouse Azure Active Directory Integrated authentication, you need tooadd hello Azure Active Directory parameters:</span></span>

* <span data-ttu-id="a8d0e-121">**Azure Active Directory 인증(-G):** 인증을 위해 Azure Active Directory를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="a8d0e-122">예를 들어 연결 문자열 hello 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-122">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="a8d0e-123">너무 필요한[Azure Active Directory 인증을 사용 하도록 설정](sql-data-warehouse-authentication.md) tooauthenticate Active Directory를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-123">You need too[enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) tooauthenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="a8d0e-124">2. 쿼리</span><span class="sxs-lookup"><span data-stu-id="a8d0e-124">2. Query</span></span>
<span data-ttu-id="a8d0e-125">연결한 후 hello 인스턴스에 대해 지원 되는 TRANSACT-SQL 문을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-125">After connection, you can issue any supported Transact-SQL statements against hello instance.</span></span>  <span data-ttu-id="a8d0e-126">이 예에서 쿼리는 대화형 모드로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="a8d0e-127">다음 예제에서는 이러한 SQL toosqlcmd 파이핑 또는 hello-Q 옵션을 사용 하 여 일괄 처리 모드에서 쿼리를 실행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-127">These next examples show how you can run your queries in batch mode using hello -Q option or piping your SQL toosqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="a8d0e-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a8d0e-128">Next steps</span></span>
<span data-ttu-id="a8d0e-129">참조 [sqlcmd 설명서] [ sqlcmd] sqlcmd에서 사용할 수 있는 hello 옵션에 대 한 세부 정보에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8d0e-129">See [sqlcmd documentation][sqlcmd] for more about details about hello options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
