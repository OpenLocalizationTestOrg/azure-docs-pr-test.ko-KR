---
title: "aaaGet은 SQL 데이터 웨어하우스 위협 검색 시작"
description: "위협 검색 tooget 시작 하는 방법"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a>위협 감지 시작
> [!div class="op_single_selector"]
> * [감사](sql-data-warehouse-auditing-overview.md)
> * [위협 감지](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a>개요
위협 검색 잠재적 보안 위협을 toohello 데이터베이스 비정상 데이터베이스 작업을 검색 합니다. 위협 감지는 미리 보기로 제공되며 SQL 데이터 웨어하우스를 지원합니다.

위협 요소 탐지 새 고객 toodetect 있고 비정상적인 활동에서 보안 경고를 제공 하 여 발생 하는 대로 toopotential 위협 응답을 보안 계층을 제공 합니다. 사용자가 사용 하 여 hello 의심 스러운 이벤트를 탐색할 수 [Azure SQL 데이터 웨어하우스 감사](sql-data-warehouse-auditing-overview.md) 는 시도 tooaccess에서 발생 한 경우 toodetermine 위반를 주거나 이들을 착취 hello 데이터 웨어하우스의 데이터에서에서 합니다.
위협 요소 탐지 간단한 tooaddress 잠재적 위협 toohello 데이터 보안 전문가 hello 필요 toobe 없이 웨어하우스 또는 시스템 모니터링 하는 고급 보안을 관리 하면 있습니다.

예를 들어 위협 감지는 잠재적인 SQL 삽입 시도를 나타내는 비정상적인 데이터베이스 활동을 감지합니다. SQL 주입 hello 일반적인 웹 응용 프로그램 보안 문제에 hello 인터넷을 사용 하는 tooattack 데이터 기반 응용 프로그램 중 하나입니다. 공격자가 활용 응용 프로그램 취약점 tooinject 악의적인 SQL 문을 졌는 지 또는 hello 데이터베이스의 데이터 수정에 대 한 응용 프로그램 입력 필드에 합니다.

## <a name="set-up-threat-detection-for-your-database"></a>데이터베이스에 대한 위협 감지 설정
1. 시작 hello Azure 포털에 [https://portal.azure.com](https://portal.azure.com)합니다.
2. SQL 데이터 웨어하우스 toomonitor 원하는 hello의 구성 블레이드에서 toohello 이동 합니다. Hello 설정 블레이드에서 선택 **감사 및 위협 요소 탐지**합니다.
   
    ![탐색 창][1]
3. Hello에 **감사 및 위협 요소 탐지** 구성 블레이드 turn **ON** 감사를 위해 표시 하는 hello 위협 검색 설정 합니다.
   
    ![탐색 창][2]
4. 위협 감지를 **켭니다**
5. 비정상적인 데이터 웨어하우스 작업 검색에 대해 보안 경고를 받을 전자 메일의 hello 목록을 구성 합니다.
6. 클릭 **저장** hello에 **감사 및 위협 검색** 구성 블레이드 toosave hello 신규 또는 업데이트 된 감사 및 위협 검색 정책입니다.
   
    ![탐색 창][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a>의심스러운 이벤트 감지 시 비정상적인 데이터 웨어하우스 활동 살펴보기
1. 비정상적인 데이터베이스 활동이 감지되면 이메일 알림을 받게 됩니다. <br/>
   hello 전자 메일 hello 비정상적인 활동, 데이터베이스 이름, 서버 이름 및 hello 이벤트 시간의 hello 특성을 포함 하 여 hello 의심 되는 보안 이벤트를 처리 정보를 제공 합니다. 또한, 가능한 원인에 정보를 제공 합니다 및 작업 tooinvestigate 권장 하 고 hello 잠재적인 위협 toohello 데이터베이스 완화 합니다.<br/>
   
    ![탐색 창][4]
2. Hello 전자 메일의 hello에서 클릭 **Azure SQL 감사 로그** 링크를 hello Azure 클래식 포털을 시작 하 고 hello 의심 스러운 이벤트의 hello 시간대 hello 관련 된 감사 레코드가 표시 됩니다.
   
    ![탐색 창][5]
3. SQL 문 처럼 hello 데이터베이스 의심 스러운 활동에 대 한 자세한 내용은 hello 감사 레코드 tooview 클릭 실패 이유 및 클라이언트 IP입니다.
   
    ![탐색 창][6]
4. Hello 감사 레코드 블레이드에서 클릭 **Excel에서 열기** tooopen 미리 구성 된 excel 서식 파일 tooimport 및 hello 의심 스러운 이벤트의 hello 시간대 hello 감사 로그의 심층 분석을 실행된 합니다.<br/>
   **참고:** Excel 2010 또는 나중에 파워 쿼리 및 hello **빠른 결합** 설정은 필수입니다.
   
    ![탐색 창][7]
5. tooconfigure hello **빠른 결합** hello에 설정- **파워 쿼리** 리본 탭 **옵션** toodisplay hello 옵션 대화 상자. Hello 개인 정보 섹션을 선택 하 고 hello 두 번째 옵션-'hello 개인 정보 수준을 무시 하 고 잠재적으로 성능 향상'를 선택 합니다.
   
    ![탐색 창][8]
6. tooload SQL 감사 로그 hello 매개 변수가 확인 hello 설정 탭에서 올바르게 설정 하 고 다음 hello '데이터' 리본 선택 hello ' 모두 새로 고침 ' 단추를 클릭 합니다.
   
    ![탐색 창][9]
7. hello에 hello 결과가 표시 **SQL 감사 로그** 시트 발견 되 고 응용 프로그램에서 hello 보안 이벤트의 hello 영향을 완화 하는 hello 비정상적인 활동의 심층 분석 toorun 있습니다.

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
