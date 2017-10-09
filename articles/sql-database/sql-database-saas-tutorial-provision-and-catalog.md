---
title: "Azure SQL 데이터베이스를 사용 하는 다중 테 넌 트 앱에서 aaaProvision에 새 테 넌 트. | Microsoft Docs"
description: "어떻게 tooprovision 및 카탈로그 새 테 넌 트에서 hello에 Wingtip SaaS 응용 프로그램에 알아봅니다"
keywords: "SQL Database 자습서"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: sstein
ms.openlocfilehash: eb26f523305650c2124e36707d187dfcdad06fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-new-tenants-and-register-them-in-hello-catalog"></a>새 테 넌 트를 프로 비전 하 고 hello 카탈로그에 등록 합니다

이 자습서에서는 hello 프로 비전 및 카탈로그 SaaS 패턴 및 hello Wingtip SaaS 응용 프로그램에서에서 구현 되는 방식에 대 한 배웁니다. 새 테 넌 트 데이터베이스 초기화 만들고 한 hello 응용 프로그램의 테 넌 트 카탈로그에 등록 합니다. hello 카탈로그는 hello SaaS 응용 프로그램의 여러 테 넌 트 및 해당 데이터 간에 hello 매핑을 유지 관리 하는 데이터베이스입니다. hello 카탈로그에서 중요 한 역할 응용 프로그램 요청 toohello 올바른 데이터베이스를 전달 합니다.  

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]

> * 구현되는 방법을 단계별로 포함하는 단일 새 테넌트 프로비전
> * 추가 테넌트의 배치 프로비전


toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.

* hello Wingtip SaaS 앱을 배포 합니다. 5 분 이내에 toodeploy 참조 [배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색](sql-database-saas-tutorial.md)
* Azure PowerShell이 설치되었습니다. 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.

## <a name="introduction-toohello-saas-catalog-pattern"></a>소개 toohello SaaS 카탈로그 패턴

데이터베이스 백업 다중 테 넌 트 SaaS 응용 프로그램에서는 각 테 넌 트에 대 한 정보가 저장 된 중요 한 tooknow 되었기 합니다. Hello SaaS 카탈로그 패턴에서 카탈로그 데이터베이스는 사용 되는 toohold hello 매핑 각 테 넌 트 사이 및 데이터가 저장 됩니다. hello Wingtip SaaS 앱 단일-테 넌 트를 사용 하 여 데이터베이스 아키텍처 당 있지만 다중 테 넌 트 또는 단일 테 넌 트 데이터베이스에서 사용 되는지 여부를 카탈로그에서 데이터베이스에 테 넌 트 매핑을 저장할 경우의 기본적인 패턴 hello 적용 됩니다.

각 테 넌 트는 hello 카탈로그에이 식별 하는 키를 지정 하 고 있는 매핑된 toohello 위치 hello 적절 한 데이터베이스의 키를 누릅니다. Hello Wingtip SaaS 응용 프로그램에서 hello 키 해시 hello 테 넌 트의 이름에서 형성 됩니다. 이 통해 테 넌 트 이름 부분은 hello 응용 프로그램 URL toobe hello tooconstruct hello 키를 사용 합니다. 다른 테넌트 키 스키마를 사용할 수 있습니다.  

hello 카탈로그 hello 데이터베이스 toobe hello 응용 프로그램에 미치는 영향을 최소화 하면서 변경 된의 hello 이름이 나 위치에 있습니다.  다중 테넌트 데이터베이스 모델에서 데이터베이스 간에 테넌트 ‘이동’을 적용합니다.  테 넌 트가 있는지 여부를 hello 카탈로그에 사용 되는 tooindicate 될 수도 있습니다 또는 데이터베이스 유지 관리 또는 기타 작업에 대 한 오프 라인 상태입니다. Hello에 대해서는이 [단일 테 넌 트 자습서 복원](sql-database-saas-tutorial-restore-single-tenant.md)합니다.

또한 SaaS 응용 프로그램에 대 한 관리 데이터베이스는 사실상 hello 카탈로그 추가 테 넌 트 또는 데이터베이스 메타 데이터를 저장할 수 있습니다, 그리고 hello와 같은 데이터베이스, 스키마 버전, 서비스 계획 또는 Sla의 계층을 제공 tootenants, 및 기타 정보를 응용 프로그램 관리, 고객 지원 또는 devops 프로세스 수 있습니다.  

