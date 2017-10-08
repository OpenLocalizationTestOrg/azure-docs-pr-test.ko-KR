---
title: "aaaThreat 검색-Azure SQL 데이터베이스 | Microsoft Docs"
description: "위협 검색 잠재적 보안 위협을 toohello 데이터베이스 비정상 데이터베이스 작업을 검색 합니다."
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a>SQL Database 위협 감지

SQL 위협 요소 탐지 한 잠재적으로 위험한 시도 tooaccess 또는 악용 데이터베이스 비정상적인 작업을 검색 합니다.

## <a name="overview"></a>개요

SQL 위협 요소 탐지 새 고객 toodetect 있고 비정상적인 활동에서 보안 경고를 제공 하 여 발생 하는 대로 toopotential 위협 응답을 보안 계층을 제공 합니다.  사용자는 의심스러운 데이터베이스 활동, 잠재적 취약성 및 SQL 삽입 공격은 물론 비정상적인 데이터베이스 액세스 패턴에 대한 경고를 받게 됩니다. SQL 위협 요소 탐지 경고의 의심 스러운 활동 세부 정보를 제공 및 방법에 대 한 작업을 권장 tooinvestigate hello 위협을 완화 합니다. 사용자가 사용 하 여 hello 의심 스러운 이벤트를 탐색할 수 [SQL 데이터베이스 감사](sql-database-auditing.md) 는 시도 tooaccess에서 발생 한 경우 toodetermine 위반를 주거나 이들을 착취 hello 데이터베이스의에서 데이터. 위협 요소 탐지 하면 간단한 tooaddress 잠재적인 위협 toohello 데이터베이스 없이 hello 필요 toobe 보안 전문가 또는 시스템 모니터링 하는 고급 보안을 관리 합니다.

예를 들어 SQL 주입 hello 일반적인 웹 응용 프로그램 보안 문제에 hello 인터넷을 사용 하는 tooattack 데이터 기반 응용 프로그램 중 하나입니다. 공격자가 활용 응용 프로그램 취약점 tooinject 악의적인 SQL 문을 응용 프로그램 입력 필드에 졌는 지 또는 hello 데이터베이스에서 데이터를 수정 합니다.

경고를 통합 하는 SQL 위협 요소 탐지 [Azure 보안 센터](https://azure.microsoft.com/en-us/services/security-center/), 이며 각 보호 된 SQL 데이터베이스 서버 hello 동일 가격에서 $15/노드/월, SQL 보호 된 각 위치에서 Azure 보안 센터 표준 계층으로 청구 됩니다 데이터베이스 서버는 하나의 노드만으로 간주 됩니다. Tootry 초대 아웃에 대 한 일 동안 무료로 합니다. 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a>위협 요소 탐지 hello Azure 포털에서에서 데이터베이스에 대 한 설정
1. 시작 hello Azure 포털에서 [https://portal.azure.com](https://portal.azure.com)합니다.
2. Hello toomonitor 사용할 SQL 데이터베이스의 구성 블레이드에서 toohello 이동 합니다. Hello 설정 블레이드에서 선택 **감사 및 위협 요소 탐지**합니다. 
    ![탐색 창][1]
3. Hello에 **감사 및 위협 요소 탐지** 구성 블레이드 turn **ON** 감사 hello 위협 검색 설정이 표시 됩니다.
  
    ![탐색 창][2]
4. 위협 감지를 **켭니다**
5. 검색 비정상 데이터베이스 작업에 대해 보안 경고를 받을 전자 메일의 hello 목록을 구성 합니다.
6. 클릭 **저장** hello에 **감사 및 위협 검색** 블레이드 toosave hello 신규 또는 업데이트 된 감사 및 위협 검색 설정 합니다.
       
    ![탐색 창][3]

## <a name="set-up-threat-detection-using-powershell"></a>PowerShell을 사용하여 위협 감지 설정

스크립트 예제는 [PowerShell을 사용하여 감사 및 위협 감지 구성](scripts/sql-database-auditing-and-threat-detection-powershell.md)을 참조하세요.

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a>의심스러운 이벤트 감지 시 비정상적인 데이터베이스 활동 살펴보기
1. 비정상적인 데이터베이스 활동이 감지되면 이메일 알림을 받게 됩니다. <br/>
   hello 전자 메일 hello 비정상적인 활동, 데이터베이스 이름, 서버 이름, 응용 프로그램 이름 및 hello 이벤트 시간의 hello 특성을 포함 하 여 hello 의심 되는 보안 이벤트를 처리 정보를 제공 합니다. 또한 hello 전자 메일 가능한 원인에 정보를 제공 합니다 및 권장 동작 tooinvestigate 않으며 hello 잠재적인 위협 toohello 데이터베이스 완화 됩니다.<br/>
     
    ![탐색 창][4]
2. hello 전자 메일 경고는 직접 링크 toohello SQL 감사 로그를 포함 합니다. Azure 포털 및 열립니다 hello SQL 감사 레코드 hello 의심 스러운 이벤트의 hello 시간대이 링크를 실행 하는 hello를 클릭합니다. 실행 된 toofind hello SQL 문을 쉽게 만드는 hello 의심 스러운 데이터베이스 작업에 대 한 자세한 내용은 감사 레코드 tooview 클릭 (액세스 한 사용자, 했다는 것 언제) hello 이벤트 올 바르 거 나 악성 했는지 확인 하 고 (예: 응용 프로그램 tooSQL 주입 취약점을 악용, 등 중요 한 데이터 위반 하는 다른 사용자).<br/>
   ![탐색 창][5]


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a>탐색 hello Azure 포털에서에서 데이터베이스에 대 한 위협을 감지 경고

SQL Database 위협 감지는 경고를 [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/)와 통합합니다. 내에서 발생 하는 위협 상태의 Azure 포털 트랙 hello hello hello 데이터베이스 블레이드 라이브 SQL 보안 타일입니다. 

   ![탐색 창][6]
   
1. Hello SQL 보안 타일을 클릭 하면 hello Azure 보안 센터 경고 블레이드를 시작 하 고 활성 SQL 위협이 hello 데이터베이스에서 검색의 개요를 제공 합니다. 

  ![탐색 창][7]

2. 특정 경고를 클릭하면 이 위협을 조사하고 향후 위협을 수정하기 위한 추가 세부 정보 및 조치가 제공됩니다.

  ![탐색 창][8]


## <a name="next-steps"></a>다음 단계

* 위협 요소 탐지에 대 한 자세한 정보, hello 방문 [Azure 블로그](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/) 
* [Azure SQL Database 감사](sql-database-auditing.md)에 대한 자세한 정보
* [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)에 대한 자세한 정보
* 가격 책정에 대 한 자세한 내용은 hello를 참조 하십시오 [SQL 데이터베이스 가격 페이지](https://azure.microsoft.com/en-us/pricing/details/sql-database/)  
* PowerShell 스크립트 예제는 [PowerShell을 사용하여 감사 및 위협 감지 구성](scripts/sql-database-auditing-and-threat-detection-powershell.md)을 참조하세요.



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


