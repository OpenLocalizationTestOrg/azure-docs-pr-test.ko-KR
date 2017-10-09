---
title: "Azure Portal: SQL Database 동적 데이터 마스킹 | Microsoft Docs"
description: "Tooget은 SQL 데이터베이스 동적 데이터 마스킹 hello Azure 포털에서에서 시작 하는 방법"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a>SQL 데이터베이스 동적 데이터 마스킹 Azure 포털 hello로 시작

이 항목에서는 tooimplement [동적 데이터 마스킹](sql-database-dynamic-data-masking-get-started.md) hello Azure 포털을 사용 합니다. 동적 데이터 마스킹 사용 하 여 구현할 수도 있습니다 [Azure SQL 데이터베이스 cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx) 또는 hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx)합니다.


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 데이터베이스에 대 한 동적 데이터 마스킹 설정
1. 시작 hello Azure 포털에 [https://portal.azure.com](https://portal.azure.com)합니다.
2. 원하는 toomask hello 중요 한 데이터를 포함 하는 hello 데이터베이스의 설정 블레이드에서 toohello 이동 합니다.
3. Hello 클릭 **동적 데이터 마스킹** hello를 시작 하는 타일 **동적 데이터 마스킹** 구성 블레이드입니다.
   
   * Toohello 아래로 스크롤할 수 또는 **작업** 섹션 및 클릭 **동적 데이터 마스킹**합니다.
     
     ![탐색 창](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. Hello에 **동적 데이터 마스킹** 해당 hello 권장 엔진 마스킹에 대 한 플래그가 지정 구성 블레이드 일부 데이터베이스 열에 표시 될 수 있습니다. 주문 tooaccept hello 권장 사항를 클릭 하기만 **마스크 추가** 하나 이상의 열과 마스크를 만들이 열에 대 한 hello 기본 형식을 기반으로 합니다. Hello hello 마스킹 규칙을 클릭 하 고 마스킹 필드 형식 tooa 선택한 다른 형식이 hello를 편집 하 여 마스킹 기능을 변경할 수 있습니다. 수 있는지 tooclick **저장** toosave 설정 합니다.
   
    ![탐색 창](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. tooadd hello hello 위쪽에 있는 데이터베이스의 모든 열에 대 한 마스크 **동적 데이터 마스킹** 구성 블레이드 클릭 **마스크 추가** tooopen hello **마스킹 규칙 추가** 구성 블레이드
   
    ![탐색 창](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. 선택 hello **스키마**, **테이블** 및 **열** toodefine hello 마스킹됩니다 필드를 지정 합니다.
7. 선택 된 **마스킹 필드 형식** hello 중요 한 데이터 마스킹 범주 목록에서 합니다.
   
    ![탐색 창](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. 클릭 **저장** hello 데이터 마스킹 규칙 블레이드 tooupdate hello 마스킹 hello 동적 데이터 마스킹 정책에서에서 규칙의 집합입니다.
9. Hello SQL 사용자나 마스킹에서 제외 해야 있고 toohello 마스크 해제 된 중요 한 데이터를 액세스 하는 AAD id 형식입니다. 세미콜론으로 구분된 사용자 목록이어야 합니다. 관리자 권한으로 사용자 액세스 toohello 원래 마스크 해제 된 데이터를 항상 있어야 한다는 참고 합니다.
   
    ![탐색 창](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > hello SQL 사용자 추가, 응용 프로그램 권한 있는 사용자에 대 한 중요 한 데이터를 표시할 수행할 수 있으므로 응용 프로그램 계층을 hello toomake 또는 AAD id hello 응용 tooquery hello 데이터베이스를 사용 합니다. 이 목록에 최소한의 권한이 있는 사용자 toominimize 노출 hello 중요 한 데이터의 포함 것이 좋습니다.
   > 
   > 
10. 클릭 **저장** hello 데이터 마스킹 블레이드 toosave hello 신규 또는 업데이트 된 마스킹 정책을 구성 합니다.


## <a name="next-steps"></a>다음 단계

* 동적 데이터 마스킹의 개요는 [동적 데이터 마스킹](sql-database-dynamic-data-masking-get-started.md)을 참조하세요.
* 동적 데이터 마스킹 사용 하 여 구현할 수도 있습니다 [Azure SQL 데이터베이스 cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx) 또는 hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx)합니다.
