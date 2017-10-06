---
title: "Operations Management Suite (OMS)에서 365 aaaOffice 솔루션 | Microsoft Docs"
description: "이 문서는 OMS에서 Office 365 hello 솔루션의 구성 및 사용에 세부 정보를 제공합니다.  로그 분석에서 만들어진 Office 365 hello 레코드에 대 한 자세한 설명을 포함 합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: a1507745251ff015abb785bae8352fea7cea0734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-solution-in-operations-management-suite-oms"></a>OMS(Operations Management Suite)의 Office 365 솔루션

![Office 365 로고](media/oms-solution-office-365/icon.png)

Office 365 솔루션이 Operations Management Suite (OMS) 용 hello toomonitor을 사용 하면 로그 분석에 Office 365 환경입니다.  

- 동작 추세를 식별할 뿐 아니라 Office 365 계정 tooanalyze 사용 패턴에 대 한 사용자 작업 모니터링 합니다. 예를 들어 hello 가장 인기 있는 SharePoint 사이트 또는 조직 외부 공유 되는 파일 등의 특정 사용 시나리오를 추출할 수 있습니다.
- 관리자 활동 tootrack 구성 변경 또는 높은 권한 작업을 모니터링 합니다.
- 조직 요구 사항에 따라 사용자 지정할 수 있는 부적절한 사용자 행동을 검색하고 조사할 수 있습니다.
- 감사 및 규정 준수 방식을 제시할 수 있습니다. 예를 들어 hello 감사 및 준수 프로세스를 얻을 수 있는 중요 한 기밀 파일에서 파일 액세스 작업을 모니터링할 수 있습니다.
- 조직의 Office 365 활동 데이터를 토대로 OMS 검색 기능을 사용해 운영상의 문제를 해결할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
hello 다음은 설치 및 구성 되 고 필요한 이전 toothis 솔루션입니다.

