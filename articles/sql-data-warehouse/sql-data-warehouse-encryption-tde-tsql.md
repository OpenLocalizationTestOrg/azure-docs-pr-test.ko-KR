---
title: "SQL 데이터 웨어하우스 (T-SQL)의 데이터 암호화 aaaTransparent | Microsoft Docs"
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
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="4ef01-103">투명한 데이터 암호화(TDE) 시작</span><span class="sxs-lookup"><span data-stu-id="4ef01-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ef01-104">보안 개요</span><span class="sxs-lookup"><span data-stu-id="4ef01-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="4ef01-105">인증</span><span class="sxs-lookup"><span data-stu-id="4ef01-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="4ef01-106">암호화(포털)</span><span class="sxs-lookup"><span data-stu-id="4ef01-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="4ef01-107">암호화(T-SQL)</span><span class="sxs-lookup"><span data-stu-id="4ef01-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="4ef01-108">필요한 권한</span><span class="sxs-lookup"><span data-stu-id="4ef01-108">Required Permssions</span></span>
<span data-ttu-id="4ef01-109">투명 한 데이터 암호화 (TDE) tooenable 관리자나 hello dbmanager 역할의 멤버 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ef01-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="4ef01-110">암호화 설정</span><span class="sxs-lookup"><span data-stu-id="4ef01-110">Enabling Encryption</span></span>
<span data-ttu-id="4ef01-111">SQL 데이터 웨어하우스에 대 한 이러한 단계 tooenable TDE를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ef01-111">Follow these steps tooenable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="4ef01-112">Toohello 연결 *마스터* hello 서버 관리자 또는 hello의 멤버인 로그인을 사용 하는 hello 데이터베이스를 호스팅하는 데이터베이스 **dbmanager** hello master 데이터베이스의 역할</span><span class="sxs-lookup"><span data-stu-id="4ef01-112">Connect toohello *master* database on hello server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="4ef01-113">다음 문을 tooencrypt hello 데이터베이스 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ef01-113">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="4ef01-114">암호화 비활성화</span><span class="sxs-lookup"><span data-stu-id="4ef01-114">Disabling Encryption</span></span>
<span data-ttu-id="4ef01-115">SQL 데이터 웨어하우스에 대 한 이러한 단계 toodisable TDE를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ef01-115">Follow these steps toodisable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="4ef01-116">Toohello 연결 *마스터* 관리자 이거나 hello의 구성원 인 로그인을 사용 하 여 데이터베이스 **dbmanager** hello master 데이터베이스의 역할</span><span class="sxs-lookup"><span data-stu-id="4ef01-116">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="4ef01-117">다음 문을 tooencrypt hello 데이터베이스 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ef01-117">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="4ef01-118">일시 중지 된 SQL 데이터 웨어하우스 toohello TDE 설정을 변경 하기 전에 다시 시작 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ef01-118">A paused SQL Data Warehouse must be resumed before making changes toohello TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="4ef01-119">암호화 확인</span><span class="sxs-lookup"><span data-stu-id="4ef01-119">Verifying Encryption</span></span>
<span data-ttu-id="4ef01-120">SQL 데이터 웨어하우스에 대 한 tooverify 암호화 상태는 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ef01-120">tooverify encryption status for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="4ef01-121">Toohello 연결 *마스터* 또는 인스턴스 데이터베이스 관리자 또는 hello의 멤버인 로그인을 사용 하 여 **dbmanager** hello master 데이터베이스의 역할</span><span class="sxs-lookup"><span data-stu-id="4ef01-121">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="4ef01-122">다음 문을 tooencrypt hello 데이터베이스 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ef01-122">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="4ef01-123">```1```의 결과는 암호화된 데이터베이스를 나타내고 ```0```은(는) 암호화되지 않은 데이터베이스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4ef01-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="4ef01-124">암호화 DMV</span><span class="sxs-lookup"><span data-stu-id="4ef01-124">Encryption DMVs</span></span>
* <span data-ttu-id="4ef01-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="4ef01-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="4ef01-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="4ef01-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
