---
title: "스트레치 데이터베이스-Azure에 대 한 투명 한 데이터 암호화 aaaEnable | Microsoft Docs"
description: "Azure에서 SQL Server Stretch Database에 대해 TDE(투명한 데이터 암호화)를 사용하도록 설정"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Azure에서 Stretch Database에 대해 TDE(투명한 데이터 암호화)를 사용하도록 설정
> [!div class="op_single_selector"]
> * [Azure 포털](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

투명 한 데이터 암호화 (TDE)는 변경 내용을 toohello 필요 없이 실시간 암호화 및 hello 데이터베이스, 연결 된 백업 및 트랜잭션 로그 파일에 대 한 암호 해독을 수행 하 여 악의적인 활동의 hello 위협 으로부터 보호 응용 프로그램입니다.

TDE 키 호출된 hello 대칭 데이터베이스 암호화 키를 사용 하 여 전체 데이터베이스의 hello 저장소를 암호화 합니다. hello 데이터베이스 암호화 키는 기본 제공 서버 인증서로 보호 됩니다. hello 기본 제공 서버 인증서는 각 Azure 서버에 대해 고유 합니다. Microsoft는 적어도 90일마다 이러한 인증서를 자동으로 회전합니다. TDE에 대한 일반적인 설명은 [투명한 데이터 암호화(TDE)]를 참조하세요.

## <a name="enabling-encryption"></a>암호화 설정
TDE tooenable hello 스트레치 사용 SQL Server 데이터베이스에서 마이그레이션된 데이터를 저장 하는 Azure 데이터베이스에 대 한 작업을 다음 hello지 않습니다.

1. Hello에 열기 hello 데이터베이스 [Azure 포털](https://portal.azure.com)
2. 데이터베이스 블레이드에서 hello hello 클릭 **설정을** 단추
3. 선택 hello **투명 한 데이터 암호화** 옵션![][1]
4. 선택 hello **에** 설정을 선택한 후 **저장**
   ![][2]

## <a name="disabling-encryption"></a>암호화 비활성화
TDE toodisable hello 스트레치 사용 SQL Server 데이터베이스에서 마이그레이션된 데이터를 저장 하는 Azure 데이터베이스에 대 한 작업을 다음 hello지 않습니다.

1. Hello에 열기 hello 데이터베이스 [Azure 포털](https://portal.azure.com)
2. 데이터베이스 블레이드에서 hello hello 클릭 **설정을** 단추
3. 선택 hello **투명 한 데이터 암호화** 옵션
4. 선택 hello **오프** 설정을 선택한 후 **저장**

<!--Anchors-->
[투명한 데이터 암호화(TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
