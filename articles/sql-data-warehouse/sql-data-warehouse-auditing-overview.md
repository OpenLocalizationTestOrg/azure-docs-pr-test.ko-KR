---
title: "Azure SQL 데이터 웨어하우스에 aaaAuditing | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 감사 시작"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스 감사
> [!div class="op_single_selector"]
> * [감사](sql-data-warehouse-auditing-overview.md)
> * [위협 감지](sql-data-warehouse-security-threat-detection.md)
> 
> 

SQL 데이터 웨어하우스 감사 이벤트를 허용 하면 toorecord Azure 저장소 계정에 데이터베이스 tooan 감사 로그에 합니다. 감사는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 비즈니스 문제나 의심스러운 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다. 또한 드릴다운 보고서 및 분석을 위해 SQL Data Warehouse 감사 기능을 Microsoft Power BI와 통합합니다.

감사 도구를 사용 하도록 설정 되 고 toocompliance 표준 준수를 용이 하 게 있지만 규정 준수를 보장 하지는 마십시오. Azure에 대 한 자세한 내용은 해당 지원 표준 준수를 프로그램에서 참조 hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure 보안 센터</a>합니다.

* [데이터베이스 감사 기본 사항]
* [데이터베이스에 대한 감사 설정]
* [감사 로그 및 보고서 분석]

## <a id="subheading-1"></a>Azure SQL 데이터 웨어하우스 데이터베이스 감사 기본 사항
SQL 데이터 웨어하우스 데이터베이스 감사를 사용하여 다음을 수행할 수 있습니다.

* **유지** 합니다. 감사 데이터베이스 작업 toobe의 범주를 정의할 수 있습니다.
* **보고** 합니다. 미리 구성 된 보고서 및 활동 및 이벤트 보고 신속 하 게 시작 하는 대시보드 tooget를 사용할 수 있습니다.
* **분석** 합니다. 의심스러운 이벤트, 특별한 활동 및 추세를 찾을 수 있습니다.

이벤트 범주에 따라 hello에 대 한 감사를 구성할 수 있습니다.

**일반 SQL** 및 **매개 변수가 있는 SQL** 로 분류 되어 수집 된 감사 로그는 hello에 대 한  

* **액세스 toodata**
* **스키마 변경(DDL)**
* **데이터 변경(DML)**
* **계정, 역할 및 사용 권한(DCL)**
* **저장 프로시저**, **로그인** 및 **트랜잭션 관리**.

각 이벤트 범주에 대해 **성공** 및 **실패** 작업의 감사를 따로 구성합니다.

Hello 활동 및 감사 된 이벤트에 대 한 자세한 내용은 참조 hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">감사 로그 형식 참조 (doc 파일 다운로드)</a>합니다.

감사 로그는 Azure 저장소 계정에 저장됩니다. 감사 로그의 보존 기간을 정의할 수 있습니다.

특정 데이터베이스에 대해 또는 기본 서버 정책으로 감사 정책을 정의할 수 있습니다. 기본 서버 감사 정책에는 특정 재정의 데이터베이스 감사 정책을 정의 되어 있지 않은 서버에 tooall 데이터베이스 적용 됩니다.

감사를 설정하기 전에 ["하위 클라이언트"](sql-data-warehouse-auditing-downlevel-clients.md)를 사용 중인지 여부를 점검합니다.

## <a id="subheading-2"></a>데이터베이스에 대한 감사 설정
1. Hello 시작 <a href="https://portal.azure.com" target="_blank">Azure 포털</a>합니다.
2. Toohello 이동 **설정을** hello tooaudit 원하는 SQL 데이터 웨어하우스의 블레이드에서 합니다. Hello에 **설정** 블레이드를 **감사 및 위협 검색**합니다.
   
    ![][1]
3. 다음으로 hello를 클릭 하 여 감사를 활성화 **ON** 단추입니다.
   
    ![][3]
4. 감사 구성 블레이드 hello, 선택 **저장소 세부 정보** tooopen hello 감사 로그 저장소 블레이드입니다. Hello 로그를 저장할 Azure 저장소 계정 및 hello 선택 보존 기간입니다. 
>[!TIP]
>사용 하 여 hello hello 최대한 활용 하는 모든 감사 데이터베이스 tooget hello에 대 한 동일한 저장소 계정을 미리 구성 된 서식 파일을 보고 합니다.
   
    ![][4]
5. Hello 클릭 **확인** 단추 toosave hello 저장소 세부 정보 구성 합니다.
6. **이벤트를 로깅 하나씩**, 클릭 **성공** 및 **오류** toolog 모든 이벤트를 하거나 개별 이벤트 범주를 선택 합니다.
7. 데이터베이스에 대 한 감사를 구성 하는 경우에 데이터 감사 올바로 캡처 프로그램 클라이언트 tooensure의 tooalter hello 연결 문자열을 할 수 있습니다. Hello 확인 [hello 연결 문자열에서 서버 FDQN 수정](sql-data-warehouse-auditing-downlevel-clients.md) 하위 수준 클라이언트 연결에 대 한 항목입니다.
8. **확인**을 클릭합니다.

## <a id="subheading-3"></a>감사 로그 및 보고서 분석
감사 로그는 저장소 테이블 컬렉션에 집계 되는 **SQLDBAuditLogs** hello 설치 도중에 선택한 Azure 저장소 계정에에서는 접두사입니다. <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure 저장소 탐색기</a>와 같은 도구를 사용하여 로그 파일을 볼 수 있습니다.

미리 구성 된 대시보드 보고서 서식 파일은 사용할 수는 <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">Excel 스프레드시트를 다운로드할 수 있는</a> toohelp 로그 데이터를 신속 하 게 분석 합니다. Excel 2013 이상 및 다운로드할 수 있는 파워 쿼리 필요한 감사 로그에 toouse hello 템플릿을 <a href="http://www.microsoft.com/download/details.aspx?id=39379">여기</a>합니다.

hello 서식 파일에는 가상의 예제 데이터, 및를 설정할 수 있습니다 파워 쿼리 tooimport 감사 로그 Azure 저장소 계정에서 직접 합니다.

## <a id="subheading-4"></a>Storage 키 다시 생성
프로덕션 환경에서 저장소 키를 주기적으로 가능성이 toorefresh 됩니다. 키를 새로 고치거 나, toosave hello 정책이 필요 합니다. hello 프로세스는 다음과 같습니다.

1. 위에서 설명한 감사 섹션 hello 설치 프로그램의 구성 블레이드에서 감사 hello에서 전환 hello **저장소 액세스 키** 에서 *기본* 너무*보조* 및  **저장**합니다.

   ![][4]
2. 이동 toohello 저장소 구성 블레이드 및 **다시 생성** hello *기본 액세스 키*합니다.
3. 감사 구성 블레이드, 스위치 hello toohello 돌아가서 **저장소 액세스 키** 에서 *보조* 너무*기본* 누릅니다 **저장**합니다.
4. 로 돌아가려면 toohello 저장소 UI 및 **다시 생성** hello *보조 액세스 키* (hello에 대 한 준비 과정으로 다음 키 새로 고침 주기 합니다.

## <a id="subheading-5"></a>Automation(PowerShell/REST API)
Hello 다음 자동화 도구를 사용 하 여 감사 Azure SQL 데이터 웨어하우스를 구성할 수 있습니다.

* **PowerShell cmdlet**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

<!--Anchors-->
[데이터베이스 감사 기본 사항]: #subheading-1
[데이터베이스에 대한 감사 설정]: #subheading-2
[감사 로그 및 보고서 분석]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy