---
title: "스트레치 데이터베이스 TSQL-Azure에 대 한 투명 한 데이터 암호화 aaaEnable | Microsoft Docs"
description: "Azure TSQL에서 SQL Server Stretch Database에 대해 TDE(투명한 데이터 암호화)를 사용하도록 설정"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="95214-103">Azure에서 Stretch Database에 대해 TDE(투명한 데이터 암호화)를 사용하도록 설정(Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="95214-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95214-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="95214-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="95214-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="95214-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="95214-106">투명 한 데이터 암호화 (TDE)는 변경 내용을 toohello 필요 없이 실시간 암호화 및 hello 데이터베이스, 연결 된 백업 및 트랜잭션 로그 파일에 대 한 암호 해독을 수행 하 여 악의적인 활동의 hello 위협 으로부터 보호 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="95214-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="95214-107">TDE 키 호출된 hello 대칭 데이터베이스 암호화 키를 사용 하 여 전체 데이터베이스의 hello 저장소를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="95214-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="95214-108">hello 데이터베이스 암호화 키는 기본 제공 서버 인증서로 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95214-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="95214-109">hello 기본 제공 서버 인증서는 각 Azure 서버에 대해 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="95214-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="95214-110">Microsoft는 적어도 90일마다 이러한 인증서를 자동으로 회전합니다.</span><span class="sxs-lookup"><span data-stu-id="95214-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="95214-111">TDE에 대한 일반적인 설명은 [투명한 데이터 암호화(TDE)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95214-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="95214-112">암호화 설정</span><span class="sxs-lookup"><span data-stu-id="95214-112">Enabling Encryption</span></span>
<span data-ttu-id="95214-113">TDE tooenable hello 스트레치 사용 SQL Server 데이터베이스에서 마이그레이션된 데이터를 저장 하는 Azure 데이터베이스에 대 한 작업을 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95214-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="95214-114">Toohello 연결 *마스터* hello Azure 서버 호스팅 hello 데이터베이스 관리자 또는 hello의 멤버인 로그인을 사용 하는 데이터베이스 **dbmanager** hello master 데이터베이스의 역할</span><span class="sxs-lookup"><span data-stu-id="95214-114">Connect toohello *master* database on hello Azure server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="95214-115">다음 문을 tooencrypt hello 데이터베이스 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95214-115">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="95214-116">암호화 비활성화</span><span class="sxs-lookup"><span data-stu-id="95214-116">Disabling Encryption</span></span>
<span data-ttu-id="95214-117">TDE toodisable hello 스트레치 사용 SQL Server 데이터베이스에서 마이그레이션된 데이터를 저장 하는 Azure 데이터베이스에 대 한 작업을 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95214-117">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="95214-118">Toohello 연결 *마스터* 관리자 이거나 hello의 구성원 인 로그인을 사용 하 여 데이터베이스 **dbmanager** hello master 데이터베이스의 역할</span><span class="sxs-lookup"><span data-stu-id="95214-118">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="95214-119">다음 문을 tooencrypt hello 데이터베이스 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95214-119">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="95214-120">암호화 확인</span><span class="sxs-lookup"><span data-stu-id="95214-120">Verifying Encryption</span></span>
<span data-ttu-id="95214-121">tooverify 암호화 상태 hello 스트레치 사용 SQL Server 데이터베이스에서 마이그레이션된 데이터를 저장 하는 Azure 데이터베이스에 대 한 작업을 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95214-121">tooverify encryption status for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="95214-122">Toohello 연결 *마스터* 또는 인스턴스 데이터베이스 관리자 또는 hello의 멤버인 로그인을 사용 하 여 **dbmanager** hello master 데이터베이스의 역할</span><span class="sxs-lookup"><span data-stu-id="95214-122">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="95214-123">다음 문을 tooencrypt hello 데이터베이스 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95214-123">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="95214-124">```1```의 결과는 암호화된 데이터베이스를 나타내고 ```0```은(는) 암호화되지 않은 데이터베이스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95214-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[투명한 데이터 암호화(TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
