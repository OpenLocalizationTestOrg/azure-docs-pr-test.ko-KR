---
title: "aaaDeploy 및 Azure SQL 데이터베이스를 사용 하는 hello 다중 테 넌 트 Wingtip SaaS 응용 프로그램 탐색 | Microsoft Docs"
description: "배포 하 고 hello Wingtip SaaS 다중 테 넌 트 응용 프로그램을 Azure SQL 데이터베이스를 사용 하 여 SaaS 패턴을 보여 주는 탐색 합니다."
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
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: 7c528ee19472d3b8c7a285b2f86013945e8f4bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-explore-a-multi-tenant-application-that-uses-azure-sql-database---wingtip-saas"></a>Azure SQL Database를 사용하는 다중 테넌트 응용 프로그램 배포 및 탐색 - Wingtip SaaS

이 자습서에서는 배포 하 고 hello Wingtip SaaS 응용 프로그램을 탐색 합니다. hello 응용 프로그램 데이터베이스-당-테 넌 트, SaaS 응용 프로그램 패턴 tooservice 여러 테 넌 트를 사용합니다. hello 응용 프로그램에 사용할 수 있도록 SaaS 시나리오를 단순화 하는 Azure SQL 데이터베이스의 디자인 된 tooshowcase 기능입니다.

클릭 한 후 5 분 hello *tooAzure 배포* 아래 단추 있고 다중 테 넌 트 SaaS 응용 프로그램을 SQL 데이터베이스를 사용 하 여 최대 hello 클라우드에서 실행 합니다. hello 응용 프로그램은 각각 자체 데이터베이스를 SQL 탄력적 풀으로 배포 된 모든 세 샘플 테 넌 트에서 배포 됩니다. hello 앱이 배포 된 tooyour Azure 구독에 대 한 모든 권한 tooexplore 및 hello 개별 응용 프로그램 구성 요소와 작업을 제공 합니다. hello 응용 프로그램 소스 코드 및 관리 스크립트 hello WingtipSaaS GitHub 리포지토리 제공 됩니다.


이 자습서에서는 다음에 대해 알아봅니다.

> [!div class="checklist"]

> * 어떻게 toodeploy hello Wingtip SaaS 응용 프로그램
> * 응용 프로그램 소스 코드 및 관리 스크립트 tooget hello 하는 위치
> * Hello 서버, 풀 및 hello 응용 프로그램을 구성 하는 데이터베이스에 대 한
> * 어떻게 테 넌 트 매핑된 hello 사용 하 여 tootheir 데이터 *카탈로그*
> * 어떻게 tooprovision 새 테 넌 트
> * Toomonitor는 hello 응용 프로그램에서 작업 테 넌 트 방식

tooexplore 다양 한 SaaS 디자인 및 관리 패턴을는 [일련의 관련된 자습서](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) ´ ï ´이 초기 배포를 구축 하 합니다. Hello 자습서를 통과 하는 동안 hello 제공 된 스크립트에 자세히 알아보기 hello 다양 한 SaaS 패턴을 구현 하는 방법 검토 하 합니다. 각 자습서 toogain 어떻게 tooimplement hello 많은 SQL 데이터베이스 기능에 대 한 깊은 이해가의 hello 스크립트를 단계별로 SaaS 응용 프로그램 개발을 간소화 합니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.

* Azure PowerShell이 설치되었습니다. 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.

## <a name="deploy-hello-wingtip-saas-application"></a>Hello Wingtip SaaS 응용 프로그램 배포

Hello Wingtip SaaS 앱을 배포 합니다.

1. 클릭 하 여 hello **tooAzure 배포** 단추 hello Azure 포털 toohello Wingtip SaaS 배포 템플릿을 엽니다. hello 템플릿에 필요 두 매개 변수 값입니다. 새 리소스 그룹에 대 한 이름 및 hello Wingtip SaaS 앱의 다른 배포에서이 배포를 구별 하는 사용자 이름입니다. hello 다음 단계는 이러한 값을 설정 하는 것에 대 한 세부 정보를 제공 합니다.

   Tooenter 구성으로 파일 나중에 필요 하므로 있는지 toonote hello 정확한 값을 사용 하는 확인 합니다.

   <a href="http://aka.ms/deploywtpapp" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

