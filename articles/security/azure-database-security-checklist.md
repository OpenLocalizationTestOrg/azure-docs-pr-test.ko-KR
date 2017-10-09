---
title: "aaaAzure 데이터베이스 보안 검사 목록 | Microsoft Docs"
description: "이 문서에서는 Azure 데이터베이스 보안에 대한 일단의 검사 목록을 제공합니다."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 5e3a69591df3c8508a8707a2d47068342863ce93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-checklist"></a>Azure 데이터베이스 보안 검사 목록

toohelp 보안 향상, Azure 데이터베이스는 여러 기본 제공 보안 컨트롤이 toolimit를 사용 하 고 액세스를 제어할 수 있는 기능이 포함 됩니다.

내용은 다음과 같습니다.

-   Toocreate를 사용 하는 방화벽 [방화벽 규칙](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) IP 주소로 연결을 제한 합니다.
-   Hello Azure 포털에서에서 액세스할 수 있는 서버 수준 방화벽
-   SSMS에서 액세스할 수 있는 데이터베이스 수준 방화벽 규칙
-   보안 연결 문자열을 사용 하 여 보안 연결 tooyour 데이터베이스
-   액세스 관리 사용
-   데이터 암호화.
-   SQL Database 감사
-   SQL Database 위협 검색

## <a name="introduction"></a>소개
클라우드 컴퓨팅 생소 한 toomany 응용 프로그램 사용자, 데이터베이스 관리자 및 프로그래머는 새로운 보안 패러다임에 필요 합니다. 따라서 일부 조직에서는 망설 tooimplement tooperceived 보안 위험 때문에 데이터 관리를 위한 클라우드 인프라 있습니다. 그러나 Microsoft Azure 및 Microsoft Azure SQL 데이터베이스에 기본 제공 되는 hello 보안 기능을 보다 잘 이해를 통해 대부분의 이러한 문제를 완화할 수 수 있습니다.

## <a name="checklist"></a>검사 목록
Hello를 읽는 것이 좋습니다 [Azure 데이터베이스 보안에 대 한 유용한 정보](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices) 문서 이전 tooreviewing이 검사이 목록입니다. Hello에 대 한 유용한 정보를 파악 한 후에이 검사 목록을 최대한 활용할 수 tooget hello 됩니다. 그런 다음이 검사 목록 toomake Azure 데이터베이스 보안에서 hello 중요 한 문제를 해결 했습니다 있는지를 사용할 수 있습니다.


|검사 목록 범주| 설명|
| ------------ | -------- |
|**데이터 보호**||
| <br> 진행 중/전송 중 암호화| <ul><li>[전송 계층 보안](https://docs.microsoft.com/en-us/windows-server/security/tls/transport-layer-security-protocol), 데이터 암호화 toohello 네트워크 정도로 데이터가 이동 하는 경우에 합니다.</li><li>데이터베이스의 hello에 따라 클라이언트에서 보안 통신 해야 [TDS (Tabular Data Stream)](https://msdn.microsoft.com/en-in/library/dd357628.aspx) tls (전송 계층 보안) 프로토콜입니다.</li></ul> |
|<br>휴지 상태의 암호화| <ul><li>[투명한 데이터 암호화](http://go.microsoft.com/fwlink/?LinkId=526242) - 비활성 데이터가 디지털 형식으로 물리적으로 저장되는 경우</li></ul>|
|**액세스 제어**||  
|<br> 데이터베이스 액세스 | <ul><li>[인증](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access)(Azure Active Directory 인증) - AD 인증은 Azure Active Directory에서 관리되는 ID를 사용합니다.</li><li>[권한 부여](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) 사용자 hello 필요한 최소한의 권한만 부여 합니다.</li></ul> |
|<br>응용 프로그램 액세스| <ul><li>[행 수준 보안](https://msdn.microsoft.com/library/dn765131) (사용 하 여 보안 정책, 사용자의 id, 역할, 또는 실행 컨텍스트를 기반으로 행 수준 액세스를 제한 하는 동시 hello에).</li><li>[동적 데이터 마스킹](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-dynamic-data-masking-get-started) (사용 하 여 사용 권한 및 정책에 중요 한 데이터 노출을 제한 toonon 권한이 사용자에 게 마스킹하 여)</li></ul>|
|**사전 모니터링**||  
| <br>추적 및 검색| <ul><li>[감사](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing) 데이터베이스 이벤트를 추적 하 고 tooan 감사 로그를 기록 활동 로그인 / 사용자 [Azure 저장소 계정](https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account)합니다.</li><li>[Azure Monitor 활동 로그](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)를 사용하여 Azure 데이터베이스 상태를 추적합니다.</li><li>[위협 검색](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-threat-detection) 잠재적 보안 위협을 toohello 데이터베이스 비정상 데이터베이스 작업을 검색 합니다. </li></ul> |
|<br>Azure 보안 센터| <ul><li>[데이터 모니터링](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-auditing-on-sql-databases) - SQL 및 기타 Azure 서비스에 대한 중앙 집중식 보안 모니터링 솔루션으로 Azure Security Center를 사용합니다.</li></ul>|     

## <a name="conclusion"></a>결론
Azure 데이터베이스는 다양한 조직 및 규정 준수 요구 사항을 충족하는 모든 보안 기능을 갖춘 강력한 데이터베이스 플랫폼입니다. Hello 물리적 tooyour 데이터에 액세스를 제어 하 고 hello 파일, 열 또는 행 수준 투명 한 데이터 암호화, 셀 수준 암호화 또는 행 수준 보안에서 보안 데이터에 대 한 다양 한 옵션을 사용 하 여 데이터를 쉽게 보호할 수 있습니다. 항상 암호화 해줍니다 암호화 된 데이터에 대 한 작업을 hello 프로세스 응용 프로그램 업데이트를 단순화 합니다. 차례로 SQL 데이터베이스 작업의 액세스 tooauditing 로그 tooknow 데이터 액세스 방법 및 시기를 허용 해야 하는 hello 정보를 제공 합니다.

## <a name="next-steps"></a>다음 단계
악의적인 사용자 또는 몇 가지 간단한 단계만 무단된 액세스 로부터 사용자 데이터베이스의 hello 보호를 향상 시킬 수 있습니다. 이 자습서에서는 다음에 대해 알아봅니다.

- 서버 및 데이터베이스에 대한 [방화벽 규칙](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) 설정
- [암호화](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption)를 사용하여 데이터 보호
- [SQL Database 감사](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing) 사용

