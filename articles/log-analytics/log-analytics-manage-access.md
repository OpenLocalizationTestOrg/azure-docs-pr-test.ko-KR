---
title: "Azure 로그 분석 및 hello OMS 포털에서 작업 영역 aaaManage | Microsoft Docs"
description: "사용자, 계정, 작업 영역 및 Azure 계정에서 다양 한 관리 작업을 사용 하 여 Azure 로그 분석 및 hello OMS 포털의 작업 영역을 관리할 수 있습니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: d0e5162d-584b-428c-8e8b-4dcaa746e783
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/06/2017
ms.author: magoedte
ms.openlocfilehash: 570e6c1f13ad28f120ecd65052d00c4ca986ac98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-workspaces"></a>작업 영역 관리

toomanage 액세스 tooLog 분석, 다양 한 관리 작업 관련된 tooworkspaces를 수행합니다. 이 문서에서는 조언과 절차 toomanage 작업 영역 모범 사례를 제공 합니다. 작업 영역은 기본적으로 hello 계정에 대 한 간단한 구성 정보와 계정 정보를 포함 하는 컨테이너입니다. 조직의 다른 구성원이 여러 작업 영역 toomanage 서로 다른 데이터 집합을 모두에서 수집 되는 또는 IT 인프라의 일부를 사용할 수 있습니다.

작업 영역 toocreate 해야합니다.

1. Azure 구독이 있어야 합니다.
2. 작업 영역 이름을 선택합니다.
3. 구독 hello 작업 영역을 연결 합니다.
4. 지리적 위치를 선택합니다.

## <a name="determine-hello-number-of-workspaces-you-need"></a>Hello 필요한 작업 영역 수 결정
작업 영역은 Azure 리소스 이며 컨테이너를 데이터 수집, 집계, 분석 및 hello Azure 포털에에서 표시 합니다.

Azure 구독 당 여러 작업 영역 있으며 하나의 작업 영역 보다 toomore 액세스를 가질 수 있습니다. 작업 영역 최소화 hello 수 tooquery 있으며 간에 상호 연결 hello 대부분의 데이터 되지 않으므로 가능한 tooquery 여러 작업 영역에서 합니다. 이 여기서는 경우는 것이 유용한 toocreate 두 개 이상의 하나의 작업 영역을 설명 합니다.

현재 작업 영역은 다음을 제공합니다.

* 데이터 저장소의 지리적 위치
* 대금 청구에 대한 세분성
* 데이터 격리
* 구성 범위

Hello 앞에 특성에 따라, 사용할 수 있습니다 toocreate 여러 작업 영역 경우.

* 글로벌 회사이며 데이터 주권 또는 규정 준수 때문에 특정 지역에 저장된 데이터가 필요합니다.
* Azure를 사용 하는 중이 고 tooavoid 아웃 바운드 데이터 전송 요금이 작업 영역을 포함 하면 hello Azure 리소스를 관리 하는 대로 동일한 지역 hello 합니다.
* 원하는 tooallocate 요금 toodifferent 부서 또는 비즈니스 그룹의 사용에 따라 합니다. 각 부서 또는 비즈니스 그룹에 대 한 작업 영역을 만들면 Azure 청구서 및 사용량 문의 각 작업 영역에 대 한 hello 요금에 별도로 표시 됩니다.
* 관리 되는 서비스 공급자 및 다른 고객의 데이터에서 격리 하는 관리 각 고객에 대 한 tookeep hello 로그 분석 데이터가 필요 합니다.
* 여러 고객을 관리 하 고 각 고객이 / 부서 / 비즈니스 그룹 toosee 자신의 데이터 하지만 hello 데이터가 아닌 다른 사용자에 대 한 합니다.

에이전트 toocollect 데이터를 사용 하는 경우 다음을 할 수 있습니다 [각 에이전트 tooreport tooone 또는 더 많은 작업 영역 구성](log-analytics-windows-agents.md)합니다.

System Center Operations Manager를 사용하는 경우 각 Operations Manager 관리 그룹을 한 작업 영역에만 연결할 수 있습니다. Operations Manager에서 관리 하는 컴퓨터에서 hello Microsoft Monitoring Agent를 설치 하 고 hello 에이전트 보고서 tooboth Operations Manager와 다른 로그 분석 작업 영역 수 있습니다.

### <a name="workspace-information"></a>작업 영역 정보

Hello Azure 포털에서에서 작업 영역에 대 한 세부 정보를 볼 수 있습니다. 또한 hello OMS 포털에서 세부 정보를 볼 수 있습니다.

#### <a name="view-workspace-information-in-hello-azure-portal"></a>Hello Azure 포털에서에서 작업 영역 정보 보기

