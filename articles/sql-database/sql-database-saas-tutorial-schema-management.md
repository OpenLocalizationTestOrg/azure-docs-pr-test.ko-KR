---
title: "다중 테 넌 트 응용 프로그램에서 Azure SQL 데이터베이스 스키마 aaaManage | Microsoft Docs"
description: "Azure SQL Database를 사용하는 다중 테넌트 응용 프로그램에서 여러 테넌트에 대한 스키마 관리"
keywords: "SQL Database 자습서"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a>Hello Wingtip SaaS 응용 프로그램에서에서 여러 테 넌 트에 대 한 스키마를 관리 합니다.

hello [첫 번째 Wingtip SaaS 자습서](sql-database-saas-tutorial.md) hello 앱 수 테 넌 트 데이터베이스 프로 비전 하 고 hello 카탈로그에 등록 하는 방법을 보여 줍니다. 모든 응용 프로그램과 마찬가지로 시간이 지남에 따라 이동 하 고 때때로 Wingtip SaaS 앱 점점 발전 hello toohello 데이터베이스 변경 해야 합니다. 새롭거나 변경 된 스키마, 새롭거나 변경 된 참조 데이터 및 일상적인 데이터베이스 유지 관리 작업 tooensure 최적의 앱 성능을 변경 내용이 포함 될 수 있습니다. SaaS 응용 프로그램을 이러한 변경 내용은 잠재적으로 대규모 대 테 넌 트 데이터베이스에서 통합 된 방식으로 배포 toobe가 필요 합니다. 이러한 변경 내용 toobe에 대 한 이후 테 넌 트 데이터베이스, 사용자가 toobe hello를 프로 비전 프로세스에 통합 합니다.

이 자습서에서는 두 가지 시나리오-모든 테 넌 트에 대 한 참조 데이터 업데이트를 배포 하 고 hello 참조 데이터가 포함 된 테이블 재조정 hello에 대 한 인덱스 작업을 수행 합니다. hello [탄력적 작업](sql-database-elastic-jobs-overview.md) 기능이 사용 되는 tooexecute를 이러한 작업은 모든 테 넌 트 및 hello에서 *골든* 새 데이터베이스에 대 한 템플릿으로 사용 되는 테 넌 트 데이터베이스.

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]

> * 작업 계정 만들기
> * 여러 테넌트 쿼리
> * 모든 테넌트 데이터베이스의 데이터 업데이트
> * 모든 테넌트 데이터베이스의 테이블에서 인덱스 만들기


이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 만족할 toocomplete:

