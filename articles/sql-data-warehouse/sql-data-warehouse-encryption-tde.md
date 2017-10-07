---
title: "SQL 데이터 웨어하우스 (포털)의 데이터 암호화 aaaTransparent | Microsoft Docs"
description: "SQL Data Warehouse의 TDE(투명한 데이터 암호화)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스에서 투명한 데이터 암호화(TDE) 시작
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
tooenable SQL 데이터 웨어하우스에 대 한 TDE는 아래의 hello 단계를 수행 합니다.

1. Hello에 열기 hello 데이터베이스 [Azure 포털](https://portal.azure.com)
2. 데이터베이스 블레이드에서 hello hello 클릭 **설정을** 단추
3. 선택 hello **투명 한 데이터 암호화** 옵션![][1]
4. 선택 hello **에** 설정![][2]
5. **저장** 선택 
   ![][3]  

## <a name="disabling-encryption"></a>암호화 비활성화
toodisable SQL 데이터 웨어하우스에 대 한 TDE는 아래의 hello 단계를 수행 합니다.

1. Hello에 열기 hello 데이터베이스 [Azure 포털](https://portal.azure.com)
2. 데이터베이스 블레이드에서 hello hello 클릭 **설정을** 단추
3. 선택 hello **투명 한 데이터 암호화** 옵션![][1]
4. 선택 hello **오프** 설정![][4]
5. **저장** 선택 
   ![][5]  

## <a name="encryption-dmvs"></a>암호화 DMV
다음 Dmv는 hello로 암호화를 확인할 수 있습니다.

* [sys.databases]
* [sys.dm_pdw_nodes_database_encryption_keys]

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