1. Hello 배포에 대 한 필수 매개 변수 값을 입력 합니다.

    > [!IMPORTANT]
    > 일부 인증 및 서버 방화벽은 데모 목적으로 의도적으로 보호되지 않습니다. **새 리소스 그룹을 만들고**, 기존 리소스 그룹, 서버 또는 풀을 사용하지 마세요. 이 응용 프로그램이나 여기에서 만든 리소스를 프로덕션에 사용하지 마세요. 이 리소스를 삭제할 응용 프로그램 toostop hello 사용을 마친 경우 그룹 관련 청구 합니다.

    * **리소스 그룹** -선택 **새로 만들기** 설명과 **이름** hello 리소스 그룹에 대 한 합니다. 선택 된 **위치** hello 드롭 다운 목록에서 합니다.
    * **사용자** - 일부 리소스에는 전역적으로 고유한 이름이 필요합니다. tooensure 고유성 hello 응용 프로그램을 배포할 때마다 toodifferentiate, 리소스를 만들 hello Wingtip 응용 프로그램의 다른 배포에 의해 생성 된 리소스에서 값을 제공 합니다. 것이 좋습니다 toouse 짧은 **사용자** 이름, 이니셜 및 많은 같은 (예를 들어 *bg1*), 다음 hello 리소스 그룹 이름에서 사용 하는 (예를 들어 *wingtip-bg1*). **User** 매개 변수에는 문자, 숫자 및 하이픈만 포함할 수 있습니다(공백 없음). hello 첫 자와 끝 자는 문자 또는 숫자 여야 합니다는 (모든 소문자 권장).


1. **Hello 응용 프로그램 배포**합니다.

    * Tooagree toohello 사용 약관을 클릭 합니다.
    * **구매**를 클릭합니다.

1. 클릭 하 여 배포 상태를 모니터링 **알림** (hello 검색 상자 오른쪽의 hello 종 모양 아이콘). Hello Wingtip SaaS 앱 배포는 5 분 정도 걸립니다.

   ![배포 성공](media/sql-database-saas-tutorial/succeeded.png)

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>다운로드 하 고 hello Wingtip SaaS 스크립트를 차단 해제

Hello 응용 프로그램을 배포 하는 동안 hello 소스 코드 및 관리 스크립트를 다운로드 합니다.

> [!IMPORTANT]
> zip 파일이 외부 원본에서 다운로드되고 추출될 때 Windows에서 실행 가능한 콘텐츠(스크립트, dll)를 차단할 수 있습니다. Zip 파일에서 hello 스크립트를 추출, 추출 하기 전에 아래 toounblock hello.zip 파일 hello 단계를 수행 합니다. 이렇게 하면 hello 스크립트 toorun 허용 됩니다.

