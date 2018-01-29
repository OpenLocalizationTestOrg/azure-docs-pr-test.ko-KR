---
title: "테넌트당 데이터베이스 SaaS 자습서 - Azure SQL Database | Microsoft Docs"
description: "Azure SQL Database를 사용하는 테넌트당 데이터베이스 및 기타 SaaS 패턴을 보여 주는 Wingtip Tickets SaaS 다중 테넌트 응용 프로그램을 배포하고 탐색합니다."
keywords: "SQL Database 자습서"
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2017
ms.author: genemi
ms.openlocfilehash: 5342b5290fab9826a2b38cd7ada63a6736c77601
ms.sourcegitcommit: 094061b19b0a707eace42ae47f39d7a666364d58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="deploy-and-explore-a-multi-tenant-saas-application-that-uses-the-database-per-tenant-pattern-with-azure-sql-database"></a>Azure SQL Database에서 테넌트당 데이터베이스 패턴을 사용하는 다중 테넌트 SaaS 응용 프로그램을 배포하고 탐색합니다.

이 자습서에서는 테넌트의 Wingtip Tickets SaaS *테넌트당 데이터베이스* 응용 프로그램(Wingtip)을 배포하고 탐색합니다. 이 앱은 테넌트당 데이터베이스 패턴을 사용하여 여러 테넌트의 데이터를 저장합니다. 이 앱은 SaaS 시나리오를 간소화하는 Azure SQL Database의 기능을 보여 주도록 설계되었습니다.

**Azure에 배포**라는 레이블의 파란색 단추를 클릭하고 5분 후에 다중 테넌트 SaaS 응용 프로그램이 설치됩니다. 이 앱에는 Microsoft Azure 클라우드에서 실행되는 Azure SQL Database가 포함됩니다. 앱은 각각 고유한 데이터베이스를 사용하여 3개의 샘플 테넌트에서 배포됩니다. 모든 데이터베이스는 SQL *탄력적 풀*에 배포됩니다. 앱은 Azure 구독에 배포됩니다. 앱의 개별 구성 요소를 탐색하고 작업할 수 있는 전체 액세스 권한이 있습니다. 응용 프로그램 C# 소스 코드 및 관리 스크립트는 [WingtipTicketsSaaS-DbPerTenant GitHub 리포지토리][github-wingtip-dpt]에서 사용할 수 있습니다.

이 자습서에서는 다음에 대해 알아봅니다.

> [!div class="checklist"]
> - Wingtip SaaS 응용 프로그램을 배포하는 방법.
> - 응용 프로그램 소스 코드 및 관리 스크립트를 가져올 위치.
> - 서버, 풀 및 앱을 구성하는 데이터베이스 정보.
> - *카탈로그*를 통해 테넌트가 데이터에 매핑되는 방법.
> - 새 테넌트를 프로비전하는 방법.
> - 앱에서 테넌트 활동을 모니터링하는 방법.