Hello SaaS 응용 프로그램, 외 hello 카탈로그 데이터베이스 도구를 사용 하도록 설정할 수 있습니다.  Hello Wingtip SaaS 샘플 hello 카탈로그 tooenable 사용 되는 테 넌 트 간 쿼리를 hello에 대해서는 [임시 분석 자습서](sql-database-saas-tutorial-adhoc-analytics.md)합니다. 데이터베이스 간 작업 관리 hello에 대해서는 [스키마 관리](sql-database-saas-tutorial-schema-management.md) 및 [분석 테 넌 트](sql-database-saas-tutorial-tenant-analytics.md) 자습서입니다. 

Hello의 hello 분할 관리 기능을 사용 하 여 hello 카탈로그는 구현 하는 hello Wingtip SaaS 응용 프로그램에서 [탄력적 데이터베이스 클라이언트 라이브러리 (EDCL)](sql-database-elastic-database-client-library.md)합니다. hello EDCL 사용 응용 프로그램 toocreate, 관리 하 고 데이터베이스 기반 분할 맵을 사용 합니다. 분할 맵은 분할 된 데이터베이스 (데이터베이스)와 키 (테 넌 트)와 데이터베이스 간의 hello 매핑 목록을 포함합니다.  EDCL 함수 테 넌 트 toocreate hello 항목 hello shard map의 프로 비전 하는 동안 응용 프로그램 또는 PowerShell 스크립트에서 사용할 수 있습니다 및 응용 프로그램 tooefficiently에서 toohello 올바른 데이터베이스를 연결 합니다. EDCL 연결 정보 toominimize hello 트래픽 toohello 카탈로그 데이터베이스와 hello 응용 프로그램의 속도 캐시합니다.  

> [!IMPORTANT]
> hello 매핑 데이터는 hello 카탈로그 데이터베이스에 액세스할 수 있지만 *편집 하지 않는*! 매핑 데이터는 Elastic Database 클라이언트 라이브러리 API를 사용해서만 편집하세요. Hello를 손상 시키는 위험 카탈로그를 사용 하며 지원 되지 않습니다 hello 매핑 데이터를 직접 조작 합니다.


## <a name="introduction-toohello-saas-provisioning-pattern"></a>소개 toohello SaaS 프로 비전 패턴

단일 테넌트 데이터베이스 모델을 사용하는 SaaS 응용 프로그램에서 새 테넌트를 온보딩하는 경우 새 테넌트 데이터베이스를 프로비전해야 합니다.  Hello 적절 한 위치 및 서비스 계층을 적절 한 스키마 및 참조 데이터를 사용 하 여 초기화 하 고 hello 카탈로그 hello 적절 한 테 넌 트 키 아래에서 등록 한 다음 만들어야 합니다.  

두 가지 방법을 사용 하는 toodatabase 프로비저닝, SQL 스크립트 실행, bacpac는 배포 또는 '골든' 템플릿 데이터베이스 복사를 포함할 수 일 수 있습니다.  

새 데이터베이스는 최신 스키마 hello로 프로 비전는 확인 해야 하면 전체 스키마 관리 전략에 접근 방식을 사용 하면 프로 비전 하는 hello는 되었습니다 해야 합니다.  Hello에 대해서는이 [스키마 관리 자습서](sql-database-saas-tutorial-schema-management.md)합니다.  

hello Wingtip SaaS 응용 프로그램 프로 비전 새로운 테 넌 트 골든 데이터베이스를 복사 하 여 라는 basetenantdb, hello 카탈로그 서버에 배포 합니다.  프로 비전 수 수 등록 환경의 일환으로 hello 응용 프로그램에 통합 및/또는 지원 스크립트를 사용 하 여 오프 라인입니다. 이 자습서는 PowerShell을 사용하는 프로비전을 살펴봅니다. hello 프로 비전 스크립트 hello basetenantdb toocreate 새 테 넌 트 데이터베이스를 탄력적 풀의 다음 테 넌 트 관련 정보를 사용 하 여 초기화 복사한 hello 카탈로그 분할 맵을에 등록 합니다.  Hello 샘플 응용 프로그램에서 데이터베이스에는 이름이 지정 hello 테 넌 트 이름 뒤에 있지만이 hello 패턴의 중요 한 부분 – hello 카탈로그 hello 사용 하면 모든 이름 할당 toobe toohello 데이터베이스. + 