1. 너무 찾아보기[hello Wingtip SaaS github 리포지토리](https://github.com/Microsoft/WingtipSaaS)합니다.
1. **복제 또는 다운로드**를 클릭합니다.
1. 클릭 **zip 파일 다운로드** hello 파일을 저장 합니다.
1. 마우스 오른쪽 단추로 클릭 hello **WingtipSaaS master.zip** 파일을 찾아 선택 **속성**합니다.
1. Hello에 **일반** 탭에서 **차단 해제**를 클릭 하 고 **적용**합니다.
1. **확인**을 클릭합니다.
1. Hello 파일을 추출 합니다.

Hello에 있는 스크립트 *... \\WingtipSaaS 마스터\\학습 모듈* 폴더입니다.

## <a name="update-hello-configuration-file-for-this-deployment"></a>이 배포에 대 한 hello 구성 파일 업데이트

모든 스크립트를 실행 하기 전에 hello 설정 *리소스 그룹* 및 *사용자* 값 **UserConfig.psm1**합니다. 배포 하는 동안 설정 된 toohello 값 이러한 변수를 설정 합니다.

1. 열기... \\학습 모듈\\*UserConfig.psm1* hello에 *PowerShell ISE*
1. 업데이트 *ResourceGroupName* 및 *이름* hello (10과 11만 줄)에서 배포에 대 한 특정 값으로.
1. Hello ब ा ळ!

여기에서이 설정 하는 모든 스크립트에서 tooupdate 이러한 배포 관련 값이 있으면에서 단순히 유지 합니다.

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행

hello 앱과 함께 홀을 재즈 클럽 스포츠 클럽 이벤트를 호스트 하는 같은 운송 수단을 보여줍니다. 운송 수단을 쉽게 toolist 이벤트에 대 한 hello Wingtip 플랫폼의 고객 (또는 테 넌 트)로 등록 하 고 티켓 판매 합니다. 각 장소 개인 설정 된 웹 응용 프로그램 toomanage 및 해당 이벤트를 나열 가져오고 독립적 이며 다른 테 넌 트 로부터 격리 된 티켓을 판매 합니다. Hello에서는 각 테 넌 트 SQL 탄력적 풀으로 배포 된 SQL 데이터베이스를 가져옵니다.

중앙 **이벤트 허브** Url 특정 tooyour 배포 테 넌 트의 목록을 제공 합니다.

1. 열기 hello _이벤트 허브_ 웹 브라우저에서: http://events.wtp.&lt; 사용자&gt;. trafficmanager.net (배포의 사용자 이름으로 대체):

    ![Events Hub](media/sql-database-saas-tutorial/events-hub.png)

1. *이벤트 허브*에서 **Fabrikam Jazz Club**을 클릭합니다.

   ![이벤트](./media/sql-database-saas-tutorial/fabrikam.png)


hello 응용 프로그램 사용 하 여 들어오는 요청의 toocontrol hello 배포 [ *Azure 트래픽 관리자*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)합니다. hello 이벤트 페이지, 즉 특정 테 넌 트, 테 넌 트 이름 hello Url에 포함 되어 있는지 필요 합니다. 모든 hello 테 넌 트 Url에는 특정 *사용자* 값은 다음과 같은이 형식 및: http://events.wtp.&lt; 사용자&gt;.trafficmanager.net/*fabrikamjazzclub*합니다. hello 이벤트 앱 hello URL에서 테 넌 트 이름을 hello를 구문 분석 하 고 사용 하 여 카탈로그 키 tooaccess toocreate 사용 [ *분할 맵 관리*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-shard-map-management)합니다. hello 카탈로그 지도 hello 키 toohello 테 넌 트의 데이터베이스 위치입니다. hello **이벤트 허브** 확장된 메타 데이터를 사용 하 여 각 데이터베이스 tooprovide hello 목록 url에 연결 된 hello 카탈로그 tooretrieve hello 테 넌 트의 이름에서입니다.

프로덕션 환경에서 일반적으로 만들면 됩니다 CNAME DNS 레코드를 [ *회사 인터넷 도메인 가리키기* ](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-point-internet-domain) hello 트래픽 관리자 프로필.

## <a name="start-generating-load-on-hello-tenant-databases"></a>Hello 테 넌 트 데이터베이스의 부하를 생성 합니다.

Hello 앱을 배포 했으므로 이제 넣습니다 toowork를! hello *데모 LoadGenerator* PowerShell 스크립트는 모든 테 넌 트 데이터베이스에 대해 실행 되는 작업 부하를 시작 합니다. 많은 SaaS 응용 프로그램에 hello 실제 부하는 일반적으로 드물게 발생 하 고 예측할 수 없는 합니다. 이러한 종류의 로드, hello 생성기 toosimulate 임의 간격으로 발생 하 여 각 테 넌 트에 임의 필요 모든 테 넌 트 간의 분산 부하를 생성 합니다. 부하 패턴 tooemerge hello에 대 일 분 정도 걸리며이 때문에 3 개에 대해 실행 하는 최상의 toolet hello 생성기는 또는 hello를 모니터링 하기 전에 4 분 로드 합니다.

1. Hello에 *PowerShell ISE*개방형 hello... \\학습 모듈\\유틸리티\\*데모 LoadGenerator.ps1* 스크립트입니다.
1. 키를 눌러 **F5** 를 hello 스크립트를 실행 하 고 hello 부하 생성기 (leave hello 매개 변수 기본값 지금은)를 시작 합니다.

> [!IMPORTANT]
> toorun 다른 스크립트, 새 PowerShell ISE 창을 엽니다. hello 부하 생성기는 일련의 작업으로 로컬 PowerShell 세션에서 실행 중입니다. hello *데모 LoadGenerator.ps1* 스크립트 명령은 foreground 작업 + 일련의 배경 부하 생성 작업으로 실행 되는 hello 실제 부하 생성기 스크립트를 시작 합니다. 부하 생성기 작업 hello 카탈로그에 등록 된 각 데이터베이스에 대해 호출 됩니다. hello 작업이 실행 되 고 로컬 PowerShell 세션에서 hello PowerShell 세션이 닫히면서 모든 작업을 중지 합니다. 컴퓨터를 일시 중단하면 부하 생성이 일시 중지되고 컴퓨터의 절전 모드를 해제하면 다시 시작됩니다.

각 테 넌 트에 대 한 부하 생성 작업을 호출 하는 hello 부하 생성기, 되 면 hello foreground 작업 추가 백그라운드 작업 이후에 프로 비전 되는 새 테 넌 트에 대 한 시작 되는 작업 호출 상태로 유지 됩니다. 사용할 수 있습니다 *Ctrl-c* 또는 키를 눌러 hello *중지* 단추 toostop hello foreground 작업 하지만 기존 백그라운드 작업은 각 데이터베이스에서 부하가 생성 계속 됩니다. 필요한 toomonitor hello 백그라운드 작업을 제어 하는 경우 사용 하 여 *Get-job*, *Receive-job* 및 *Stop-job*합니다. Hello foreground 작업 하면 실행 되는 동안 없습니다 사용 하 여 hello 같은 PowerShell 세션 tooexecute 다른 스크립트입니다. toorun 다른 스크립트, 새 PowerShell ISE 창을 엽니다.

Toorestart hello 부하 생성기 세션을 실행 하려면 예를 들어 서로 다른 매개 변수를 사용 중지할 수 있습니다 hello foreground 작업을 다시 실행 하는 hello *데모 LoadGenerator.ps1* 스크립트입니다. 다시 실행 *데모 LoadGenerator.ps1* 먼저 현재 실행 중인 작업, 및 새로운 hello 현재 매개 변수를 사용 하 여 작업 집합이 교육은 다시 시작 hello 생성기를 모두 중지 합니다.

지금은 hello 작업 호출 상태에서 실행 하는 hello 부하 생성기를 둡니다.


## <a name="provision-a-new-tenant"></a>새 테넌트 프로비전

hello 초기 배포 3 개 샘플 테 넌 트를 만들지만 다른 테 넌 트 toosee 만들기 hello 배포 응용 프로그램에 미치는 영향에 있습니다. hello Wingtip SaaS 프로 비전-테 넌 트 워크플로 hello에 자세히 설명 되어 [프로 비전 및 카탈로그 자습서](sql-database-saas-tutorial-provision-and-catalog.md)합니다. 이 단계에서는 신속하게 새 테넌트를 만들 수 있습니다.

1. 열기... \\학습 Modules\Provision 및 카탈로그\\*데모 ProvisionAndCatalog.ps1* hello에 *PowerShell ISE*합니다.
1. 키를 눌러 **F5** hello 스크립트 (지금은 leave hello 기본 값)를 실행 합니다.

   > [!NOTE]
   > 많은 SaaS Wingtip 스크립트 사용 하 여 *$PSScriptRoot* tooallow 다른 스크립트의 toocall 함수 폴더를 탐색 합니다. 이 변수는 키를 눌러 hello 스크립트가 실행 될 때에 평가 되기 **F5**합니다.  선택 내용을 강조 표시하고 실행(**F8**)하면 오류가 발생할 수 있으므로 스크립트를 실행할 때는 **F5** 키를 누르세요.

새 테 넌 트 데이터베이스 hello SQL 탄력적 풀에서 만든, 초기화 및 hello 카달로그에 등록 합니다. 성공적으로 프로 비전 한 후 hello 새 테 넌 트의 티켓 판매 *이벤트* 사이트 브라우저에 나타납니다.

![새 테넌트](./media/sql-database-saas-tutorial/red-maple-racing.png)

Hello 새로 고침 *이벤트 허브* hello 새 테 넌 트 hello 목록에 나타납니다.


## <a name="explore-hello-servers-pools-and-tenant-databases"></a>Hello 서버 풀, 탐색 하 고 데이터베이스를 테 넌 트

테 넌 트의 hello 컬렉션에 대해 부하를 실행 중인 시작 했으므로 배포 된 hello 리소스 중 일부에서 살펴보겠습니다.

1. 에 [Azure 포털](http://portal.azure.com)SQL servers 목록을 tooyour 찾아 열은 **카탈로그-&lt;사용자&gt;**  서버입니다. hello 카탈로그 서버는 두 개의 데이터베이스를 포함합니다. hello **tenantcatalog**, 및 hello **basetenantdb** (빈 *골든* 템플릿 데이터베이스는 복사 toocreate 새 테 넌 트 또는).

   ![데이터베이스](./media/sql-database-saas-tutorial/databases.png)

1. SQL server tooyour 목록 돌아가서 열 hello **tenants1-&lt;사용자&gt;**  hello 테 넌 트 데이터베이스를 보유 하는 서버입니다. 각 테넌트 데이터베이스는 50eDTU 표준 풀의 _탄력적 표준_ 데이터베이스입니다. 또한 것을 볼 수는 _빨간색 단풍나무 레이싱_ 데이터베이스, hello 테 넌 트 데이터베이스를 이전에 프로 비전 합니다.

   ![server](./media/sql-database-saas-tutorial/server.png)

## <a name="monitor-hello-pool"></a>Hello 풀 모니터

몇 분 동안 hello 부하 생성기를 실행 하는 경우 충분 한 데이터에 사용할 수 있는 toostart hello 모니터링 풀 및 데이터베이스에 기본 제공 되는 기능 중 일부를 살펴보면 되어야 합니다.

1. Toohello 서버 찾아보기 **tenants1-&lt;사용자&gt;**를 클릭 하 고 **Pool1** hello 풀에 대 한 리소스 사용률을 볼 수 (hello 차트 뒤에 1 시간 동안 실행 hello 부하 생성기) :

   ![풀 모니터링](./media/sql-database-saas-tutorial/monitor-pool.png)

이 두 차트는 SaaS 응용 프로그램 워크로드에 대해 탄력적 풀 및 SQL Database가 얼마나 적합한지 보기 좋게 설명하고 있습니다. 각 전환 tooas 것 처럼 쉽게 40 Edtu 50 eDTU 풀에서 지원 되는 4 개의 데이터베이스. 각 필요 toobe는 S2 경우 독립 실행형 데이터베이스 프로 비전 된 경우 (50 DTU) toosupport hello 필요 합니다. 독립 실행형 S2 데이터베이스 4의 hello 비용은 거의 3 hello 가격 hello 풀의와 hello 풀에 아직 충분 한 리소스가 더 많은 데이터베이스에 대 한 합니다. 실제 상황에서 SQL 데이터베이스의 고객 200 eDTU 풀의 too500 데이터베이스를 현재 실행 중인 합니다. 자세한 내용은 참조 hello [성능 모니터링 자습서](sql-database-saas-tutorial-performance-monitoring.md)합니다.


## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음에 대해 알아보았습니다.

> [!div class="checklist"]

> * 어떻게 toodeploy hello Wingtip SaaS 응용 프로그램
> * Hello 서버, 풀 및 hello 응용 프로그램을 구성 하는 데이터베이스에 대 한
> * 테 넌 트는 않습니다 hello 사용 하 여 매핑된 tootheir 데이터 *카탈로그*
> * 어떻게 tooprovision 새 테 넌 트
> * Tooview 풀 사용률이 toomonitor 활동 테 넌 트 방식
> * Toodelete 샘플 리소스 toostop 청구의 관계

이제 hello 시도 [프로 비전 및 카탈로그 자습서](sql-database-saas-tutorial-provision-and-catalog.md)



## <a name="additional-resources"></a>추가 리소스

* 추가 [자습서에 구축 된 hello Wingtip SaaS 응용 프로그램](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* 탄력적 풀에 대 한 toolearn 참조 [ *Azure SQL 탄력적 풀 이란*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)
* toolearn 탄력적 작업에 대 한 참조 [ *관리 확장 클라우드 데이터베이스*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)
* 다중 테 넌 트 SaaS 응용 프로그램에 대 한 toolearn 참조 [ *디자인 다중 테 넌 트 SaaS 응용 프로그램에 대 한 패턴은*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)
