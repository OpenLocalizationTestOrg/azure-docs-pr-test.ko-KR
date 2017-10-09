---
title: "Azure SQL 데이터베이스에 대 한 튜닝 자동 aaaEnable | Microsoft Docs"
description: "Azure SQL Database에서 쉽게 자동 조정을 사용할 수 있습니다."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a>자동 조정 사용

Azure SQL 데이터베이스는 지속적으로 쿼리를 모니터링 하 고 hello 작업 워크 로드의 성능 tooimprove을 수행할 수 있음을 식별 하는 자동으로 관리 되는 데이터 서비스. 권장 사항을 검토하고 수동으로 적용하거나 Azure SQL Database에서 정정 작업을 자동으로 적용하도록 할 수 있습니다. 이는 **자동 조정 모드**로 알려져 있습니다. 자동 튜닝 hello 서버 또는 hello 데이터베이스 수준에서 사용할 수 있습니다.

## <a name="enable-automatic-tuning-on-server"></a>서버에서 자동 조정 사용

tooenable 자동 튜닝 Azure SQL 데이터베이스 서버에 Azure 포털을 다음 선택에서 toohello 서버를 이동 **자동 튜닝** hello 메뉴에 있습니다. 선택 hello 자동 튜닝 옵션 tooenable 한 선택 **적용**:

![서버](./media/sql-database-automatic-tuning-enable/server.png)

튜닝 옵션 서버에서 자동는 hello 서버에 적용 된 tooall 데이터베이스입니다. 기본적으로 모든 데이터베이스에서 해당 부모 서버 hello 구성을 상속 하지만 재정의 되 고 개별적으로 각 데이터베이스에 대해 지정 된 수 수 있습니다.

## <a name="configure-automatic-tuning-on-database"></a>데이터베이스에서 자동 조정 구성

안녕 tooindividually 하면 각 데이터베이스에서 hello 자동 튜닝 구성을 지정 하는 Azure 포털 수 있습니다.

> [!NOTE]
> hello 일반적인 권장 구성은 toomanage hello 자동 튜닝 서버 수준에서 너무 hello 같은 구성 설정을 모든 데이터베이스에 대해 자동으로 적용할 수 있습니다. Hello 데이터베이스가 동일한 서버 hello에 다른 사용자는 서로 다른 경우 개별 데이터베이스에 자동 조정을 구성 합니다.
>

튜닝 단일 데이터베이스에 자동 tooenable hello Azure 포털에서에서 toohello 데이터베이스 이동 이동한 선택 **자동 튜닝**합니다. Hello 확인란을 선택 하 여 hello 데이터베이스에서 단일 데이터베이스 tooinherit hello 설정을 구성 하거나 데이터베이스에 대 한 hello 구성을 개별적으로 지정할 수 있습니다.

![데이터베이스](./media/sql-database-automatic-tuning-enable/database.png)

적절한 구성을 선택한 후 **적용**을 클릭합니다.

## <a name="next-steps"></a>다음 단계
* 읽기 hello [자동 튜닝 문서](sql-database-automatic-tuning.md) toolearn 자동 조정 및 방법을 파악할 수 성능이 개선 하는 방법에 대 한 자세한 합니다.
* Azure SQL Database 성능 권장 사항에 대한 개요는 [성능 권장 사항](sql-database-advisor.md)을 참조하세요.
* 참조 [Query Performance Insight](sql-database-query-performance.md) toolearn hello 상위 쿼리의 성능에 영향을 확인 하는 방법에 대 한 합니다.