- 조직 Office 365 구독
- 전역 관리자 사용자 계정의 자격 증명
- 해야 tooreceive 감사 데이터 [감사 구성](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&rs=en-US&ad=US#PickTab=Before_you_begin) Office 365 구독에 있습니다.  [사서함 감사](https://technet.microsoft.com/library/dn879651.aspx)는 별도로 구성합니다.  Hello 솔루션을 설치 하 고 감사 구성 되지 않은 경우 다른 데이터를 수집할 수 있습니다.
 


## <a name="management-packs"></a>관리 팩
이 솔루션은 연결된 관리 그룹에서 관리 팩을 설치하지 않습니다.
  

## <a name="configuration"></a>구성
수행한 후 [hello Office 365 솔루션 tooyour 구독 추가](../log-analytics/log-analytics-add-solutions.md), tooconnect 있는 것 tooyour Office 365 구독 합니다.

1. Hello 프로세스를 사용 하 여 OMS 작업 영역에서 설명 하는 hello 경고 관리 솔루션 tooyour 추가 [솔루션 추가](../log-analytics/log-analytics-add-solutions.md)합니다.
2. 너무 이동**설정을** hello OMS 포털의.
3. **연결된 원본** 아래에서 **Office 365**를 선택합니다.
4. **Office 365 연결**을 클릭합니다.<br>![Office 365 연결](media/oms-solution-office-365/configure.png)
5. TooOffice 365 구독에 대 한 전역 관리자 계정으로 로그인 합니다. 
6. hello 구독 hello 솔루션은 모니터링 하는 hello 워크 로드로 나열 됩니다.<br>![Office 365 연결](media/oms-solution-office-365/connected.png) 


## <a name="data-collection"></a>데이터 수집
### <a name="supported-agents"></a>지원되는 에이전트
Office 365 솔루션이 hello hello 중 하나에서 데이터를 검색 하지 않습니다 [OMS 에이전트](../log-analytics/log-analytics-data-sources.md)합니다.  즉, Office 365에서 직접 데이터를 검색합니다.

### <a name="collection-frequency"></a>수집 빈도
Office 365 보냅니다는 [webhook 알림](https://msdn.microsoft.com/office-365/office-365-management-activity-api-reference#receiving-notifications) tooLog 분석 될 때마다 세부 데이터와 레코드가 만들어집니다.

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여
Office 365 hello 솔루션 tooyour OMS 작업 영역에 추가 하면 hello **Office 365** tooyour OMS 대시보드에 타일 추가 됩니다. 이 타일의 업데이트 준수 및 사용자 환경에 개수 및 그래픽으로 나타낸 hello 수의 컴퓨터를 표시합니다.<br><br>
![Office 365 요약 타일](media/oms-solution-office-365/tile.png)  

Hello 클릭 **Office 365** 타일 tooopen hello **Office 365** 대시보드 합니다.

![Office 365 대시보드](media/oms-solution-office-365/dashboard.png)  

hello 대시보드는 다음 표에 hello에 hello 열을 포함 합니다. 각 열에는 hello 상위 10 개의 경고 개수를 비교 하 여 hello에 대 한 열의 조건을 범위 및 시간 범위를 지정 했는지 나열 됩니다. Hello 열 hello 맨 아래에 모든 참조를 클릭 하 여 또는 hello 열 머리글을 클릭 하 여 hello 전체 목록을 제공 하는 로그 검색을 실행할 수 있습니다.

| 열 | 설명 |
|:--|:--|
| 작업 | 모든 모니터링된 Office 365 구독에서 활성 사용자 hello에 대 한 정보를 제공합니다. 시간에 따라 발생 하는 활동 수 toosee hello 수도 됩니다.
| Exchange | Exchange Server 사서함 추가 권한 또는 Set-mailbox 하는 등의 작업 hello 필드도 함께 표시 합니다. |
| SharePoint | 사용자가 SharePoint 문서에서 수행 하는 hello 상위 활동을 표시 합니다. 이 타일에서 드릴 다운 하면 hello 검색 페이지 hello 대상 문서 및이 활동의 hello 위치와 같은 이러한 활동의 hello 세부 정보를 표시 합니다. 예를 들어 파일에 액세스 하는 이벤트에 대 한 됩니다 수 toosee hello 문서 액세스 되는 정의와 연결 된 계정 이름 및 IP 주소입니다. |
| Azure Active Directory | 사용자 암호 다시 설정, 로그인 시도 등 자주 수행하는 사용자 활동이 포함됩니다. 드릴 다운 하면 수 toosee hello 세부 정보 결과 상태를 hello와 같은 이러한 활동의 됩니다. 대부분이 Azure Active Directory에서 toomonitor 의심 스러운 활동을 원하는 경우에 유용 합니다. |




## <a name="log-analytics-records"></a>Log Analytics 레코드

Office 365 hello 솔루션에 의해 hello 로그 분석 작업 영역에서 만든 모든 레코드는 **형식** 의 **OfficeActivity**합니다.  hello **OfficeWorkload** 속성은 Office 365 서비스 hello 레코드가 참조 너무 Exchange, AzureActiveDirectory, SharePoint 또는 OneDrive를 결정 합니다.  hello **RecordType** 속성 연산의 hello 유형을 지정 합니다.  hello 각 작업 유형에 대해 달라 집니다 속성과 hello 테이블 아래에 표시 됩니다.

### <a name="common-properties"></a>공용 속성
다음과 같은 속성 hello는 일반적인 tooall Office 365 레코드입니다.

| 속성 | 설명 |
|:--- |:--- |
| 형식 | *OfficeActivity* |
| ClientIP | hello hello 활동 기록 된 때 사용 된 hello 장치의 IP 주소입니다. hello IP 주소는 IPv4 또는 IPv6 주소 형식으로 표시 됩니다. |
| OfficeWorkload | Hello 레코드를 참조 하는 office 365 서비스입니다.<br><br>AzureActiveDirectory<br>Exchange<br>SharePoint|
| 작업 | hello 사용자 또는 관리자 활동의 hello 이름입니다.  |
| OrganizationId | 조직의 Office 365 테 넌 트에 대 한 GUID 번호입니다. 이 값은 항상 될 hello 동일한 조직에 대해,는 자신이 hello Office 365 서비스에 관계 없이 발생 합니다. |
| RecordType | 수행한 작업의 유형입니다. |
| ResultStatus | Hello 동작 (에 지정 된 hello Operation 속성이 필요) 성공 했는지 여부를 나타냅니다. 가능한 값은 Succeeded, PartiallySucceded 또는 Failed입니다. Exchange 관리자 활동 hello 값은 True 또는 False입니다. |
| UserId | hello hello 레코드가 기록; 유발한 hello 동작을 수행한 hello 사용자의 UPN (User Principal Name) 예를 들어 my_name@my_domain_name합니다. SHAREPOINT\system 또는 NTAUTHORITY\SYSTEM과 같은 시스템 계정이 수행한 활동에 대한 레코드도 포함됩니다. | 
| UserKey | UserId 속성 hello에서 식별 된 hello 사용자에 대 한 대체 ID입니다.  예를 들어이 속성이 비즈니스 및 Exchange에 대 한 OneDrive, SharePoint에서 사용자가 수행 하는 이벤트에 대 한 hello passport 고유 ID (PUID)으로 채워집니다. 이 속성에는 동일한 값으로 다른 서비스 및 이벤트에서 발생 하는 이벤트에 대 한 UserID 속성 hello 시스템 계정에서 수행 하는 hello도 지정할 수 있습니다.|
| UserType | hello 작업을 수행한 사용자의 hello 형식입니다.<br><br>관리자<br>응용 프로그램<br>DcAdmin<br>일반<br>Reserved<br>ServicePrincipal<br>시스템 |


### <a name="azure-active-directory-base"></a>Azure Active Directory 기본 속성
다음과 같은 속성 hello는 일반적인 tooall Azure Active Directory 레코드입니다.

| 속성 | 설명 |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AzureActiveDirectory_EventType | Azure AD 이벤트의 hello 형식입니다. |
| ExtendedProperties | hello는 hello Azure AD 이벤트의 속성을 확장 합니다. |


### <a name="azure-active-directory-account-logon"></a>Azure Active Directory 계정 로그온
이러한 레코드는 Active Directory 사용자에 toolog 시도할 때 만들어집니다.

| 속성 | 설명 |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectoryAccountLogon |
| 응용 프로그램 | Office 15 같은 hello 계정 로그인 이벤트를 트리거하는 hello 응용 프로그램입니다. |
| 클라이언트 | 클라이언트 hello에 대 한 세부 정보, 장치, 운영 체제, 장치 및 hello 계정 로그인 이벤트의 hello에 사용 했던 장치 브라우저. |
| LoginStatus | OrgIdLogon.LoginStatus에서 직접 생성되는 속성입니다. 다양 한 흥미로운 로그온 실패의 hello 매핑 알고리즘을 경고 하 여 수행할 수 있었습니다. |
| UserDomain | 테 넌 트 Identity 정보 (TII) 번호입니다. | 


### <a name="azure-active-directory"></a>Azure Active Directory
이러한 레코드는 변경 또는 추가 tooAzure Active Directory 개체 이루어집니다 때 생성 됩니다.

| 속성 | 설명 |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AADTarget | hello 작업 (Operation 속성 hello로 식별)에서 수행 된 hello 사용자입니다. |
| 행위자 | hello 사용자 또는 서비스 사용자는 hello 작업을 수행 합니다. |
| ActorContextId | hello 행위자 hello hello 조직의 GUID에 속해 있습니다. |
| ActorIpAddress | hello 행위자의 IP 주소를 IPV4 또는 IPV6 주소 형식입니다. |
| InterSystemsId | hello hello Office 365 서비스 내에서 구성 요소에서 hello 동작을 추적 하는 GUID입니다. |
| IntraSystemId |   hello Azure Active Directory tootrack hello 동작에 의해 생성 된 GUID입니다. |
| SupportTicketId | hello 고객 "act-에-를 대신 하 여-의" 상황에서 hello 동작에 대 한 티켓 ID를 지원 합니다. |
| TargetContextId | hello GUID의 대상된 사용자 hello hello 조직에 속해 있습니다. |


### <a name="data-center-security"></a>데이터 센터 보안
다음 레코드는 데이터 센터 보안 감사 데이터에서 생성됩니다.  

| 속성 | 설명 |
|:--- |:--- |
| EffectiveOrganization | 권한 상승/cmdlet hello hello 테 넌 트의 hello 이름을 대상으로 합니다. |
| ElevationApprovedTime | hello 상승 승인에 대 한 hello 타임 스탬프입니다. |
| ElevationApprover | Microsoft 관리자의 hello 이름입니다. |
| ElevationDuration | 권한 상승은 hello에 대 한 활성 상태 였던 hello 기간입니다. |
| ElevationRequestId |  Hello 권한 상승 요청에 대 한 고유 식별자입니다. |
| ElevationRole | hello 역할 hello 권한 상승에 대 한 요청 되었습니다. |
| ElevationTime | hello 시작 시간 hello 상승입니다. |
| Start_Time | hello 시작 시간 hello cmdlet 실행입니다. |


### <a name="exchange-admin"></a>Exchange 관리
이러한 레코드는 tooExchange 구성 변경 될 때 생성 됩니다.

| 속성 | 설명 |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeAdmin |
| ExternalAccess |  데이터 센터 서비스 계정이 나 Microsoft 데이터 센터 담당자가 조직에서 사용자가 또는 위임 된 관리자가 hello cmdlet가 실행 하는지 여부를 지정 합니다. hello 값 False 조직에서 사용자가 해당 hello cmdlet가 실행을 나타냅니다. hello 값 true이 고 데이터 센터 담당자, 데이터 센터 서비스 계정 또는 위임 된 관리자가 해당 hello cmdlet가 실행을 나타냅니다. |
| ModifiedObjectResolvedName |  Hello hello cmdlet에서 수정 된 hello 개체의 사용자 식별 이름입니다. Hello cmdlet hello 개체를 수정 하는 경우에 로깅됩니다. |
| OrganizationName | hello 테 넌 트의 hello 이름입니다. |
| OriginatingServer | 어떤 hello cmdlet가 실행 하는 hello 서버 hello 이름입니다. |
| 매개 변수 | hello 이름과 hello 작업 속성에서에서 식별 되는 hello cmdlet과 함께 사용 된 모든 매개 변수에 대 한 값입니다. |


### <a name="exchange-mailbox"></a>Exchange 사서함
이러한 레코드는 변경 또는 추가 사항을 tooExchange 사서함을 수행 하는 생성 됩니다.

| 속성 | 설명 |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| ClientInfoString | 브라우저 버전, Outlook 버전 및 모바일 장치 정보 등 사용된 tooperform hello 작업이 hello 전자 메일 클라이언트에 대 한 정보입니다. |
| Client_IPAddress | hello hello 작업이 기록 되어 때 사용 된 hello 장치의 IP 주소입니다. hello IP 주소는 IPv4 또는 IPv6 주소 형식으로 표시 됩니다. |
| ClientMachineName | hello Outlook 클라이언트를 호스팅하는 hello 컴퓨터 이름입니다. |
| ClientProcessName | hello 전자 메일 클라이언트를 사용 하는 tooaccess hello 사서함입니다. |
| ClientVersion | hello 전자 메일 클라이언트의 hello 버전입니다. |
| InternalLogonType | 내부용으로 예약된 속성입니다. |
| Logon_Type | Hello 사서함 액세스 하 고 기록 된 hello 작업을 수행한 사용자의 hello 유형을 나타냅니다. |
| LogonUserDisplayName |    hello hello 작업을 수행한 hello 사용자의 친숙 한 이름입니다. |
| LogonUserSid | hello hello 작업을 수행한 hello 사용자의 SID입니다. |
| MailboxGuid | 번호는 액세스 hello 사서함의 Exchange GUID입니다. |
| MailboxOwnerMasterAccountSid | 사서함 소유자 계정의 마스터 계정 SID입니다. |
| MailboxOwnerSid | hello hello 사서함 소유자의 SID입니다. |
| MailboxOwnerUPN | hello hello 사서함 액세스를 소유 하는 hello 사용자의 전자 메일 주소입니다. |


### <a name="exchange-mailbox-audit"></a>Exchange 사서함 감사
다음 레코드는 사서함 감사 항목을 만들면 생성됩니다.

| 속성 | 설명 |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| 항목 | 작업을 수행 시 어떤 hello hello 항목을 나타냅니다. | 
| SendAsUserMailboxGuid | hello 했던 hello 사서함의 Exchange GUID 액세스 toosend 메일. |
| SendAsUserSmtp | 가장 hello 사용자의 SMTP 주소입니다. |
| SendonBehalfOfUserMailboxGuid | hello 했던 hello 사서함의 Exchange GUID 액세스 대신 toosend 메일. |
| SendOnBehalfOfUserSmtp | 주체인 hello 전자 메일 hello 사용자의 SMTP 주소 전송 됩니다. |


### <a name="exchange-mailbox-audit-group"></a>Exchange 사서함 감사 그룹
이러한 레코드는 변경 또는 추가 사항을 tooExchange 그룹 사항이 있을 때 만들어집니다.

| 속성 | 설명 |
|:--- |:--- |
| OfficeWorkload | Exchange |
| OfficeWorkload | ExchangeItemGroup |
| AffectedItems | Hello 그룹의 각 항목에 대 한 정보입니다. |
| CrossMailboxOperations | Hello 작업이 둘 이상의 사서함을 포함 하는 경우를 나타냅니다. |
| DestMailboxId | Hello CrossMailboxOperations 매개 변수는 True 하는 경우에 설정 합니다. Hello 대상 사서함 GUID를 지정합니다. |
| DestMailboxOwnerMasterAccountSid | Hello CrossMailboxOperations 매개 변수는 True 하는 경우에 설정 합니다. Hello 마스터 계정 hello 대상 사서함 소유자의 SID에 대 한 hello SID를 지정합니다. |
| DestMailboxOwnerSid | Hello CrossMailboxOperations 매개 변수는 True 하는 경우에 설정 합니다. Hello hello 대상 사서함의 SID를 지정합니다. |
| DestMailboxOwnerUPN | Hello CrossMailboxOperations 매개 변수는 True 하는 경우에 설정 합니다. Hello hello 대상 사서함의 hello 소유자의 UPN을 지정합니다. |
| DestFolder | hello 대상 폴더를 이동 하는 등의 작업에 대 한 합니다. |
| 폴더 | hello 항목 그룹에 있는 폴더입니다. |
| 폴더 |     작업;에 포함 된 hello 소스 폴더에 대 한 정보 예를 들어, 폴더를 선택 하 고 이후에 삭제 됩니다. |


### <a name="sharepoint-base"></a>Sharepoint 기본 속성
이러한 속성은 일반적인 tooall SharePoint 레코드입니다.

| 속성 | 설명 |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| EventSource | SharePoint에서 이벤트가 발생했음을 나타냅니다. 가능한 값은 SharePoint 또는 ObjectModel입니다. |
| ItemType | hello 형식 액세스 또는 수정 된 개체입니다. 참조 hello 유형의 개체에 대 한 자세한 내용은 hello ItemType 테이블입니다. |
| MachineDomainInfo | 장치 동기화 작업에 대한 정보입니다. 이 정보는 hello 요청에 있는 경우에 보고 됩니다. |
| MachineId |   장치 동기화 작업에 대한 정보입니다. 이 정보는 hello 요청에 있는 경우에 보고 됩니다. |
| Site_ | hello hello 파일 또는 폴더를 액세스 하 여 hello 사용자가 있는 hello 사이트의 GUID입니다. |
| Source_Name | hello 엔터티 hello를 발생 시킨 작업을 감사 합니다. 가능한 값은 SharePoint 또는 ObjectModel입니다. |
| UserAgent | Hello 사용자의 클라이언트 또는 브라우저에 대 한 정보입니다. 이 정보는 클라이언트 hello 또는 브라우저에서 제공 됩니다. |


### <a name="sharepoint-schema"></a>SharePoint 스키마
이러한 레코드는 구성을 변경 tooSharePoint 때 생성 됩니다.

| 속성 | 설명 |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| CustomEvent | 사용자 지정 이벤트에 대한 선택적 문자열입니다. |
| Event_Data |  사용자 지정 이벤트에 대한 선택적 페이로드입니다. |
| ModifiedProperties | hello 속성 사용자는 사이트 또는 사이트 모음 관리 그룹의 구성원으로 추가 하는 등의 관리 이벤트에 대 한 포함 됩니다. hello 속성에는 새 값의 hello 속성 (이러한 hello 추가 된 사용자는 사이트 관리자)를 수정 하 고 hello hello의 이전 값 개체를 수정 하는 hello (예: hello 사이트 관리자 그룹) 수정 된 hello 속성의 hello 이름을 포함 합니다. |


### <a name="sharepoint-file-operations"></a>SharePoint 파일 작업
이러한 레코드는 SharePoint에서 응답 toofile 작업에서 생성 됩니다.

| 속성 | 설명 |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePointFileOperation |
| DestinationFileExtension | hello 복사 되거나 이동 하는 파일의 파일 확장명입니다. 이 속성은 FileCopied 및 FileMoved 이벤트에 대해서만 표시됩니다. |
| DestinationFileName | hello 이름 복사 되거나 이동 된 hello 파일입니다. 이 속성은 FileCopied 및 FileMoved 이벤트에 대해서만 표시됩니다. |
| DestinationRelativeUrl | 파일을 복사 하거나 이동 hello 대상 폴더의 hello URL입니다. SiteURL, DestinationRelativeURL, 및 DestinationFileName 매개 변수에 대 한 hello 값의 hello 조합 hello 파일 복사에 대 한 전체 경로 이름을 hello hello ObjectID 속성에 대 한 hello 값과 같으며 hello 됩니다. 이 속성은 FileCopied 및 FileMoved 이벤트에 대해서만 표시됩니다. |
| SharingType | hello 형식으로 hello 리소스 공유 toohello 사용자를 할당 된 사용 권한을 공유입니다. 이 사용자는 hello UserSharedWith 매개 변수에 의해 식별 됩니다. |
| Site_Url | hello 파일 또는 폴더를 액세스 하 여 hello 사용자가 있는 hello 사이트의 hello URL입니다. |
| SourceFileExtension | hello hello 사용자가 액세스 하는 hello 파일의 파일 확장명입니다. 이 속성을 액세스 하는 hello 개체 폴더인 경우 비어 있습니다. |
| SourceFileName |  hello 파일 또는 폴더 hello 사용자가 액세스할의 hello 이름입니다. |
| SourceRelativeUrl | hello 사용자가 액세스 하는 hello 파일을 포함 하는 hello 폴더의 hello URL입니다. hello SiteURL, SourceRelativeURL, 및 SourceFileName 매개 변수에 대 한 hello 값의 hello 조합 hello 사용자가 액세스 하는 hello 파일에 대 한 전체 경로 이름을 hello hello ObjectID 속성에 대 한 hello 값과 같으며 hello 됩니다. |
| UserSharedWith |  hello 사용자와 공유 리소스입니다. |




## <a name="sample-log-searches"></a>샘플 로그 검색
다음 표에서 hello이이 솔루션에 의해 수집 된 레코드 업데이트에 대 한 예제 로그 검색을 제공 합니다.

| 쿼리 | 설명 |
| --- | --- |
|Office 365 구독에 대 한 모든 hello 작업의 수 |`Type = OfficeActivity | measure count() by Operation` |
|SharePoint 사이트 사용량|`Type=OfficeActivity OfficeWorkload=sharepoint | measure count() as Count by SiteUrl | sort Count asc`|
|사용자 유형별 파일 액세스 작업|`Type=OfficeActivity OfficeWorkload=sharepoint Operation=FileAccessed | measure count() by UserType`|
|특정 키워드를 사용한 검색|`Type=OfficeActivity OfficeWorkload=azureactivedirectory "MyTest"`|
|Exchange에서 외부 작업 모니터링|`Type=OfficeActivity OfficeWorkload=exchange ExternalAccess = true`|



## <a name="troubleshooting"></a>문제 해결

Office 365 솔루션은 예상 대로 데이터를 수집 하지, 경우에 hello OMS 포털에서 상태를 확인 하십시오. **설정** -> **연결 된 원본** -> **Office 365** . 다음 표에서 hello 각 상태를 설명 합니다.

| 가동 상태 | 설명 |
|:--|:--|
| Active | hello Office 365 구독이 활성 상태 이며 hello 작업은 성공적으로 연결 된 tooyour OMS 작업 영역. |
| Pending | hello Office 365 구독이 활성화 되어 있지만 아직 tooyour OMS 작업 영역을 성공적으로 연결 되지 않은 hello 작업. hello 처음으로 hello Office 365 구독을 연결할 hello 작업도 됩니다이 상태에서 성공적으로 연결 될 때까지 합니다. 모든 hello 작업 tooswitch tooActive 24 시간을 할애 하십시오. |
| 비활성 | hello Office 365 구독이 비활성 상태에서입니다. 자세한 내용은 Office 365 관리 페이지를 확인하세요. Office 365 구독을 활성화 한 후 OMS 작업 영역에서 연결을 해제 하 고 다시 연결 데이터를 받는 toostart 합니다. |



## <a name="next-steps"></a>다음 단계
* 로그 검색을 사용 하 여 [로그 분석](../log-analytics/log-analytics-log-searches.md) tooview 업데이트 데이터를 자세히 설명 합니다.
* [고유한 대시보드 만들기](../log-analytics/log-analytics-dashboards.md) toodisplay Office 365 검색 쿼리를 합니다.
* [경고를 만들](../log-analytics/log-analytics-alerts.md) toobe 중요 한 Office 365 활동의 사전 알림을 받습니다.  
