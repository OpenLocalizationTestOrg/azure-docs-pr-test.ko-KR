---
title: "SQL Data Warehouse의 투명한 데이터 암호화(T-SQL) | Microsoft Docs"
description: "SQL Data Warehouse의 TDE(투명한 데이터 암호화)(T-SQL)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 74c9032aababdce91ed617cd7a4c628915b42504
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="1bd48-103">투명한 데이터 암호화(TDE) 시작</span><span class="sxs-lookup"><span data-stu-id="1bd48-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1bd48-104">보안 개요</span><span class="sxs-lookup"><span data-stu-id="1bd48-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="1bd48-105">인증</span><span class="sxs-lookup"><span data-stu-id="1bd48-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="1bd48-106">암호화(포털)</span><span class="sxs-lookup"><span data-stu-id="1bd48-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="1bd48-107">암호화(T-SQL)</span><span class="sxs-lookup"><span data-stu-id="1bd48-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="1bd48-108">필요한 권한</span><span class="sxs-lookup"><span data-stu-id="1bd48-108">Required Permssions</span></span>
<span data-ttu-id="1bd48-109">TDE(투명한 데이터 암호화)를 사용하려면 관리자 또는 dbmanager 역할의 멤버여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd48-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="1bd48-110">암호화 설정</span><span class="sxs-lookup"><span data-stu-id="1bd48-110">Enabling Encryption</span></span>
<span data-ttu-id="1bd48-111">SQL Data Warehouse에 대한 TDE를 사용하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="1bd48-111">Follow these steps to enable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="1bd48-112">마스터 데이터베이스에서 *dbmanager* 역할의 관리자 또는 멤버인 로그인을 사용하여 데이터베이스를 호스팅하는 서버의 **마스터** 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="1bd48-112">Connect to the *master* database on the server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="1bd48-113">다음 문을 실행하여 데이터베이스를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd48-113">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="1bd48-114">암호화 비활성화</span><span class="sxs-lookup"><span data-stu-id="1bd48-114">Disabling Encryption</span></span>
<span data-ttu-id="1bd48-115">SQL Data Warehouse에 대한 TDE를 사용하지 않으려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="1bd48-115">Follow these steps to disable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="1bd48-116">마스터 데이터베이스에서 *dbmanager* 역할의 관리자 또는 멤버인 로그인을 사용하여 **마스터** 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="1bd48-116">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="1bd48-117">다음 문을 실행하여 데이터베이스를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd48-117">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="1bd48-118">TDE 설정을 변경하기 전에 일시 중지된 SQL Data Warehouse를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd48-118">A paused SQL Data Warehouse must be resumed before making changes to the TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="1bd48-119">암호화 확인</span><span class="sxs-lookup"><span data-stu-id="1bd48-119">Verifying Encryption</span></span>
<span data-ttu-id="1bd48-120">SQL 데이터 웨어하우스에 대한 암호화 상태를 확인하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="1bd48-120">To verify encryption status for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="1bd48-121">마스터 데이터베이스에서 *dbmanager* 역할의 관리자 또는 멤버인 로그인을 사용하여 **마스터** 또는 인스턴스 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="1bd48-121">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="1bd48-122">다음 문을 실행하여 데이터베이스를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd48-122">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="1bd48-123">```1```의 결과는 암호화된 데이터베이스를 나타내고 ```0```은(는) 암호화되지 않은 데이터베이스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1bd48-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="1bd48-124">암호화 DMV</span><span class="sxs-lookup"><span data-stu-id="1bd48-124">Encryption DMVs</span></span>
* <span data-ttu-id="1bd48-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="1bd48-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="1bd48-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="1bd48-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