1. 그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com) Azure 구독을 사용 하 여 합니다.
2. Hello에 **허브** 메뉴를 클릭 하 여 **더 많은 서비스** hello 리소스 목록에 입력 하 고 **로그 분석**합니다. 입력을 시작할 때 hello 사용자 입력에 따라 필터를 나열 합니다. **Log Analytics**를 클릭합니다.  
    ![Azure 허브](./media/log-analytics-manage-access/hub.png)  
3. Hello 구독 블레이드에서 로그 분석 작업 영역을 선택 합니다.
4. 작업 영역 블레이드 hello hello 작업 영역 및 추가 정보에 대 한 링크에 대 한 세부 정보를 표시 합니다.  
    ![작업 영역 정보](./media/log-analytics-manage-access/workspace-details.png)  


## <a name="manage-accounts-and-users"></a>계정 및 사용자 관리
각 작업 영역 수, 연관 된 여러 계정을 있으며 각 계정 (Microsoft 계정 또는 조직 계정) access toomultiple 작업 영역을 가질 수 있습니다.

기본적으로 hello Microsoft 계정 또는 조직 계정을 hello 작업 영역을 만드는 hello hello 작업 영역의 관리자가 됩니다.

액세스 tooa 로그 분석 작업 영역을 제어 하는 두 개의 사용 권한 모델 가지가 있습니다.

1. 레거시 Log Analytics 사용자 역할
2. [Azure 역할 기반 액세스](../active-directory/role-based-access-control-configure.md)

다음 표에 hello 각 권한 모델을 사용 하 여 설정할 수 있는 hello 액세스를 요약 되어 있습니다.

|                          | Log Analytics 포털 | Azure Portal | API(PowerShell 포함) |
|--------------------------|----------------------|--------------|----------------------------|
| Log Analytics 사용자 역할 | 예                  | 아니요           | 아니요                         |
| Azure 역할 기반 액세스  | 예                  | 예          | 예                        |

> [!NOTE]
> 로그 분석은 이동 toouse Azure 역할 기반 액세스 hello 사용 권한 모델으로 hello 로그 분석 사용자 역할을 대체 합니다.
>
>