[관련된 일련의 자습서](saas-dbpertenant-wingtip-app-overview.md#sql-database-wingtip-saas-tutorials)에서는 다양한 SaaS 디자인 및 관리 패턴을 탐색합니다. 이 자습서는 이 초기 배포 이후에도 빌드됩니다.
자습서를 사용하는 경우 제공된 스크립트를 검토하여 다양한 SaaS 패턴을 구현하는 방법을 확인할 수 있습니다.
스크립트는 SaaS 응용 프로그램 개발을 간소화하는 SQL Database의 기능을 보여줍니다.

## <a name="prerequisites"></a>필수 조건

이 자습서를 수행하려면 다음 필수 조건이 완료되었는지 확인합니다.

* Azure PowerShell이 설치되었습니다. 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.

## <a name="deploy-the-wingtip-tickets-saas-application"></a>Wingtip Tickets SaaS 응용 프로그램 배포

앱 배포:

1. 다음 매개 변수에 필요한 값을 선택하고 기억합니다.

    - **사용자**: 이니셜 뒤에 숫자와 같은 짧은 값을 선택합니다. 예: *af1* 사용자 매개 변수에는 문자, 숫자 및 하이픈만 포함할 수 있습니다(공백 없음). 첫 번째 및 마지막 문자는 문자 또는 숫자여야 합니다. 모든 문자가 소문자인 것이 좋습니다.
    - **리소스 그룹**: Wingtip 응용 프로그램을 배포할 때마다 새 리소스 그룹에 다른 고유 이름을 선택해야 합니다. 리소스 그룹의 기본 이름에 사용자 이름을 추가하는 것이 좋습니다. 예제 리소스 그룹 이름은 *wingtip-af1*일 수 있습니다. 다시 언급하지만 모든 문자가 소문자인 것이 좋습니다.

2. 파란색 **Azure에 배포** 단추를 클릭하여 Azure Portal에서 Wingtip Tickets SaaS 테넌트당 데이터베이스 배포 템플릿을 엽니다.

   <a href="https://aka.ms/deploywingtipdpt" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

3. 템플릿에 필수 매개 변수의 값을 입력합니다.

    > [!IMPORTANT]
    > 일부 인증 및 서버 방화벽은 데모 목적으로 의도적으로 보호되지 않습니다. *새 리소스 그룹을 만드는* 것이 좋습니다. 기존 리소스 그룹, 서버 또는 풀을 사용하지 마세요. 이 응용 프로그램, 스크립트 또는 배포된 리소스를 프로덕션에 사용하지 마세요. 관련된 결제를 중지하려면 응용 프로그램을 완료할 때 이 리소스 그룹을 삭제합니다.

    - **리소스 그룹** - **새로 만들기**를 선택하고 리소스 그룹에서 이전에 선택한 고유 **이름**을 입력합니다. 
    - **위치** - 드롭다운 목록에서 **위치**를 선택합니다.
    - **사용자** - 앞에서 선택한 사용자 이름 값을 사용합니다.

4. 응용 프로그램을 배포합니다.

    - 사용 약관에 동의하려면 클릭합니다.
    - **구매**를 클릭합니다.

5. **알림**(검색 상자 오른쪽 벨 아이콘)을 클릭하여 배포 상태를 모니터링합니다. Wingtip Tickets SaaS 앱을 배포하는 데는 5분 정도 걸립니다.

   ![배포 성공](media/saas-dbpertenant-get-started-deploy/succeeded.png)

## <a name="download-and-unblock-the-wingtip-tickets-management-scripts"></a>Wingtip Tickets 관리 스크립트 다운로드 및 차단 해제

응용 프로그램이 배포되는 동안 소스 코드 및 관리 스크립트를 다운로드합니다.

> [!IMPORTANT]
> .zip 파일이 외부 원본에서 다운로드되고 추출될 때 Windows에서 실행 가능한 콘텐츠(스크립트, DLL)를 차단할 수 있습니다. Zip 파일에서 스크립트를 추출할 경우 다음 단계에 따라 추출하기 전에 .zip 파일을 차단 해제하세요. 차단을 해제하면 스크립트를 실행할 수 있습니다.

1. [WingtipTicketsSaaS-DbPerTenant GitHub 리포지토리][github-wingtip-dpt]로 이동합니다.
2. **복제 또는 다운로드**를 클릭합니다.
3. **ZIP 다운로드**를 클릭하고 파일을 저장합니다.
4. **WingtipTicketsSaaS-DbPerTenant-master.zip** 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.
5. **일반** 탭에서 **차단 해제**를 선택하고 **적용**을 클릭합니다.
6. **확인**을 클릭합니다.
7. 파일의 압축을 풉니다.

스크립트는 *..\\WingtipTicketsSaaS-DbPerTenant-master\\Learning Modules* 폴더에 있습니다.

## <a name="update-the-user-configuration-file-for-this-deployment"></a>이 배포에 대한 사용자 구성 파일 업데이트

스크립트를 실행하기 전에 **UserConfig.psm1**에서 *리소스 그룹* 및 *사용자* 값을 업데이트합니다. 이러한 변수를 배포 중에 사용한 값으로 설정합니다.

1. *PowerShell ISE*에서 ...*Learning Modules*\\UserConfig.psm1\\을 엽니다. 
2. 배포에 대한 특정 값(줄 10 및 11에서만)으로 *ResourceGroupName* 및 *Name*을 업데이트합니다.
3. 변경 내용을 저장합니다.

이러한 값은 거의 모든 스크립트에서 참조됩니다.

## <a name="run-the-application"></a>응용 프로그램 실행

앱은 이벤트를 호스트하는 장소를 표시합니다. 장소 유형에는 콘서트 홀, 재즈 클럽 및 스포츠 클럽 등이 포함됩니다. Wingtip Tickets에서 장소는 테넌트로 등록됩니다. 테넌트가 되면 장소에 이벤트를 나열하고 고객에게 티켓을 판매하는 편리한 방법을 제공할 수 있습니다. 각 장소는 해당 이벤트를 나열하고 티켓을 판매하는 개인 설정된 웹 사이트를 얻게 됩니다.

앱에서 내부적으로 각 테넌트는 SQL 탄력적 풀에 배포된 SQL Database를 가져옵니다.

중앙 **이벤트 허브** 페이지는 배포에 있는 테넌트의 링크 목록을 제공합니다.

1. 웹 브라우저에서 *이벤트 허브*(http://events.wingtip-dpt.&lt;사용자&gt;.trafficmanager.net)를 엽니다. 여기서 &lt;사용자&gt;를 배포의 사용자 값으로 대체합니다.

    ![Events Hub](media/saas-dbpertenant-get-started-deploy/events-hub.png)

2. *이벤트 허브*에서 **Fabrikam Jazz Club**을 클릭합니다.

    ![이벤트](./media/saas-dbpertenant-get-started-deploy/fabrikam.png)

#### <a name="azure-traffic-manager"></a>Azure Traffic Manager

Wingtip 응용 프로그램에서는 [*Azure Traffic Manager*](../traffic-manager/traffic-manager-overview.md)를 사용하여 들어오는 요청의 분산을 제어할 수 있습니다. 한 테넌트의 Events Hub에 액세스하는 URL은 다음 형식을 준수해야 합니다.

- http://events.wingtip-dpt.&lt;USER&gt;.trafficmanager.net/fabrikamjazzclub

이전 형식의 부분을 다음 표에서 설명합니다.

| URL 부분 | 설명 |
| :------- | :---------- |
| http://events.wingtip-dpt | Wingtip 앱의 이벤트 부분입니다.<br /><br />***-dpt*** 부분은 Wingtip의 *데이터베이스당 테넌트* 구현을 약간 다른 구현과 구분합니다. 예를 들어 다른 설명서에서는 *Standalong*(*-sa*) 또는 *다중 테넌트 DB*의 Wingtip을 제공합니다. |
| .*&lt;USER&gt;* | 예에서는 *af1*입니다. |
| .trafficmanager.net/ | Azure Traffic Manager, 기준 URL입니다. |
| fabrikamjazzclub | *Fabrikam Jazz Club*이라는 테넌트의 경우입니다. |
| &nbsp; | &nbsp; |

1. 테넌트 이름은 이벤트 앱에 의해 URL에서 구문 분석됩니다.
2. 테넌트 이름은 키를 만드는 데 사용됩니다.
3. 테넌트 데이터베이스의 위치를 가져오기 위해 카탈로그에 액세스하는 데 키를 사용합니다.
    - 카탈로그는 *분할 맵 관리*를 사용하여 구현됩니다.
4. *Events Hub*는 카탈로그에서 확장된 메타데이터를 사용하여 이벤트 URL 목록을 가져옵니다.

프로덕션 환경에서는 일반적으로 CNAME DNS 레코드를 만들어 [*회사 인터넷 도메인이 Traffic Manager 프로필을 가리키도록*](../traffic-manager/traffic-manager-point-internet-domain.md) 합니다.

## <a name="start-generating-load-on-the-tenant-databases"></a>테넌트 데이터베이스에서 부하 생성 시작

이제 앱이 배포되었으므로 작동해 보겠습니다.
*Demo-LoadGenerator* PowerShell 스크립트는 모든 테넌트 데이터베이스에서 실행되는 워크로드를 시작합니다.
많은 SaaS 앱상의 실제 부하는 간헐적이고 예측할 수 없습니다.
이 형식의 부하를 시뮬레이션하려면 생성기는 각 테넌트의 작업에 대해 임의의 스파이크 또는 버스트된 부하를 생성합니다.
버스트는 임의 간격으로 발생합니다.
부하 패턴이 나타나는 데는 몇 분 정도가 걸립니다. 따라서 부하를 모니터링하기 전에 생성기를 최소한 3~4분 실행하는 것이 가장 좋습니다.

1. *PowerShell ISE*에서 ...\\Learning Modules\\Utilities\\*Demo-LoadGenerator.ps1* 스크립트를 엽니다.
2. **F5** 키를 눌러 스크립트를 실행하고 부하 생성기를 시작합니다. (지금은 기본 매개 변수 값을 그대로 적용합니다.)

*Demo-LoadGenerator.ps1*을 다시 실행하는 것 외에는 동일한 PowerShell ISE 인스턴스를 다시 사용하지 마십시오. 다른 PowerShell 스크립트를 실행해야 하는 경우 별도 PowerShell ISE를 시작합니다.

#### <a name="rerun-with-different-parameters"></a>다른 매개 변수를 사용하여 다시 실행

다른 매개 변수를 사용하여 워크로드 테스트를 다시 실행하려는 경우 다음 단계를 따릅니다.

1. *LoadGenerator.ps1*을 중지합니다.
    - **Ctrl+C**를 사용하거나 **중지** 단추를 클릭합니다.
    - 이 중지는 실행 중인 불완전한 백그라운드 작업을 중지하거나 영향을 주지 않습니다.

2. *Demo-LoadGenerator.ps1*을 다시 실행합니다.
    - 이 다시 실행은 먼저 *sp_CpuLoadGenerator*를 실행하고 있는 백그라운드 작업을 중지합니다.

또는 PowerShell ISE 인스턴스를 종료할 수 있습니다. 그러면 모든 백그라운드 작업을 중지합니다. 그런 다음 PowerShell ISE의 새 인스턴스를 시작하고 *Demo-LoadGenerator.ps1*을 다시 실행합니다.

#### <a name="monitor-the-background-jobs"></a>백그라운드 작업을 모니터링합니다.

백그라운드 작업을 제어하고 모니터링하려면 다음과 같은 cmdlet을 사용할 수 있습니다.

- Get-Job
- Receive-Job
- Stop-Job

#### <a name="demo-loadgeneratorps1-actions"></a>Demo-LoadGenerator.ps1 작업

*Demo-LoadGenerator.ps1*은 고객 트랜잭션의 활성 워크로드를 모방합니다. 다음 단계는 *Demo-LoadGenerator.ps1*이 시작하는 작업의 시퀀스를 설명합니다.

1. *Demo-LoadGenerator.ps1* 전경에서 *LoadGenerator.ps1*을 시작합니다.
    - 이러한.ps1 파일은 모두 *학습 모듈\\유틸리티\\* 폴더 아래에 저장됩니다.

2. *LoadGenerator.ps1*은 카탈로그에 등록된 모든 테넌트 데이터베이스를 반복합니다.

3. 각 테넌트 데이터베이스의 경우 *LoadGenerator.ps1*은 *sp_CpuLoadGenerator*라는 Transact-SQL 저장 프로시저를 실행하기 시작합니다.
    - 실행은 *Invoke-SqlAzureWithRetry* cmdlet을 호출하여 백그라운드에서 시작됩니다.
    - *sp_CpuLoadGenerator*는 60초라는 기본 기간 동안 SQL SELECT 문을 반복합니다. SELECT 문제 간의 시간 간격은 매개 변수 값에 따라 달라집니다.
    - .sql 파일은 *WingtipTenantDB\\dbo\\StoredProcedures\\* 아래에 저장됩니다.

4. 각 테넌트 데이터베이스의 경우 *LoadGenerator.ps1*은 *Start-Job* cmdlet을 시작합니다.
    - *Start-Job*은 티켓 판매의 워크로드를 모방합니다.

5. *LoadGenerator.ps1*을 계속 실행하여 프로비전된 새 테넌트에 대해 모니터링합니다.

&nbsp;

다음 섹션을 계속하기 전에 부하 생성기를 작업 호출 상태로 계속 실행합니다.

## <a name="provision-a-new-tenant"></a>새 테넌트 프로비전

초기 배포는 세 가지 샘플 테넌트를 만듭니다. 이제 또 다른 테넌트를 만들어 배포된 응용 프로그램에 어떻게 영향을 미치는지 확인합니다. Wingtip 앱에서 새 테넌트를 프로비전하는 워크플로는 [프로비전 및 카탈로그 자습서](saas-dbpertenant-provision-and-catalog.md)에 설명됩니다. 이 단계에서는 새 테넌트를 만드는 데 1분이 걸리지 않습니다.

1. *PowerShell ISE*에서 ...\\Learning Modules\Provision and Catalog\\*Demo-ProvisionAndCatalog.ps1*을 엽니다.
2. **F5** 키를 눌러 스크립트를 실행합니다. (지금은 기본값을 그대로 적용합니다.)

   > [!NOTE]
   > 대부분의 Wingtip SaaS 스크립트에서는 *$PSScriptRoot*를 사용하여 다른 스크립트에 있는 함수를 호출하기 위해 폴더를 탐색합니다. 이 변수는 **F5** 키를 눌러 전체 스크립트를 실행할 경우에만 평가됩니다.  **F8** 키를 사용하여 선택 영역을 강조 표시하고 실행하면 오류가 발생할 수 있습니다. 따라서 **F5** 키를 눌러 스크립트를 실행합니다.

새 테넌트 데이터베이스는 다음과 같습니다.

- SQL 탄력적 풀에 만들어집니다.
- 초기화되었습니다.
- 카탈로그에 등록됩니다.

성공적으로 프로비전한 후에 새 테넌트의 *이벤트* 사이트가 브라우저에 나타납니다.

![새 테넌트](./media/saas-dbpertenant-get-started-deploy/red-maple-racing.png)

*Events Hub*를 새로 고치면 목록에 새 테넌트가 나타납니다.

## <a name="explore-the-servers-pools-and-tenant-databases"></a>서버, 풀 및 테넌트 데이터베이스 탐색

테넌트 컬렉션에 대해 부하 실행을 시작했으므로 배포된 리소스 중 일부를 살펴보겠습니다.

1. [Azure Portal](http://portal.azure.com)에서 SQL 서버 목록으로 이동하여 **catalog-dpt-&lt;USER&gt;** 서버를 엽니다.
    - 카탈로그 서버에는 두 가지 데이터베이스인 **tenantcatalog** 및 **basetenantdb**(새 테넌트를 만들기 위해 복사한 템플릿 데이터베이스)가 포함됩니다.

   ![데이터베이스](./media/saas-dbpertenant-get-started-deploy/databases.png)

2. SQL 서버 목록으로 이동합니다.

3. 테넌트 데이터베이스가 있는 **tenants1-dpt-&lt;USER&gt;** 서버를 엽니다.

4. 다음 항목을 확인합니다.
    - 각 테넌트 데이터베이스는 50eDTU 표준 풀의 *탄력적 표준* 데이터베이스입니다.
    - 이전에 프로비전한 테넌트 데이터베이스인 *Red Maple Racing* 데이터베이스입니다.

   ![server](./media/saas-dbpertenant-get-started-deploy/server.png)

## <a name="monitor-the-pool"></a>풀 모니터링

*LoadGenerator.ps1*을 몇 분 동안 실행한 후에 일부 모니터링 기능을 살펴보기에 충분한 데이터를 사용할 수 있어야 합니다. 이러한 기능은 풀 및 데이터베이스에 빌드됩니다.

**tenants1-dpt-&lt;USER&gt;** 서버로 이동하고, **Pool1**을 클릭하여 풀의 리소스 사용률을 확인합니다. 다음 차트에서 부하 생성기를 1시간 동안 실행했습니다.

   ![풀 모니터링](./media/saas-dbpertenant-get-started-deploy/monitor-pool.png)

- **리소스 사용률**이라는 레이블의 첫 번째 차트는 풀 eDTU 사용량을 보여줍니다.
- 두 번째 차트는 풀에서 상위 5개 데이터베이스의 eDTU 사용률을 보여줍니다.

두 차트는 탄력적 풀 및 SQL Database가 SaaS 응용 프로그램 워크로드에 얼마나 적합한지 설명합니다.
차트에서는 4개의 데이터베이스가 40개의 eDTU로 버스트되는 것을 보여줍니다. 하지만 모든 데이터베이스는 안전하게 50개의 eDTU 풀에서 지원됩니다. 50개의 eDTU 풀은 더 많은 워크로드를 지원할 수 있습니다.
데이터베이스가 독립 실행형 데이터베이스로 프로비전된 경우, 데이터베이스는 각각 버스트를 지원하는 S2(50 DTU)가 되어야 합니다.
독립 실행형 S2 데이터베이스 4개의 비용은 풀의 가격의 거의 3배입니다.
실제 상황에서 SQL Database 고객은 현재 200eDTU 풀에서 최대 500개의 데이터베이스까지 실행 중입니다.
자세한 내용은 [성능 모니터링 자습서](saas-dbpertenant-performance-monitoring.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Wingtip Tickets SaaS 테넌트당 데이터베이스 응용 프로그램을 기반으로 빌드되는 추가 자습서](saas-dbpertenant-wingtip-app-overview.md#sql-database-wingtip-saas-tutorials)
- 탄력적 풀에 대한 자세한 내용은 [*Azure SQL 탄력적 풀이란?*](sql-database-elastic-pool.md)을 참조하세요.
- 탄력적 작업에 대해 알아보려면 [*규모가 확장된 클라우드 데이터베이스 관리*](sql-database-elastic-jobs-overview.md)를 참조하세요.
- 다중 테넌트 SaaS 응용 프로그램에 대해 알아보려면 [*다중 테넌트 SaaS 응용 프로그램을 위한 디자인 패턴*](saas-tenancy-app-design-patterns.md)을 참조하세요.


## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음에 대해 알아보았습니다.

> [!div class="checklist"]
> - Wingtip Tickets SaaS 응용 프로그램을 배포하는 방법
> - 서버, 풀 및 앱을 구성하는 데이터베이스 정보
> - *카탈로그*를 사용하여 데이터에 매핑된 테넌트
> - 새 테넌트를 프로비전하는 방법
> - 풀 사용률을 검토하여 테넌트 작업을 모니터링하는 방법
> - 샘플 리소스를 삭제하여 관련 결제를 중지하는 방법

다음으로 [프로비전 및 카탈로그 자습서](saas-dbpertenant-provision-and-catalog.md)를 사용해 보세요.



<!-- Link references. -->

[github-wingtip-dpt]: https://github.com/Microsoft/WingtipTicketsSaaS-DbPerTenant 