## <a name="get-hello-wingtip-application-scripts"></a>Hello Wingtip 응용 프로그램 스크립트 가져오기

hello Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드에서에서 사용할 수 있는 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다. [Toodownload hello Wingtip SaaS 스크립트 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)합니다.


## <a name="provision-and-catalog-detailed-walkthrough"></a>자세한 연습 프로비전 및 카탈로그

toounderstand 방법 응용 프로그램에는 새 테 넌 트 프로비저닝 구현 Wingtip hello, 중단점을 추가 및 테 넌 트가 프로 비전 할 때 hello 워크플로 통해 단계:

1. 열기... \\학습 모듈\\ProvisionAndCatalog\\_데모 ProvisionAndCatalog.ps1_ 집합 hello 다음 매개 변수:
   * **$TenantName** = hello 새 장소의 hello 이름 (예를 들어 *Bushwillow 파란색*).
   * **$VenueType** = hello 장소 미리 정의 된 형식 중 하나: *파란색*, classicalmusic, 댄스, jazz, judo, motorracing multipurpose, opera, rockmusic, 축구 합니다.
   * **$DemoScenario** = **1**너무 설정,**1** 너무*단일 테 넌 트를 프로 비전*합니다.

1. 줄 48, hello 라고 표시 된 줄에 아무 곳 이나 커서를 배치 하 여 중단점을 추가: *새로 만들기-테 넌 트 '*, 누릅니다 **F9**합니다.

   ![중단점](media/sql-database-saas-tutorial-provision-and-catalog/breakpoint.png)

1. toorun hello 스크립트 키를 눌러 **F5**합니다.

1. Hello 스크립트 실행이 hello 중단점에서 중지 되 후 눌러 **F11** hello 코드로 toostep 합니다.

   ![중단점](media/sql-database-saas-tutorial-provision-and-catalog/debug.png)



Hello를 사용 하 여 hello 스크립트의 실행을 추적 **디버그** 메뉴 옵션- **F10** 및 **F11** toostep 통해 또는 함수를 호출 하는 hello에 있습니다. PowerShell 스크립트를 디버깅하는 방법에 대한 자세한 내용은 [PowerShell 스크립트 사용 및 디버깅 관련 팁](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise)을 참조하세요.


hello 다음은 hello 스크립트를 디버깅 하는 동안 단계별로 실행 하는 hello 워크플로 대해 설명 하지만 tooexplicitly 수행 단계:

1. **가져오기 hello SubscriptionManagement.psm1** hello 사용 하는 Azure 구독을 선택 하 고 tooAzure를 로그인에 대 한 함수가 포함 된 모듈입니다.
1. **가져오기 hello CatalogAndDatabaseManagement.psm1** hello 동안의 카탈로그 및 테 넌 트 수준 추상화를 제공 하는 모듈 [분할 관리](sql-database-elastic-scale-shard-map-management.md) 함수입니다. 이 중요 한 모듈 hello 카탈로그 패턴의 대부분을 캡슐화 하 고 살펴볼입니다.
1. **구성 세부 정보를 가져옵니다**. Get-(F11)와 구성으로 실행 하 고 hello 응용 프로그램 구성을 지정 하는 방법을 참조 하십시오. 리소스 이름 및 기타 응용 프로그램 특정 값 여기에서 정의 되지만 hello 스크립트에 잘 알고 있다면 때까지 이러한 값 변경 되지 않습니다.
1. **Hello 카탈로그 개체 가져오기**합니다. 한 단계씩 코드를 작성 하 고 hello 더 높은 수준의 스크립트에 사용 되는 카탈로그 개체를 반환 하는 Get 카탈로그 실행 합니다.  이 함수는 **AzureShardManagement.psm1**에서 가져온 분할 관리 기능을 사용합니다. hello 카탈로그 개체 hello 다음으로 이루어져 있습니다.
   * $catalogServerFullyQualifiedName hello 표준 어간 및 사용자 이름을 사용 하 여 생성 됩니다: _카탈로그-\<사용자\>. database.windows.net_합니다.
   * $catalogDatabaseName hello 구성에서 검색 됩니다: *tenantcatalog*합니다.
   * $shardMapManager 개체 hello 카탈로그 데이터베이스에서 초기화 됩니다.
   * hello에서 $shardMap 개체가 인스턴스화될 *tenantcatalog* hello 카탈로그 데이터베이스에서 분할 맵은 합니다.
   카탈로그 개체의 구성 반환 및 hello 더 높은 수준의 스크립트에서 사용 합니다.