hello 레거시 로그 분석 사용자 역할 제어 hello에서 수행 하는 액세스 tooactivities [로그 분석 포털](https://mms.microsoft.com)합니다.

hello도 활동 뒤에 Azure 권한이 필요 합니다.

| 동작                                                          | 필요한 Azure 권한 | 참고 |
|-----------------------------------------------------------------|--------------------------|-------|
| 관리 솔루션 추가 및 제거                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/*` <br> `Microsoft.OperationsManagement/*` <br> `Microsoft.Automation/*` <br> `Microsoft.Resources/deployments/*/write` | |
| Hello 가격 책정 계층을 변경 합니다.                                       | `Microsoft.OperationalInsights/workspaces/*/write` | |
| 데이터 보기 hello에 *백업* 및 *사이트 복구* 솔루션 타일 | 관리자 / 공동 관리자 | 리소스 액세스 hello 클래식 배포 모델을 사용 하 여 배포 |
| Hello Azure 포털에서에서 작업 영역 만들기                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/workspaces/*` ||


### <a name="managing-access-toolog-analytics-using-azure-permissions"></a>분석 tooLog 액세스 관리 Azure 권한을 사용 하 여
toogrant 액세스 toohello 로그 분석 작업 영역을 Azure의 권한을 사용 하 여 hello 단계에 따라 [역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](../active-directory/role-based-access-control-configure.md)합니다.

Azure의 Log Analytics에는 기본 제공되는 2개의 사용자 역할이 있습니다.
- Log Analytics 독자
- Log Analytics 참가자

멤버의 hello *로그 분석 판독기* 역할 수 있습니다.
- 모든 모니터링 데이터 검색 및 보기 
- 모든 Azure 리소스에 Azure 진단의 hello 구성 보기 등의 설정을 모니터링 하는 보기입니다.

| 형식    | 사용 권한 | 설명 |
| ------- | ---------- | ----------- |
| 동작 | `*/read`   | 기능 tooview 모든 리소스 및 리소스 구성 합니다. 볼 수 있습니다. <br> 가상 컴퓨터 확장 상태 <br> 리소스에 대한 Azure 진단 구성 <br> 모든 리소스의 모든 속성 및 설정 |
| 동작 | `Microsoft.OperationalInsights/workspaces/analytics/query/action` | 기능 tooperform v2 로그 검색 쿼리 |
| 동작 | `Microsoft.OperationalInsights/workspaces/search/action` | 기능 tooperform v1 로그 검색 쿼리 |
| 동작 | `Microsoft.Support/*` | 기능 tooopen 지원 사례 |
|동작 없음 | `Microsoft.OperationalInsights/workspaces/sharedKeys/read` | 작업 영역 키 필요한 toouse hello 데이터 컬렉션 API 및 tooinstall 에이전트의 읽기를 방지합니다. |


멤버의 hello *로그 분석 참가자* 역할 수 있습니다.
- 모든 모니터링 데이터 읽기 
- Automation 계정 만들기 및 구성
- 관리 솔루션 추가 및 제거
- 저장소 계정 키 읽기 
- Azure Storage에서 로그 수집 구성
- 다음을 포함한 Azure 리소스의 모니터링 설정 편집
  - Hello VM 확장 tooVMs 추가
  - 모든 Azure 리소스에 대한 Azure 진단 구성

> [!NOTE] 
> Hello 기능 tooadd는 가상 컴퓨터 확장 tooa 가상 컴퓨터 toogain 대 한 모든 권한을 가상 컴퓨터를 사용할 수 있습니다.

| 사용 권한 | 설명 |
| ---------- | ----------- |
| `*/read`     | 기능 tooview 모든 리소스 및 리소스 구성 합니다. 볼 수 있습니다. <br> 가상 컴퓨터 확장 상태 <br> 리소스에 대한 Azure 진단 구성 <br> 모든 리소스의 모든 속성 및 설정 |
| `Microsoft.Automation/automationAccounts/*` | 기능 toocreate를 추가 하 고 runbook을 편집 하는 Azure 자동화 계정을 구성 하 고 |
| `Microsoft.ClassicCompute/virtualMachines/extensions/*` <br> `Microsoft.Compute/virtualMachines/extensions/*` | 추가, 업데이트 및 hello Microsoft Monitoring Agent 확장 및 Linux 확장에 대 한 hello OMS 에이전트를 포함 하 여 가상 컴퓨터 확장을 제거 합니다. |
| `Microsoft.ClassicStorage/storageAccounts/listKeys/action` <br> `Microsoft.Storage/storageAccounts/listKeys/action` | 보기 hello 저장소 계정 키입니다. 필요한 Azure 저장소 계정에서 tooconfigure 로그 분석 tooread 로그 |
| `Microsoft.Insights/alertRules/*` | 규칙 추가, 업데이트 및 제거 |
| `Microsoft.Insights/diagnosticSettings/*` | Azure 리소스에 대한 진단 설정 추가, 업데이트 및 제거 |
| `Microsoft.OperationalInsights/*` | Log Analytics 작업 영역에 대한 구성 추가, 업데이트 및 제거 |
| `Microsoft.OperationsManagement/*` | 관리 솔루션 추가 및 제거 |
| `Microsoft.Resources/deployments/*` | 디렉터리를 만들고 삭제합니다. 솔루션, 작업 공간 및 자동화 계정 추가 및 제거에 필요 |
| `Microsoft.Resources/subscriptions/resourcegroups/deployments/*` | 디렉터리를 만들고 삭제합니다. 솔루션, 작업 공간 및 자동화 계정 추가 및 제거에 필요 |

필요는 tooadd 및 제거 하는 사용자가 tooa 사용자 역할 toohave `Microsoft.Authorization/*/Delete` 및 `Microsoft.Authorization/*/Write` 권한.

이러한 역할 toogive 사용자 액세스를 사용 하 여 다른 범위에:
- 구독-hello 구독에서 Access tooall 작업 영역
- 리소스 그룹-hello 리소스 그룹에 대 한 액세스 tooall 작업 영역
- 리소스-액세스 tooonly hello 지정 된 작업 영역

사용 하 여 [사용자 정의 역할](../active-directory/role-based-access-control-custom-roles.md) toocreate 역할과 함께 hello 특정 사용 권한 필요 합니다.

### <a name="azure-user-roles-and-log-analytics-portal-user-roles"></a>Azure 사용자 역할 및 Log Analytics 포털 사용자 역할
최소 Azure hello 로그 분석 작업 영역에 대 한 권한이 읽기, hello를 클릭 하 여 hello 로그 분석 포털을 열 수에서 경우 **OMS 포털** hello 로그 분석 작업 영역을 볼 때 작업 합니다.

Hello 로그 분석 포털을 열 때 toousing hello 레거시 로그 분석 사용자 역할을 전환 합니다. Hello 로그 분석 포털에서 역할 할당이 없는 경우 서비스 hello [검사 hello hello 작업 영역에 있는 Azure 권한을](https://docs.microsoft.com/rest/api/authorization/permissions#Permissions_ListForResource)합니다.
Hello 로그 분석 포털에서 역할 할당은 다음과 같이 사용 하 여 결정 됩니다.

| 조건                                                   | 할당된 Log Analytics 사용자 역할 | 참고 사항 |
|--------------------------------------------------------------|----------------------------------|-------|
| 사용자 계정이 속한 tooa 레거시 로그 분석 사용자 역할     | hello 로그 분석 사용자 역할 지정 | |
| 계정은 tooa 레거시 로그 분석 사용자 역할에 속하지 않습니다. <br> 전체 Azure 권한 toohello 작업 영역 (`*` 권한 <sup>1</sup>) | 관리자 ||
| 계정은 tooa 레거시 로그 분석 사용자 역할에 속하지 않습니다. <br> 전체 Azure 권한 toohello 작업 영역 (`*` 권한 <sup>1</sup>) <br> `Microsoft.Authorization/*/Delete` 및 `Microsoft.Authorization/*/Write`의 *not actions* | 참여자 ||
| 계정은 tooa 레거시 로그 분석 사용자 역할에 속하지 않습니다. <br> Azure 읽기 권한 | 읽기 전용 ||
| 계정은 tooa 레거시 로그 분석 사용자 역할에 속하지 않습니다. <br> Azure 권한이 인식되지 않음 | 읽기 전용 ||
| CSP(클라우드 솔루션 공급자) 관리 구독용 <br> hello 연결 된 Azure Active Directory toohello 작업 영역에 hello 계정으로 로그인 | 관리자 | 일반적으로 hello 고객 CSP에 |
| CSP(클라우드 솔루션 공급자) 관리 구독용 <br> hello 계정으로 로그인 했으면 hello 연결 된 Azure Active Directory toohello 작업 영역에 없는 | 참여자 | 일반적으로 hello CSP |

<sup>1</sup> 너무 참조[Azure 권한을](../active-directory/role-based-access-control-custom-roles.md) 역할 정의 대 한 자세한 내용은 합니다. 역할의 동작을 평가할 때 `*` 너무 동일 하지 않습니다`Microsoft.OperationalInsights/workspaces/*`합니다.

Hello Azure 포털에 대해 알아 두어야 포인트 tookeep 일부:

* Hello 참조 http://mms.microsoft.com를 사용 하 여 toohello OMS 포털에 로그인 할 때 **작업 영역 선택** 목록입니다. 이 목록은 Log Analytics 사용자 역할을 보유하는 작업 영역만 포함합니다. toosee hello 작업 영역에 있는 액세스할 toowith Azure 구독을 hello URL의 일부로 toospecify 테 넌 트가 필요 합니다. 예제: `mms.microsoft.com/?tenant=contoso.com` hello 테 넌 트 식별자는 마지막 부분의 hello 전자 메일 주소에서 toosign를 사용 하는 경우가 많습니다.
* Toonavigate 직접 적용 해야 tooa 포털 toousing Azure에 액세스 하려는 경우 다음 권한을 hello URL의 일부로 toospecify hello 리소스가 필요 합니다. 것은 가능한 tooget PowerShell을 사용 하 여이 URL입니다.

  예: `(Get-AzureRmOperationalInsightsWorkspace).PortalUrl`.

  hello URL 같이 표시 됩니다.`https://eus.mms.microsoft.com/?tenant=contoso.com&resource=%2fsubscriptions%2faaa5159e-dcf6-890a-a702-2d2fee51c102%2fresourcegroups%2fdb-resgroup%2fproviders%2fmicrosoft.operationalinsights%2fworkspaces%2fmydemo12`

### <a name="managing-users-in-hello-oms-portal"></a>Hello OMS 포털에서 사용자 관리
사용자 및 그룹 hello에 관리 **사용자 관리** hello 아래의 탭 **계정** hello 설정 페이지에서 탭 합니다.   

![사용자 관리](./media/log-analytics-manage-access/setup-workspace-manage-users.png)


#### <a name="add-a-user-tooan-existing-workspace"></a>추가 사용자 tooan 기존 작업 영역
단계 tooadd 사용자 또는 그룹 tooa 작업 영역을 다음 hello를 사용 합니다.

1. Hello OMS 포털에서 클릭 hello **설정** 바둑판식으로 배열입니다.
2. Hello 클릭 **계정** 탭 클릭 한 후 hello **사용자 관리** 탭 합니다.
3. Hello에 **사용자 관리** 섹션에서 계정 유형 tooadd hello: **조직 계정**, **Microsoft 계정**, **Microsoft 지원**.

   * Microsoft 계정을 선택 했다면 Microsoft 계정 hello와 관련 된 hello 사용자 hello 전자 메일 주소를 입력 합니다.
   * 조직 계정을 선택 했다면 hello 사용자의 일부를 입력/드롭다운 상자에 그룹의 이름이 나 메일 별칭 및 사용자 및 그룹을 일치 하는 목록을 표시 합니다. 사용자 또는 그룹을 선택합니다.
   * 문제 해결을 Microsoft 지원 엔지니어 또는 다른 Microsoft 직원 임시 액세스 tooyour 작업 영역 toohelp toogive Microsoft 기술 지원 서비스를 사용 합니다.

     > [!NOTE]
     > 최상의 성능을 위해서는 hello hello 하나의 OMS 계정 toothree와 연결 된 Active Directory 그룹 수를 제한-관리자, 참가자 및 읽기 전용 사용자에 대 한 하나 있습니다. 더 많은 그룹을 사용 하 여 로그 분석의 hello 성능 영향을 줄 수 있습니다.
     >
     >
4. Hello 유형의 tooadd 사용자 또는 그룹 선택: **관리자**, **참가자**, 또는 **읽기 전용 사용자**합니다.  
5. **추가**를 클릭합니다.

   Microsoft 계정을 추가 하는 경우 사용자가 제공한 toohello 전자 메일 초대 toojoin hello 작업 영역에 전송 됩니다. Hello 사용자 뒤 hello 초대 toojoin OMS의에서 hello 지침 hello 사용자 hello 작업 영역을 액세스할 수 있습니다.
   조직 계정을 추가 하는 경우 hello 사용자 로그 분석 즉시 액세스할 수 있습니다.  

#### <a name="edit-an-existing-user-type"></a>기존 사용자 유형 편집
OMS 계정과 연결 된 사용자에 대 한 hello 계정 역할을 변경할 수 있습니다. Hello 다음 역할 옵션을 사용할 수 있습니다.

* *관리자*: 사용자를 관리하고, 모든 경고를 보고 작업하며, 서버를 추가 및 제거할 수 있습니다.
* *참여자*: 모든 경고를 보고 작업하며 서버를 추가 및 제거할 수 있습니다.
* *읽기 전용사용자*: 읽기 전용으로 표시된 사용자는 다음을 할 수 없습니다.

  1. 솔루션을 추가/제거합니다. hello 솔루션 갤러리를 숨깁니다.
  2. **내 대시보드**에서 타일을 추가/수정/제거합니다.
  3. 보기 hello **설정을** 페이지입니다. hello 페이지 숨겨집니다.
  4. Hello 검색 보기, PowerBI 구성, 저장 된 검색 및 경고에서 작업은 숨겨집니다.

#### <a name="tooedit-an-account"></a>tooedit 계정
1. Hello OMS 포털에서 클릭 hello **설정** 바둑판식으로 배열입니다.
2. Hello 클릭 **계정** 탭 클릭 한 후 hello **사용자 관리** 탭 합니다.
3. Toochange hello 사용자에 대 한 hello 역할을 선택 합니다.
4. Hello 확인 대화 상자에서 클릭 **예**합니다.

### <a name="remove-a-user-from-a-workspace"></a>작업 영역에서 사용자 제거
Hello 단계 tooremove 사용자 작업 영역에서 다음을 사용 합니다. 제거 hello 사용자 hello 작업 영역은 닫히지 않습니다. 대신, 해당 사용자 및 hello 작업 영역 간의 hello 연결을 제거 합니다. 사용자가 여러 작업 영역과 연결에 해당 사용자 tooOMS 로그인 그렇지만 아니며 해당 작업 영역을 확인할 수 있습니다.

1. Hello OMS 포털에서 클릭 hello **설정** 바둑판식으로 배열입니다.
2. Hello 클릭 **계정** 탭 클릭 한 후 hello **사용자 관리** 탭 합니다.
3. 클릭 **제거** tooremove 되도록 다음 toohello 사용자 이름입니다.
4. Hello 확인 대화 상자에서 클릭 **예**합니다.

### <a name="add-a-group-tooan-existing-workspace"></a>추가 그룹 tooan 기존 작업 영역
1. 이전 섹션 "tooadd 사용자 tooan 기존 작업 영역" hello, 1-4 단계를 수행 합니다.
2. **사용자/그룹 선택**에서 **그룹**을 선택합니다.  
   ![추가 그룹 tooan 기존 작업 영역](./media/log-analytics-manage-access/add-group.png)
3. Hello 표시 이름 또는 전자 메일 주소를 입력 hello 그룹에 대 한 tooadd 원할 것입니다.
4. Hello 목록 결과에서 hello 그룹을 선택 하 고 클릭 **추가**합니다.

## <a name="link-an-existing-workspace-tooan-azure-subscription"></a>기존 작업 영역 tooan Azure 구독 연결
2016 년 9 월 26 일 이후에 만든 모든 작업 영역에 연결 된 Azure 구독을 만들 때 tooan 이어야 합니다. 이 날짜 이전에 만든 작업 영역에 로그인 할 때 연결 된 tooa 작업 영역 이어야 합니다. Hello Azure 포털에서에서 hello 작업 영역을 만들 때 또는 사용자 작업 영역 tooan Azure 구독을 연결 하면 Azure Active Directory 조직 계정으로 연결 됩니다.

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-oms-portal"></a>toolink 작업 영역 tooan hello OMS 포털에서 Azure 구독

- Hello OMS 포털에 로그인 할 때 메시지 표시 tooselect Azure 구독 됩니다. Hello 구독 toolink tooyour 작업 영역을 선택 하 고 클릭 선택 **링크**합니다.  
    ![Azure 구독 연결](./media/log-analytics-manage-access/required-link.png)

    > [!IMPORTANT]
    > 작업 영역 toolink Azure 계정 액세스 toohello toolink 원하는 작업 영역에 이미 있어야 합니다.  즉, tooaccess hello Azure 포털을 사용 하는 hello 계정 이어야 합니다 **동일 hello** hello 계정 tooaccess hello 작업 영역을 사용 합니다. 그렇지 않은 경우 [사용자 tooan 기존 작업 영역을 추가할](#add-a-user-to-an-existing-workspace)합니다.

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-azure-portal"></a>toolink 작업 영역 tooan hello Azure 포털에서에서 Azure 구독
1. Hello에 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. **Log Analytics**를 찾아서 선택합니다.
3. 기존 작업 영역 목록이 표시됩니다. **추가**를 클릭합니다.  
   ![작업 영역 목록](./media/log-analytics-manage-access/manage-access-link-azure01.png)
4. **OMS 작업 영역**에서 **또는 기존 항목 연결**을 클릭합니다.  
   ![기존 항목 연결](./media/log-analytics-manage-access/manage-access-link-azure02.png)
5. **필수 설정 구성**을 클릭합니다.  
   ![필수 설정 구성](./media/log-analytics-manage-access/manage-access-link-azure03.png)
6. Hello 되지 않은 작업 영역 목록이 아직 tooyour Azure 계정을 연결 하는 것이 표시 됩니다. 작업 영역을 선택합니다.  
   ![작업 영역 선택](./media/log-analytics-manage-access/manage-access-link-azure04.png)
7. 필요한 경우에 다음 항목 hello에 대 한 값을 변경할 수 있습니다.
   * 구독
   * 리소스 그룹
   * 위치
   * 가격 책정 계층   
     ![값 변경](./media/log-analytics-manage-access/manage-access-link-azure05.png)
8. **확인**을 클릭합니다. 이제 hello 영역은 연결 된 tooyour Azure 계정입니다.

> [!NOTE]
> Hello 작업 영역 표시 되지 않으면 toolink, 원하는 경우 Azure 구독 액세스 toohello hello OMS 포털을 사용 하 여 만든 작업 영역이 없습니다.  hello OMS 포털에서 toogrant 액세스 toothis 계정을 참조 [사용자 tooan 기존 작업 영역을 추가할](#add-a-user-to-an-existing-workspace)합니다.
>
>

## <a name="upgrade-a-workspace-tooa-paid-plan"></a>계획을 지불 하는 작업 영역 tooa 업그레이드
OMS에 대한 작업 영역 플랜 유형에는 **무료**, **독립 실행형** 및 **OMS**의 세 가지가 있습니다.  Hello 사용 중인 *무료* 계획, 500MB의 데이터를 받 tooLog 분석 당 제한이 있습니다.  이 용량을 초과 하는 경우이 제한 초과 하 여 데이터를 수집 하지 하 여 작업 영역 유료 tooa 계획 tooavoid toochange를 할 수 있습니다. 언제든지 플랜 유형을 변경할 수 있습니다.  OMS 가격 책정에 대한 자세한 내용은 [가격 정보](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-pricing)를 참조하세요.

### <a name="using-entitlements-from-an-oms-subscription"></a>OMS 구독에서 자격 사용
OMS E1, E2 OMS OMS 또는 System Center 용 OMS 추가 기능 구매 으로부터의 toouse hello 자격 선택 hello *OMS* OMS 로그 분석의 계획 합니다.

OMS 구독을 구입 hello 자격 tooyour 기업 계약 추가 됩니다. 본이 계약에 따라 생성 하는 모든 Azure 구독 hello 자격을 사용할 수 있습니다. 이 구독에서 모든 작업 영역에는 hello OMS 권한은 사용합니다.

작업 영역 사용 hello OMS 구독에서에서 적용 된 tooyour 자격 임을 tooensure를 해야 합니다.

1. Hello hello OMS 구독에 포함 된 기업 계약의 일부인 Azure 구독에서 작업 영역 만들기
2. 선택 hello *OMS* hello 작업 영역에 대 한 계획

> [!NOTE]
> 작업 영역 2016 년 9 월 26 일 전에 생성 된 하 고 가격 계획에 로그 분석은 *프리미엄*,이 작업 영역 System Center 용 OMS 추가 기능의 hello에서 자격을 사용 하 여 합니다. 권한에 toohello 변경 하 여 사용할 수도 있습니다 *OMS* 가격 책정 계층입니다.
>
>

hello OMS 구독 권한은 hello Azure 또는 OMS 포털에 표시 되지 않습니다. 자격 및 hello 엔터프라이즈 포털에서에서 사용량을 볼 수 있습니다.  

Toochange hello 작업 영역에 연결 된 Azure 구독을 해야 하는 경우에 hello Azure PowerShell을 사용할 수 있습니다 [Move-azurermresource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet.

### <a name="using-azure-commitment-from-an-enterprise-agreement"></a>엔터프라이즈 규약을 통해 Azure 약정 사용
OMS 구독 없는 경우 OMS의 각 구성 요소에 대해 따로따로 지불 하 고 hello 사용, Azure 청구서에 나타납니다.

현금 약정 Azure enterprise 등록 toowhich hello에 있는 경우 연결 된 Azure 구독, 통화 커밋 남은 hello에 대 한 로그 분석의 사용 금액 자동으로 됩니다.

Hello 작업 영역을 hello Azure 구독에 연결 된를 hello Azure PowerShell을 사용할 수 있습니다 toochange가 필요한 경우 [Move-azurermresource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet.  

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-azure-portal"></a>Hello Azure 포털에서에서 가격 책정 계층을 지불 하는 작업 영역 tooa 변경
1. Hello에 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. **Log Analytics**를 찾아서 선택합니다.
3. 기존 작업 영역 목록이 표시됩니다. 작업 영역을 선택합니다.  
4. Hello 작업 영역 블레이드에서 아래 **일반**, 클릭 **가격 책정 계층**합니다.  
5. **가격 책정 계층**에서 가격 책정 계층 선택을 클릭한 다음 **선택**을 클릭합니다.  
    ![요금제 선택](./media/log-analytics-manage-access/manage-access-change-plan03.png)
6. 참조 hello Azure 포털에서에서 보기를 새로 고칠 때 **가격 책정 계층** 선택한 hello 계층에 대 한 업데이트 합니다.  
    ![업데이트된 요금제](./media/log-analytics-manage-access/manage-access-change-plan04.png)

> [!NOTE]
> 연결 된 자동화 계정을 tooan 작업 영역을 사용 하는 경우 전에 선택할 수 있습니다 hello *독립 실행형 (GB 당)* 가격 책정 계층을 삭제 해야 모든 **자동화 및 제어** 솔루션 hello 자동화의 연결을 해제 하 고 계정입니다. Hello 작업 영역 블레이드에서 아래 **일반**, 클릭 **솔루션** 솔루션 toosee 및 삭제 합니다. 자동화 계정을 toounlink hello hello hello에 대 한 자동화 계정의 hello 이름을 클릭 **가격 책정 계층** 블레이드입니다.
>
>

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-oms-portal"></a>Hello OMS 포털에서 가격 책정 계층을 지불 하는 작업 영역 tooa 변경

toochange hello hello OMS 포털을 사용 하 여 가격 책정 계층, Azure 구독이 있어야 합니다.

1. Hello OMS 포털에서 클릭 hello **설정** 바둑판식으로 배열입니다.
2. Hello 클릭 **계정** 탭 클릭 한 후 hello **Azure 구독 및 데이터 계획** 탭 합니다.
3. 가격 책정 계층 toouse 원하는 hello를 클릭 합니다.
4. **Save**를 클릭합니다.  
   ![구독 및 데이터 계획](./media/log-analytics-manage-access/subscription-tab.png)

새 데이터 계획 hello 웹 페이지의 위쪽 hello에 OMS 포털 리본 메뉴에에서 표시 됩니다.

![OMS 리본 메뉴](./media/log-analytics-manage-access/data-plan-changed.png)


## <a name="change-how-long-log-analytics-stores-data"></a>Log Analytics의 데이터 저장 기간 변경

무료 가격 책정 계층 hello, 로그 분석 보이게 hello를 사용할 수 있는 데이터의 마지막 7 일입니다.
Hello 표준 가격 책정 계층에 로그 분석 데이터의 지난 30 일 동안 사용할 수 있는 hello을 만듭니다.
Hello 프리미엄 가격 책정 계층에서 로그 분석 데이터의 최근 365 일간 사용할 수 있는 hello을 만듭니다.
독립 실행형 hello 및 가격 책정 계층을 기본적으로 OMS 로그 분석 데이터의 마지막 31 일 사용할 수 있는 hello을 만듭니다.

독립 실행형 hello를 사용 하는 경우와 OMS 가격 책정 계층을 too2 년 분량의 데이터 (730 일)을 유지할 수 있습니다. Hello 기본값은 31 일 보다 오래 저장 된 데이터를 한 데이터 보존 요금이 부과 됩니다. 가격 책정에 대한 자세한 내용은 [초과 요금](https://azure.microsoft.com/pricing/details/log-analytics/)을 참조하세요.

데이터 보존의 toochange hello 길이:

1. Hello에 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. **Log Analytics**를 찾아서 선택합니다.
3. 기존 작업 영역 목록이 표시됩니다. 작업 영역을 선택합니다.  
4. 작업 영역 블레이드에서 hello **일반**, 클릭 **보존**합니다.  
5. 슬라이더 tooincrease hello를 사용 하 여 hello 보존의 날짜 수가 줄어들고 클릭 **저장**합니다.  
    ![보존 변경](./media/log-analytics-manage-access/manage-access-change-retention01.png)

## <a name="change-an-azure-active-directory-organization-for-a-workspace"></a>작업 영역의 Azure Active Directory 조직 변경

작업 영역의 Azure Active Directory 조직을 변경할 수 있습니다. Azure Active Directory 조직 변경 hello tooadd 사용자 및 해당 디렉터리 toohello 작업 영역에서 그룹 수 있습니다.

### <a name="toochange-hello-azure-active-directory-organization-for-a-workspace"></a>작업 영역에 대 한 Azure Active Directory 조직 toochange hello

1. Hello hello OMS 포털의 설정 페이지를 클릭 **계정** hello를 클릭 한 다음 **사용자 관리** 탭 합니다.  
2. 조직 계정에 대 한 hello 정보를 검토 한 다음 클릭 **변경 조직**합니다.  
    ![조직 변경](./media/log-analytics-manage-access/manage-access-add-adorg01.png)
3. Azure Active Directory 도메인의 관리자에 게에 대 한 hello id 정보를 입력 합니다. 나중에 작업 영역 연결된 tooyour Azure Active Directory 도메인 임을 나타내는 승인이 표시 합니다.  
    ![연결 된 작업 영역 승인](./media/log-analytics-manage-access/manage-access-add-adorg02.png)


## <a name="delete-a-log-analytics-workspace"></a>Log Analytics 작업 영역 삭제
로그 분석 작업 영역을 삭제 하면 모든 관련 된 데이터 작업 영역 tooyour 30 일 이내 hello OMS 서비스에서에서 삭제 됩니다.

관리자가 사용자가 여러 명이면 hello 작업 영역과 연결 된 경우 hello 해당 사용자와 hello 작업 영역 간의 연결이 끊어집니다. 다른 작업 영역과 연결 된 hello 사용자가 OMS를 사용 하 여 이러한 다른 작업 영역과 계속 수 있습니다. 그러나 다른 작업 영역과 연결 되지 않은 경우 작업 영역 toouse OMS toocreate가 필요한 다음 합니다.

### <a name="toodelete-a-workspace"></a>toodelete 작업 영역
1. Hello에 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. **Log Analytics**를 찾아서 선택합니다.
3. 기존 작업 영역 목록이 표시됩니다. 원하는 toodelete hello 작업 영역을 선택 합니다.
4. Hello 작업 영역 블레이드 클릭 **삭제**합니다.  
    ![delete](./media/log-analytics-manage-access/delete-workspace01.png)
5. Hello 삭제 작업 영역 확인 대화 상자에서 클릭 **예**합니다.

## <a name="next-steps"></a>다음 단계
* 참조 [연결 Windows 컴퓨터 tooLog 분석](log-analytics-windows-agents.md) tooadd 에이전트 고 데이터를 수집 합니다.
* [로그 분석 솔루션 hello 솔루션 갤러리에서에서 추가](log-analytics-add-solutions.md) tooadd 기능 및 수집 데이터입니다.
* [로그 분석에서 프록시 및 방화벽 설정을 구성](log-analytics-proxy-firewall.md) 조직에서 사용 하는 프록시 서버나 방화벽 에이전트 hello 로그 분석 서비스와 통신할 수 있도록 하는 경우.
