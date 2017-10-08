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
# <a name="get-started-with-transparent-data-encryption-tde"></a>투명한 데이터 암호화(TDE) 시작
> [!div class="op_single_selector"]
> * [보안 개요](sql-data-warehouse-overview-manage-security.md)
> * [인증](sql-data-warehouse-authentication.md)
> * [암호화(포털)](sql-data-warehouse-encryption-tde.md)
> * [암호화(T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>필요한 권한
투명 한 데이터 암호화 (TDE) tooenable 관리자나 hello dbmanager 역할의 멤버 여야 합니다.

## <a name="enabling-encryption"></a>암호화 설정
SQL 데이터 웨어하우스에 대 한 이러한 단계 tooenable TDE를 수행 합니다.

1. Toohello 연결 *마스터* hello 서버 관리자 또는 hello의 멤버인 로그인을 사용 하는 hello 데이터베이스를 호스팅하는 데이터베이스 **dbmanager** hello master 데이터베이스의 역할
2. 다음 문을 tooencrypt hello 데이터베이스 hello를 실행 합니다.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>암호화 비활성화
SQL 데이터 웨어하우스에 대 한 이러한 단계 toodisable TDE를 수행 합니다.

1. Toohello 연결 *마스터* 관리자 이거나 hello의 구성원 인 로그인을 사용 하 여 데이터베이스 **dbmanager** hello master 데이터베이스의 역할
2. 다음 문을 tooencrypt hello 데이터베이스 hello를 실행 합니다.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> 일시 중지 된 SQL 데이터 웨어하우스 toohello TDE 설정을 변경 하기 전에 다시 시작 되어야 합니다.
> 
> 

## <a name="verifying-encryption"></a>암호화 확인
SQL 데이터 웨어하우스에 대 한 tooverify 암호화 상태는 아래의 hello 단계를 수행 합니다.

1. Toohello 연결 *마스터* 또는 인스턴스 데이터베이스 관리자 또는 hello의 멤버인 로그인을 사용 하 여 **dbmanager** hello master 데이터베이스의 역할
2. 다음 문을 tooencrypt hello 데이터베이스 hello를 실행 합니다.

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

```1```의 결과는 암호화된 데이터베이스를 나타내고 ```0```은(는) 암호화되지 않은 데이터베이스를 나타냅니다.

## <a name="encryption-dmvs"></a>암호화 DMV
* [sys.databases][sys.databases] 
* [sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