1. **Hello 새 테 넌 트 키를 계산**합니다. 해시 함수 hello 테 넌 트 이름에서 사용 되는 toocreate hello 테 넌 트 키입니다.
1. **Hello 테 넌 트 키가 이미 있는 경우 확인**합니다. hello 카탈로그 tooensure hello 키를 사용할 수 확인 됩니다.
1. **새로 만들기-TenantDatabase와 hello 테 넌 트 데이터베이스 프로 비전 됩니다.** 사용 하 여 **F11** 에 toostep hello 데이터베이스는 어떻게 확인할를 사용 하 여 사용자를 프로 비전는 [Azure 리소스 관리자 템플릿](../azure-resource-manager/resource-manager-template-walkthrough.md)합니다.

hello 데이터베이스 이름은 hello 테 넌 트 이름 toomake 것을 알 수는 분할 영역 속한 toowhich 테 넌 트에서에서 생성 됩니다. (데이터베이스 이름 지정에 대 한 다른 전략 쉽게 사용할 수 있습니다.) + 리소스 관리자 템플릿은 골든 데이터베이스 (baseTenantDB) hello 카탈로그 서버에 복사 하 여 사용 되는 toocreate 테 넌 트 데이터베이스입니다. 다른 접근 방식은 수 수 toocreate 빈 데이터베이스 초기화 한 다음 해당 bacpac, 또는 tooexecute 가져와서 잘 알려진 위치에서 초기화 스크립트는 합니다.  

hello...\Learning Modules\Common\ 폴더에 hello 리소스 관리자 서식 파일은: *tenantdatabasecopytemplate.json*

Hello 테 넌 트 데이터베이스를 만든 후 하는 추가 **hello 장소 형식과 hello 장소 (테 넌 트) 이름을 사용 하 여 초기화**합니다. 여기서 다른 초기화가 수행될 수도 있습니다.

hello **hello 카탈로그에서 테 넌 트 데이터베이스를 등록** 와 *추가 TenantDatabaseToCatalog* hello 테 넌 트 키를 사용 하 여 합니다. 사용 하 여 **F11** toostep hello 세부 정보로:

* hello 카탈로그 데이터베이스 toohello 분할 맵은 (알려진된 데이터베이스 hello 목록)에 추가 됩니다.
* 해당 링크 hello 키 값 toohello 분할 매핑 hello가 만들어집니다.
* Hello 테 넌 트에 대 한 추가 메타 데이터 (hello 장소 이름)는 toohello 테 넌 트 테이블 hello 카탈로그에 추가 됩니다.  hello 테 넌 트 테이블 hello ShardManagement 스키마의 일부가 아니며 hello EDCL 설치 되어 있지 않습니다.  이 표에서 어떻게 hello 카탈로그 데이터베이스를 확장할 수 toosupport 추가 응용 프로그램 관련 데이터를 설명 합니다.   


프로 비전 완료 된 후 실행 하 여 반환 toohello 원래 *데모 ProvisionAndCatalog* hello를 열 수 있는 스크립트 **이벤트** hello 브라우저에서 새 테 넌 hello에 대 한 페이지:

   ![events](media/sql-database-saas-tutorial-provision-and-catalog/new-tenant.png)


## <a name="provision-a-batch-of-tenants"></a>테넌트의 배치 프로비전

이 연습에서는 17개의 테넌트의 배치를 프로비전합니다. 테 넌 트의이 일괄 처리와 방금 여러 데이터베이스 toowork 이므로 다른 Wingtip SaaS 자습서를 시작 하기 전에 프로 비전 하는 것이 좋습니다.

1. 열기... \\학습 모듈\\ProvisionAndCatalog\\*데모 ProvisionAndCatalog.ps1* hello에 *PowerShell ISE* hello 변경 *$ DemoScenario* too3 매개 변수:
   * **$DemoScenario** = **3**도 변경**3** 너무*테 넌 트의 일괄 처리를 프로 비전*합니다.
1. 키를 눌러 **F5** hello 스크립트를 실행 합니다.