* hello Wingtip SaaS 앱을 배포 합니다. 5 분 이내에 toodeploy 참조 [배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색](sql-database-saas-tutorial.md)
* Azure PowerShell이 설치되었습니다. 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.
* SQL Server Management Studio (SSMS) hello 최신 버전이 설치 됩니다. [SSMS 다운로드 및 설치](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

*이 자습서에서는 제한 된 미리 보기 (탄력적 데이터베이스 작업)에 있는 hello SQL 데이터베이스 서비스의 기능을 사용 합니다. 이 자습서 toodo을 원할 경우 구독 id를 제공 tooSaaSFeedback@microsoft.com 주체 = 탄력적 작업 미리 보기. 구독에서 사용할 수 있는 확인 메시지가 나타나면 [다운로드 하 여 hello 최신 시험판 작업 cmdlet 설치](https://github.com/jaredmoo/azure-powershell/releases)합니다. 이 미리 보기는 제한적으로만 제공되므로 관련 질문이 있거나 지원이 필요한 경우 SaaSFeedback@microsoft.com에 문의해야 합니다.*


## <a name="introduction-toosaas-schema-management-patterns"></a>소개 tooSaaS 스키마 관리 패턴

hello 데이터베이스 마다 단일 테 넌 트 SaaS 패턴 여러 면에서 결과 hello 데이터 격리 이점을 있지만 hello에 동시 hello 유지 및 많은 데이터베이스 관리의 복잡성이 추가 합니다. [탄력적 작업](sql-database-elastic-jobs-overview.md) hello SQL 데이터 계층의 관리를 용이 하 게 합니다. Toosecurely를 활성화 하 고 안전 하 게 데이터베이스 그룹에 대 한 작업 (T-SQL 스크립트) 사용자 상호 작용 및 입력을에 관계 없이 실행 하는 작업입니다. 이 메서드는 응용 프로그램에서 모든 테 넌 트 간에 사용 되는 toodeploy 스키마 및 일반 참조 데이터 변경 내용 수 있습니다. 탄력적 작업에 사용 되는 toomaintain 될 수도 있습니다는 *골든* hello 데이터베이스의 복사본이 toocreate 새 테 넌 트를 hello 최신 스키마 및 참조 데이터를 항상에 확인을 사용 합니다.

![화면](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a>탄력적 작업의 제한된 미리 보기

현재 Azure SQL Database(추가 서비스 또는 구성 요소 불필요)의 통합 기능인 새로운 탄력적 작업 버전이 있습니다. 이 새로운 탄력적 작업 버전은 현재 제한된 미리 보기 상태입니다. 이 제한 된 미리 보기는 현재 PowerShell toocreate 작업 계정 및 T-SQL toocreate 지원 하 고 작업을 관리 합니다.

> [!NOTE]
> *이 자습서에서는 제한 된 미리 보기 (탄력적 데이터베이스 작업)에 있는 hello SQL 데이터베이스 서비스의 기능을 사용 합니다. 이 자습서 toodo을 원할 경우 구독 id를 제공 tooSaaSFeedback@microsoft.com 주체 = 탄력적 작업 미리 보기. 구독에서 사용할 수 있는 확인 메시지가 나타나면 [다운로드 하 여 hello 최신 시험판 작업 cmdlet 설치](https://github.com/jaredmoo/azure-powershell/releases)합니다. 이 미리 보기는 제한적으로만 제공되므로 관련 질문이 있거나 지원이 필요한 경우 SaaSFeedback@microsoft.com에 문의해야 합니다.*

## <a name="get-hello-wingtip-application-scripts"></a>Hello Wingtip 응용 프로그램 스크립트 가져오기

hello Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드에서에서 사용할 수 있는 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다. [Toodownload hello Wingtip SaaS 스크립트 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)합니다.

## <a name="create-a-job-account-database-and-new-job-account"></a>작업 계정 데이터베이스 및 새 작업 계정 만들기

이 자습서에서는 계정을 사용 하 여 PowerShell toocreate hello 작업 계정 데이터베이스와 작업이 필요 합니다. MSDB 등 SQL 에이전트 탄력적 작업 사용 하 여 Azure SQL 데이터베이스 toostore 작업 정의 작업 상태 및 기록 합니다. Hello 작업 계정이 만들어지면 만들 수 있으며 작업을 즉시 모니터링.

1. 열기... \\학습 모듈\\스키마 관리\\*데모 SchemaManagement.ps1* hello에 **PowerShell ISE**합니다.
1. 키를 눌러 **F5** toorun hello 스크립트입니다.

hello *데모 SchemaManagement.ps1* 스크립트 호출 hello *배포 SchemaManagement.ps1* toocreate 스크립트는 *S2* 라는 데이터베이스 **jobaccount** hello 카탈로그 서버에 있습니다. 그런 다음 hello jobaccount 데이터베이스 매개 변수 toohello 작업 계정 만들기 호출으로 전달 되는 hello 작업 계정을 만듭니다.

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a>작업 toodeploy 새 참조 데이터 tooall 테 넌 트 만들기

각 테 넌 트 데이터베이스 한 장소에서 호스트 되는 이벤트의 hello 종류를 정의 하는 장소 형식의 집합을 가집니다. 이 연습에서는 업데이트 tooall hello 테 넌 트 데이터베이스 tooadd 두 추가 장소 형식을 배포 있습니다: *오토바이 레이싱* 및 *수영 클럽*합니다. 이러한 장소 형식은 해당 toohello 배경 이미지 hello 테 넌 트에 대 한 이벤트 응용 프로그램에서 참조 합니다.

Hello 장소 유형 드롭다운 메뉴를 클릭 하 고 10 개만 장소 유형 옵션을 사용할 수 있고 특히 해당 ' 오토바이 레이싱 ' 및 ' 수영 클럽 ' hello 목록에 포함 되지 않습니다 하는지 유효성을 검사 합니다.

이제 작업 tooupdate hello를 만들어 보겠습니다 *VenueTypes* 모든 hello 테 넌 트 데이터베이스에서 테이블을 hello 새 장소 유형을 추가 합니다.

toocreate 새 작업을 사용 하 여 작업 집합이 시스템 저장 프로시저 hello 작업 계정을 만들 때 hello jobaccount 데이터베이스에서 만들어집니다.

1. SSMS를 열고 고 toohello 카탈로그 서버에 연결: 카탈로그-\<사용자\>. database.windows.net 서버
1. 또한 toohello 테 넌 트 서버를 연결할: tenants1-\<사용자\>. database.windows.net
1. Toohello 찾아보기 *contosoconcerthall* hello에 대 한 데이터베이스 *tenants1* 서버와 쿼리 hello *VenueTypes* 테이블 tooconfirm는 *오토바이 레이싱*  및 *수영 클럽* **없는** hello 결과 목록에 있습니다.
1. 파일 열기 hello 중... \\학습 모듈\\스키마 관리\\DeployReferenceData.sql
1. Hello 문을 수정: 설정 @wtpUser = &lt;사용자&gt; hello Wingtip 앱을 배포할 때 사용 하는 hello 사용자 값 대체
1. 연결 된 toohello jobaccount 데이터베이스 및 키를 눌러 준수할 **F5** hello 스크립트를 실행 하려면

* **sp\_추가\_대상\_그룹** tooadd 대상 멤버 필요 이제 hello 대상 그룹 이름, DemoServerGroup를 만듭니다.
* **sp\_추가\_대상\_그룹\_멤버** 추가 *서버* 대상 해당 서버 (이 hello tenants1내의모든데이터베이스하다고판단되는멤버유형&lt; 사용자&gt; hello 테 넌 트 데이터베이스를 포함 하는 서버) 작업의 시간에 실행에에서 포함 되어야 hello 작업 hello 두 번째로 추가 하는 것을 *데이터베이스* 대상 멤버 유형, 특히 '골든' 데이터베이스 (hello basetenantdb) 카탈로그에 있는&lt;사용자&gt; 서버 및 마지막으로 다른 *데이터베이스* 대상 그룹 멤버 형식 tooinclude hello adhocanalytics 데이터베이스는 이후 자습서에서 사용 합니다.
* **sp\_add\_job**은 "참조 데이터 배포"라는 작업을 만듭니다.
* **sp\_추가\_jobstep** T-SQL 명령 텍스트 tooupdate hello 참조 테이블 VenueTypes를 포함 하는 hello 작업 단계를 만듭니다
* hello 스크립트에 hello 나머지 보기 hello 개체 및 모니터링 작업을 실행의 hello 존재 여부를 표시합니다. 이러한 쿼리 tooreview hello 상태 값을 사용 하 여 hello에 **수명 주기** 열 toodetermine hello 작업이 모든 테 넌 트 데이터베이스 및 hello 참조 테이블을 포함 하는 hello 두 추가 데이터베이스에서 성공적으로 완료 된 경우.

1. SSMS에서 찾아보기 toohello *contosoconcerthall* hello에 대 한 데이터베이스 *tenants1* 서버와 쿼리 hello *VenueTypes* 테이블 tooconfirm는 *오토바이 레이싱* 및 *수영 클럽* **는** hello 결과 목록에서 이제 합니다.


## <a name="create-a-job-toomanage-hello-reference-table-index"></a>작업 toomanage hello 참조 테이블 인덱스 만들기

비슷한 toohello 이전 연습이이 연습 작업 toorebuild hello 인덱스 hello 참조 테이블에 대 한 기본 키에, 테이블에 대형 데이터 로드 후 관리자가 일반적인 데이터베이스 관리 작업을 수행할 수 있습니다.

동일한 작업 'system' hello를 사용 하 여 작업을 만드는 저장 프로시저입니다.

1. SSMS를 열고 연결 toohello 카탈로그-&lt;사용자&gt;. database.windows.net 서버
1. 파일 열기 hello 중... \\학습 모듈\\스키마 관리\\OnlineReindex.sql
1. 마우스 오른쪽 단추로 클릭 하 고, 연결을 선택 하 고, 연결 toohello 카탈로그-&lt;사용자&gt;. 아직 연결 되지 경우 database.windows.net 서버
1. 연결 된 toohello jobaccount 데이터베이스를 있으며 toorun hello 스크립트 F5 키를 눌러 확인

* sp\_add\_job은 "Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885"라는 새 작업을 만듭니다.
* sp\_추가\_jobstep T-SQL 명령 텍스트 tooupdate hello 인덱스를 포함 하는 hello 작업 단계를 만듭니다.




## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]

> * 여러 테 넌 트 플랫폼에서 작업 계정 tooquery 만들기
> * 모든 테넌트 데이터베이스의 데이터 업데이트
> * 모든 테넌트 데이터베이스의 테이블에서 인덱스 만들기

[임시 분석 자습서](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a>추가 리소스

* [Hello Wingtip SaaS 응용 프로그램 배포를 구축 하는 추가 자습서](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [규모가 확장된 클라우드 데이터베이스 관리](sql-database-elastic-jobs-overview.md)
* [규모가 확장된 클라우드 데이터베이스 만들기 및 관리](sql-database-elastic-jobs-create-and-manage.md)