hello 스크립트 추가 테 넌 트의 일괄 처리를 배포합니다. 사용 하 여 프로그램 [Azure 리소스 관리자 템플릿](../azure-resource-manager/resource-manager-template-walkthrough.md) hello 일괄 처리를 제어 하 고 각 데이터베이스 tooa 연결 된 템플릿의 프로 비전을 위임 합니다. 이러한 방식으로 템플릿을 사용 하 여 Azure 리소스 관리자 toobroker hello를 스크립트에 대 한 프로세스를 프로 비전 수 있습니다. 서식 파일 수, 하 고 필요한 경우 재시도 처리 하는 동시에는 데이터베이스를 프로 비전 hello 전반적인 프로세스를 최적화 합니다. 스크립트 hello은 idempotent 이므로 실패 하거나 어떤 이유로 든 중지 하는 경우 다시 실행 합니다.

### <a name="verify-hello-batch-of-tenants-successfully-deployed"></a>성공적으로 배포 하는 테 넌 트의 hello 일괄 처리를 확인 합니다.

* 열기 hello *tenants1* hello에서 서버의 tooyour 목록을 검색 하 여 서버 [Azure 포털](https://portal.azure.com), 클릭 **SQL 데이터베이스**, 17 추가 된 데이터베이스의 hello 일괄 처리는 이제 확인 hello 목록:

   ![데이터베이스 목록](media/sql-database-saas-tutorial-provision-and-catalog/database-list.png)



## <a name="other-provisioning-patterns"></a>기타 프로비전 패턴

이 자습서에 포함되지 않은 기타 프로비전 패턴은 다음을 포함합니다.

**데이터베이스를 미리 프로비전.** 추가 비용 탄력적 풀의 데이터베이스를 추가 하지 않는 hello 팩트를 악용 하는 hello 패턴을 미리 프로 비전 됩니다. 청구 hello 탄력적 풀에 대 한 데이터베이스, 하지 hello 있고, 유휴 데이터베이스 없는 리소스를 소비 합니다. 풀에 있는 데이터베이스를 미리 프로비전하고 필요한 경우 할당하면 테넌트 온보딩 시간이 크게 감소할 수 있습니다. 필요한 tookeep hello에 대 한 적합 한 버퍼 속도 프로 비전 하는 것으로 예상 대로 hello 미리 제공 하는 데이터베이스 수를 조정할 수 없습니다.

**자동 프로비전.** Hello 자동 프로 비전 패턴에서 전용된 프로 비전 서비스는 사용 되는 tooprovision 서버, 풀 및 데이터베이스 자동으로 필요한 경우 탄력적 풀에 미리 프로 비전 데이터베이스를 비롯 한 – 필요에 따라. 고 탄력적 풀의 간격 데이터베이스가, 삭제 및 제거 하는 경우 필요에 따라 서비스를 프로 비전 하는 hello 여 채울 수 있습니다. 그러한 서비스는 단순할 수도 있고 복잡할 수도 있으며(예를 들어 여러 지리적 영역에 걸쳐 프로비전을 처리) 재해 복구에 대해 그러한 전략을 사용 중인 경우 지역에서 복제를 자동으로 설정할 수 있습니다. Hello 자동 프로 비전 패턴으로는 클라이언트 응용 프로그램 또는 스크립트 서비스를 프로 비전 하는 hello에서 처리 하는 프로 비전 요청 tooa 큐 toobe 제출 것 하 고 hello 서비스 toodetermine 완료를 폴링하는. 미리 프로 비전을 사용 하는 요청 hello 백그라운드에서 실행 되는 대체 데이터베이스 프로 비전을 관리 하는 hello 서비스와 신속 하 게 처리 합니다.



## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]

> * 단일 새 테넌트 프로비전
> * 추가 테넌트의 배치 프로비전
> * 테 넌 트를 프로 비전 하 고 hello 카탈로그에 등록 하는 중 hello 세부 정보를 한 단계씩

Hello 시도 [성능 모니터링 자습서](sql-database-saas-tutorial-performance-monitoring.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* 추가 [hello Wingtip SaaS 응용 프로그램을 구축 하는 자습서](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Elastic Database 클라이언트 라이브러리](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-database-client-library)
* [Windows PowerShell ISE에서 tooDebug 스크립트 하는 방법](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise)
