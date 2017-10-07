---
title: "Active Directory 감사 보고서 이벤트 aaaAzure | Microsoft Docs"
description: "Azure Active Directory에서 확인하고 다운로드할 수 있는 감사된 이벤트"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 307eedf7-05bc-448d-a84d-bead5a4c5770
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 4a84cce2be56bde006164abf10ad1e72ca6e99bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Azure Active Directory 감사 보고서 이벤트
*이 설명서는 hello의 일부 [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)합니다.*

Azure Active Directory 감사 보고서 hello 고객은 Azure Active Directory에 발생 한 특권이 필요한 작업을 식별할 수 있습니다. 특권이 필요한 작업 (예를 들어 역할 만들기 또는 암호 재설정) 상승 변경 내용을 포함 toodirectory 구성 변경 (예: 변경 내용 toodomain 페더레이션 설정) 또는 정책 구성 (예: 암호 정책)을 변경 합니다. hello 보고서 hello 변경 및 hello 날짜 및 시간 (UTC)에 영향을 받는 hello 대상 리소스 hello 동작을 수행한 hello 행위자 hello 이벤트 이름에 대 한 hello 감사 레코드를 제공 합니다. 고객은 hello 통해 자신의 Azure Active Directory에 대 한 감사 이벤트의 수 tooretrieve hello 목록을 [Azure 포털](https://portal.azure.com/)에 설명 된 대로 [감사 로그를 보려면](active-directory-reporting-azure-portal.md)합니다.

## <a name="list-of-audit-report-events"></a>감사 보고서 이벤트 목록
<!--- audit event descriptions should be in hello past tense --->

| 이벤트 | 이벤트 설명 |
| --- | --- |
| **사용자 이벤트** | |
| 사용자 추가 |사용자 toohello 디렉터리를 추가 합니다. |
| 사용자 삭제 |Hello 디렉터리에서 사용자를 삭제 합니다. |
| 라이선스 속성 설정 |Hello 디렉터리의 사용자에 대 한 hello 라이선스 속성을 설정 합니다. |
| 사용자 암호 재설정 |Hello 디렉터리의 사용자에 대 한 hello 암호 다시 설정 합니다. |
| 사용자 암호 변경 |Hello 디렉터리의 사용자에 대 한 hello 암호를 변경 합니다. |
| 사용자 라이선스 변경 |Hello 디렉터리의 tooa 사용자를 할당 하는 hello 라이선스를 변경 합니다. 어떤 라이선스에서 업데이트 된, 봐 hello toosee [사용자 업데이트](#update-user-attributes) 아래 속성 |
| 사용자 업데이트 |Hello 디렉터리의 사용자를 업데이트 합니다. [아래에서 참조](#update-user-attributes) 합니다. |
| 사용자 암호 강제 변경 설정 |로그인에 사용자 toochange를 강제로 실행 하는 hello 속성 자신의 암호를 설정 합니다. |
| 사용자 자격 증명 업데이트 |사용자 변경 된 hello 암호 |
| **그룹 이벤트** | |
| 그룹 추가 |Hello 디렉터리에는 그룹을 만들었습니다. |
| 그룹 업데이트 |Hello 디렉터리에 그룹을 업데이트 합니다. 그룹 속성을 알아 업데이트 된 toosee 너무 참조[그룹 속성 감사](#update-group-attributes) hello 섹션 아래에 |
| 그룹 삭제 |Hello 디렉터리에서 그룹을 삭제 합니다. |
| CreateGroupSettings |생성된 그룹 설정 |
| UpdateGroupSettings |그룹 설정을 업데이트했습니다. 어떤 그룹 설정이 업데이트 되었습니다 toosee 너무 참조[그룹 속성 감사](#update-group-attributes) hello 섹션 아래에 |
| DeleteGroupSettings |삭제된 그룹 설정 |
| SetGroupLicense |그룹 라이선스를 설정합니다. |
| SetGroupManagedBy |사용자가 관리 그룹 toobe 설정 |
| AddGroupMember |추가 된 멤버 toogroup |
| RemoveGroupMember |그룹에서 멤버 제거 |
| AddGroupOwner |추가 된 소유자 toogroup |
| RemoveGroupOwner |그룹에서 제거된 소유자 |
| **응용 프로그램 이벤트** | |
| 서비스 주체 추가 |서비스 보안 주체 toohello 디렉터리를 추가 합니다. |
| 서비스 주체 제거 |Hello 디렉터리에서 서비스 사용자를 제거 합니다. |
| 서비스 주체 자격 증명 추가 |추가 된 자격 증명 tooa 서비스 보안 주체입니다. |
| 서비스 주체 자격 증명 제거 |서비스 주체에서 자격 증명을 제거합니다. |
| 위임 항목 추가 |생성 된 [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) hello 디렉터리에 있습니다. |
| 위임 항목 설정 |업데이트는 [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) hello 디렉터리에 있습니다. |
| 위임 항목 제거 |삭제는 [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) hello 디렉터리에 있습니다. |
| **역할 이벤트** | |
| 역할 멤버 tooRole 추가 |사용자 tooa 디렉터리 역할을 추가 합니다. |
| 역할에서 역할 멤버 제거 |디렉터리 역할에서 사용자를 제거합니다. |
| AddRoleDefinition |역할 정의를 추가했습니다. |
| UpdateRoleDefinition |역할 정의를 업데이트했습니다. 역할 설정 업데이트 된 toosee 너무 참조[역할 정의 속성 감사](#update-role-definition-attributes) hello 섹션 아래에 |
| DeleteRoleDefinition |역할 정의를 삭제했습니다. |
| AddRoleAssignmentToRoleDefinition |역할 할당 toorole 정의 추가 합니다. |
| RemoveRoleAssignmentFromRoleDefinition |역할 정의에서 역할 할당을 제거했습니다. |
| AddRoleFromTemplate |템플릿에서 역할을 추가했습니다. |
| UpdateRole |역할을 업데이트했습니다. |
| AddRoleScopeMemberToRole |Toorole 범위가 지정 된 멤버를 추가 합니다. |
| RemoveRoleScopedMemberFromRole |역할에서 범위가 지정된 멤버를 제거했습니다. |
| **장치 이벤트(모든 새 이벤트)** | |
| AddDevice |장치를 추가했습니다. |
| UpdateDevice |장치를 업데이트했습니다. 장치 속성 업데이트 된 toosee 너무 참조[장치 속성 Audited](#update-device-attributes) hello 섹션 아래에 |
| DeleteDevice |장치를 삭제했습니다. |
| AddDeviceConfiguration |장치 구성을 추가했습니다. |
| UpdateDeviceConfiguration |장치 구성을 업데이트했습니다. 장치 구성 속성 업데이트 된 toosee 너무 참조[장치 구성 속성 Audited](#update-device-configuration-attributes) hello 섹션 아래에 |
| DeleteDeviceConfiguration |장치 구성을 삭제했습니다. |
| AddRegisteredOwner |등록 된 소유자 toodevice를 추가 됩니다. |
| AddRegisteredUsers |등록 된 사용자 toodevice를 추가 됩니다. |
| RemoveRegisteredOwner |장치에서 등록된 소유자를 제거합니다. |
| RemoveRegisteredUsers |장치에서 등록된 사용자를 제거합니다. |
| RemoveDeviceCredentials |장치 자격 증명을 제거합니다. |
| **B2B 이벤트** | |
| 배치 초대가 업로드되었습니다. |관리자 초대 toobe 전송 toopartner 사용자를 포함 하는 파일을 업로드 했습니다. |
| 배치 초대가 처리되었습니다. |초대 toopartner 사용자가 포함 된 파일을 처리 합니다. |
| 외부 사용자를 초대합니다. |외부 사용자는 초대 된 toohello 디렉터리 되었습니다. |
| 외부 사용자 초대를 충전합니다. |외부 사용자가 자신의 초대 toohello 디렉터리를 사용 합니다. |
| 외부 사용자 toogroup를 추가 합니다. |외부 사용자가 구성원 tooa 그룹 hello 디렉터리에 할당 되었습니다. |
| 외부 사용자 tooapplication를 할당 합니다. |외부 사용자가 직접 액세스 tooan 응용 프로그램을 할당 되었습니다. |
| 바이럴 테넌트 만들기입니다. |새 테 넌 트 hello 초대 상환 하 여 Azure AD에서 생성 되었습니다. |
| 바이럴 사용자 만들기입니다. |사용자는 기존 테 넌 트의 Azure ad에서로 만들어진 hello 초대 상환 합니다. |
| **관리 장치(모든 새 이벤트)** | |
| AddAdministrativeUnit |관리 장치를 추가합니다. |
| UpdateAdministrativeUnit |관리 장치를 업데이트합니다. 관리 단위 속성 업데이트 된 toosee 너무 참조[감사 관리 장치 속성](#update-administrative-unit-attributes) hello 섹션 아래에 |
| DeleteAdministrativeUnit |관리 장치를 삭제합니다. |
| AddMemberToAdministrativeUnit |멤버 tooadministrative 단위를 추가 합니다. |
| RemoveMemberFromAdministrativeUnit |관리 장치에서 멤버를 제거합니다. |
| **Directory 이벤트** | |
| 파트너 toocompany 추가 |파트너 toohello 디렉터리를 추가 합니다. |
| 회사에서 파트너 제거 |Hello 디렉터리에서 파트너를 제거 합니다. |
| DemotePartner |파트너를 강등합니다. |
| 도메인 toocompany 추가 |도메인 toohello 디렉터리를 추가 합니다. |
| 회사에서 도메인 제거 |Hello 디렉터리에서 도메인을 제거 합니다. |
| 도메인 업데이트 |Hello 디렉터리에 도메인을 업데이트 합니다. 도메인 속성을 알아 업데이트 된 toosee 너무 참조[감사는 도메인 속성](#update-domain-attributes) hello 섹션 아래에 |
| 도메인 인증 설정 |Hello 회사에 대 한 hello 기본 도메인 설정을 변경 했습니다. |
| 회사 연락처 정보 설정 |회사 수준 연락처 기본 설정을 지정합니다. 여기에는 Microsoft 온라인 서비스에 대한 기술 관련 알림 및 마케팅을 위한 메일 주소가 포함됩니다. |
| 도메인에 페더레이션 설정 지정 |도메인에 대 한 hello 페더레이션 설정을 업데이트 했습니다. |
| 도메인 확인 |Hello 디렉터리에 도메인을 확인 했습니다. |
| 메일로 확인된 도메인 확인 |전자 메일 확인을 사용 하 여 hello 디렉터리에 도메인을 확인 했습니다. |
| 회사에 DirSyncEnabled 플래그 설정 |Azure AD Sync에 대 한 디렉터리를 사용할 수 있는 hello 속성을 설정 합니다. |
| 암호 정책 설정 |사용자 암호의 길이 및 문자 제약 조건을 설정합니다. |
| 회사 정보 설정 |업데이트 된 hello 회사 수준 정보입니다. Hello 참조 [Get-msolcompanyinformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) 자세한 내용은 PowerShell cmdlet. |
| SetCompanyAllowedDataLocation |회사에 허용된 데이터 위치를 설정합니다. |
| SetCompanyDirSyncEnabled |DirSyncEnabled 플래그를 설정합니다. |
| SetCompanyDirSyncFeature |DirSync 기능을 설정합니다. |
| SetCompanyInformation |회사 정보를 설정합니다. |
| SetCompanyMultiNationalEnabled |회사에 다국적 기능 활성화를 설정합니다. |
| SetDirectoryFeatureOnTenant |테넌트에 디렉터리 기능을 설정합니다. |
| SetTenantLicenseProperties |테넌트 라이선스 속성을 설정합니다. |
| CreateCompanySettings |회사 설정 만들기 |
| UpdateCompanySettings |회사 설정을 업데이트합니다. 회사 속성 업데이트 된 toosee 너무 참조[감사 회사 속성](#update-company-attributes) hello 섹션 아래에 |
| DeleteCompanySettings |회사 설정 삭제 |
| SetAccidentalDeletionThreshold |실수로 인한 삭제 임계값을 설정합니다. |
| SetRightsManagementProperties |권한 관리 속성을 설정합니다. |
| PurgeRightsManagementProperties |권한 관리 속성을 제거합니다. |
| UpdateExternalSecrets |외부 암호 업데이트 |
| **정책 이벤트(모든 새 이벤트)** | |
| AddPolicy |정책을 추가합니다. |
| UpdatePolicy |정책을 업데이트합니다. |
| DeletePolicy |정책을 삭제합니다. |
| AddDefaultPolicyApplication |정책 tooapplication를 추가 합니다. |
| AddDefaultPolicyServicePrincipal |정책 tooservice 보안 주체를 추가 합니다. |
| RemoveDefaultPolicyApplication |응용 프로그램에서 정책을 제거합니다. |
| RemoveDefaultPolicyServicePrincipal |서비스 주체에서 정책을 제거합니다. |
| RemovePolicyCredentials |정책 자격 증명을 제거합니다. |

## <a name="audit-report-retention"></a>감사 보고서 보존

Hello 보존에 대 한 최신 정보를 참조 하십시오. [Azure Active Directory 보고서 보존 정책](active-directory-reporting-retention.md)합니다.


더 긴 보존 기간에 대 한 감사 이벤트를 저장 관심이 있는 고객, hello Reporting API 가능 사용된 tooregularly 끌어오기를 별도 데이터 저장소로 이벤트를 감사 합니다. 참조 [Reporting API hello 시작](active-directory-reporting-api-getting-started.md) 대 한 자세한 내용은 합니다.

## <a name="properties-included-with-each-audit-event"></a>각 감사 이벤트에 포함된 속성
| 속성 | 설명 |
| --- | --- |
| 날짜 및 시간 |발생 한 감사 이벤트 hello hello 날짜 및 시간 |
| 행위자 |hello 사용자 또는 hello 작업을 수행 하는 서비스 사용자 |
| 동작 |hello 수행한 작업을 |
| 대상 |hello 사용자 또는 서비스 사용자는 hello 작업이 수행 |

## <a name="update-user-attributes"></a>"업데이트 사용자" 특성
사용자 hello"업데이트" 감사 이벤트는 업데이트 된 사용자 특성에 대 한 추가 정보를 포함 합니다. 각 특성에 대 한 이전 값을 hello 둘 다 및 hello 새 값이 포함 되어 있습니다.

| 특성 | 설명 |
| --- | --- |
| AccountEnabled |hello 사용자가 로그인 할 수 있습니다. |
| AssignedLicense |Toohello 사용자 지정 된 모든 라이선스입니다. |
| AssignedPlan |Hello 라이선스에서 발생 하는 서비스 계획 toohello 사용자를 할당 합니다. |
| LicenseAssignmentDetail |라이선스에 대 한 내용은 toohello 사용자를 할당 합니다. 예를 들어, 그룹 기반 라이선스 있어서 여기 라이선스를 부여 hello hello 그룹을 포함 됩니다. |
| 모바일 |hello 사용자의 휴대폰 합니다. |
| OtherMail |사용자의 대체 전자 메일 주소를 hello 합니다. |
| OtherMobile |사용자의 대체 휴대폰 hello 합니다. |
| StrongAuthenticationMethod |목록 확인 방법 모바일 앱에서 음성 통화, SMS 또는 확인 코드와 같이 hello 사용자가 Multi-factor Authentication에 대 한 구성입니다. |
| StrongAuthenticationRequirement |이 사용자에 대한 Multi-Factor Authentication의 강제 적용, 사용 또는 사용 안 함의 여부입니다. |
| StrongAuthenticationUserDetails |Multi-factor Authentication에 사용 되는 주소 및 암호 재설정 확인 hello 사용자의 전화 번호, 대체 전화 번호 및 전자 메일. |
| StrongAuthenticationPhoneAppDetail |세부 정보 forof 전화 앱 tooperform 2FA 로그인 등록 |
| TelephoneNumber |hello 사용자의 전화 번호입니다. |
| AlternativeSecurityId |Hello 개체에 대 한 대체 보안 ID입니다. |
| CreationType |생성 방법 (초대 하 여 또는 바이러스에 감염) hello 사용자입니다. |
| InviteTicket |Hello 사용자에 대 한 초대 티켓의 목록입니다. |
| InviteReplyUrl |초대 수락 시 tooreply url의 목록입니다. |
| InviteResources |리소스 toowhich hello 사용자 목록은 초대 되었습니다. |
| LastDirSyncTime |마지막으로 hello 개체가 업데이트 된 hello 신뢰할 수 있는 (사용자 고객 온-프레미스)에서 동기화로 인해 디렉터리입니다. |
| MSExchRemoteRecipientType |받는 사람 tooMSO 형식을 매핑합니다. 너무 참조 [MSO 받는 사람 유형] https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx 받는 사람 형식에 대 한 |
| PreferredDataLocation |hello 사용자, 그룹, 연락처의 공용 폴더의 기본 위치 또는 장치의 데이터 hello 합니다. |
| ProxyAddresses |hello 주소 외부 메일 시스템에서 인식 하는 Exchange Server 받는 사람 개체입니다. |
| StsRefreshTokensValidFrom |새로 고침 토큰 해지 정보를 전달합니다. 이 시간 전에 발급된 STS 새로 고침 토큰은 만료된 것으로 간주됩니다. |
| UserPrincipalName |hello UPN은 사용자에 대 한 인터넷 스타일 로그온 이름입니다. |
| UserState |사용자 PendingApproval/PendingAcceptance/Accepted/PendingVerification의 상태입니다. |
| UserStateChangedOn |마지막 변경 tooUserState의 타임 스탬프입니다. Tootrigger 수명 주기 워크플로 사용 했습니다. |
| UserType |사용자의 유형입니다. 멤버(0), 게스트(1), 바이럴(2)입니다. |

## <a name="update-group-attributes"></a>"그룹 업데이트" 특성
| 특성 | 설명 |
| --- | --- |
| 분류 |통합 그룹 (HBI, MBI 등)에 대 한 hello 분류 합니다. |
| 설명 |Hello 개체에 대 한 설명이 포함 된 구를 사람이 읽을 수 있습니다. |
| displayName |개체에 대 한 hello 표시 이름 |
| DirSyncEnabled |동기화가 권한이 있는 (고객, 온-프레미스) 디렉터리에서 발생하는지 여부를 나타냅니다. |
| GroupLicenseAssignment |그룹의 라이선스 할당 |
| GroupType |그룹 유형, 통합(0) |
| IsMembershipRuleLocked |해당 hello MembershipRule 속성 hello 셀프 서비스 그룹 관리 서비스에 의해 설정 되 고 사용자가 변경할 수 없는 나타냅니다. 적용 가능한 유일한 toogroups GroupType GroupType.DynamicMembership를 포함 하는 위치 |
| IsPublic |Hello 그룹이 공개/개인 이면 tooindicate를 플래그입니다. |
| LastDirSyncTime |마지막으로 hello 개체가 업데이트 된 hello 신뢰할 수 있는 (고객, 온-프레미스)에서 동기화의 결과 디렉터리입니다. |
| Mail |기본 전자 메일 주소 |
| MailEnabled |이 그룹에 전자 메일 기능이 있는지 여부를 나타냅니다. |
| MailNickname |주소록 개체에 대 한 모니커, 일반적으로 전자 메일 이름 앞에 hello hello 부분 "@" 기호입니다. |
| MembershipRule |Hello 셀프 서비스 그룹 관리 서비스 toodetermine 멤버 toothis 그룹에 속해야 합니다.에서 사용 하는 hello 조건을 표현 하는 문자열입니다. IsMembershipRuleLocked도 참조하세요. 적용 가능한만 toogroups GroupType GroupType.DynamicMembership에 포함 되어 있습니다. |
| MembershipRuleProcessingState |이 그룹에 대 한 처리 하는 구성원의 hello 상태를 정의 하는 hello 셀프 서비스 그룹 관리 서비스에 의해 정의 되는 열거형 값입니다. 적용 가능한만 toogroups GroupType GroupType.DynamicMembership에 포함 되어 있습니다. |
| ProxyAddresses |hello 주소 외부 메일 시스템에서 인식 하는 Exchange Server 받는 사람 개체입니다. |
| RenewedDateTime |그룹이 가장 최근에 갱신된 때의 타임스탬프 레코드입니다. |
| SecurityEnabled |Hello 그룹의 멤버 자격 권한 부여 결정 영향을 줄 수 있는지 여부를 나타냅니다. |
| WellKnownObject |미리 정의된 집합 중 하나로 지정하여 디렉터리 개체를 표시합니다. |

## <a name="update-device-attributes"></a>"장치 업데이트" 특성
| 특성 | 설명 |
| --- | --- |
| AccountEnabled |보안 주체가 인증할 수 있는지 여부를 나타냅니다. |
| CloudAccountEnabled |보안 주체가 인증할 수 있는지 여부를 나타냅니다. InTune을 통해 작성 된 hello 장치는 온-프레미스에서 마스터 됩니다. |
| CloudDeviceOSType |Hello 예: Windows RT, iOS 운영 체제에 따라 hello 장치의 형식입니다. 클라우드 서비스 (예: Intune)으로 설정 된 경우이 특성은 hello 디렉터리에서 DeviceOSType에 대 한 합니다. |
| CloudDeviceOSVersion |Hello OS의 버전입니다. 클라우드 서비스 (예: Intune)으로 설정 된 경우이 특성은 hello 디렉터리에서 DeviceOSVersion에 대 한 합니다. |
| CloudDisplayName |Hello displayName LDAP 특성 값입니다. 클라우드 서비스 (예: Intune)으로 설정 된 경우이 특성 displayName hello 디렉터리에서 권한을 얻게 됩니다. |
| CloudCreated |Hello 개체가 클라우드 서비스에서 생성 되었는지 여부를 나타냅니다. |
| CompliantUntil |어떤 시간까지 장치가 규정 준수로 간주됩니다. |
| DeviceMetadata |Hello 장치에 대 한 사용자 지정 메타 데이터 |
| DeviceObjectVersion |이 특성은 hello 장치의 사용 되는 tooidentify hello 스키마 버전입니다. |
| DeviceOSType |Hello 예: Windows RT, iOS 운영 체제에 따라 hello 장치의 형식입니다. 기록한 hello 등록 서비스 및 의도 한 toobe에 의해 업데이트 hello MDM 관리 서비스 또는 STS 연한 관리 서비스입니다. |
| DeviceOSVersion |Hello OS의 버전입니다. 기록한 hello 등록 서비스 및 의도 한 toobe에 의해 업데이트 hello MDM 관리 서비스 또는 STS 연한 관리 서비스입니다. |
| DevicePhysicalIds |다중값된 특성 toostore 식별자 hello 물리적 장치를 위한 것입니다. BIOS ID, TPM 지문, 하드웨어 특정 ID 등을 포함할 수 있습니다. |
| DirSyncEnabled |동기화가 권한이 있는 (고객, 온-프레미스) 디렉터리에서 발생하는지 여부를 나타냅니다. |
| displayName |개체에 대 한 hello 표시 이름 |
| IsCompliant |이 특성은 사용 되는 toomanage hello 장치의 hello 모바일 장치 관리 상태입니다. |
| IsManaged |이 특성은 사용 tooindicate hello 장치를 관리 하는 클라우드에서 mdm. |
| LastDirSyncTime |마지막으로 hello 개체가 업데이트 된 hello 신뢰할 수 있는 (고객, 온-프레미스)에서 동기화로 인해 디렉터리입니다. |

## <a name="update-device-configuration-attributes"></a>"장치 구성 업데이트" 특성
| 특성 | 설명 |
| --- | --- |
| MaximumRegistrationInactivityPeriod |hello 최대 일 수는 장치 수 전에 비활성 상태로 유지 해결을 위한 것으로 간주 됩니다. |
| RegistrationQuota |정책을은 toolimit hello 수가 단일 사용자에 허용 되는 장치 등록을 사용 합니다. |

## <a name="update-service-principal-configuration-attributes"></a>"서비스 주체 구성 업데이트" 특성
| 특성 | 설명 |
| --- | --- |
| AccountEnabled |보안 주체가 인증할 수 있는지 여부를 나타냅니다. |
| AppPrincipalId |보안 주체에 대한 외부, 응용 프로그램 정의 ID입니다. |
| displayName |개체에 대 한 hello 표시 이름 |
| ServicePrincipalName |"이름/기관이"를 여기서 이름 응용 프로그램 클래스 값을 지정 하 고 기관 이상 포함 되어 있는 서비스 사용자 이름, 호스트 이름 [: 포트] 또는 "name" hello 서비스 사용자에 대 한 식별자를 지정 하는 합니다. |

## <a name="update-app-attributes"></a>"앱 업데이트" 특성
| 특성 | 설명 |
| --- | --- |
| AppAddress |hello 집합이 tooa 서비스 사용자를 할당 된 주소 (Url 리디렉션). |
| AppId |Hello 응용 프로그램의 응용 프로그램 ID |
| AppIdentifierUri |Hello 응용 프로그램을 식별 하는 응용 프로그램 URI입니다.  이 일반적으로 hello 응용 프로그램 액세스 URL입니다. |
| AppLogoUrl |CDN에 저장 된 hello 응용 프로그램 로고 이미지에 대 한 hello url입니다. |
| AvailableToOtherTenants |True 이면 hello 응용 프로그램은 다중 테 넌 트 응용 프로그램 (즉, 사용 가능 하 여 다른 테 넌 트)입니다. |
| displayName |응용 프로그램 이름에 대 한 hello 표시 이름 |
| Entitlement |응용 프로그램 권한 부여의 목록입니다. |
| ExternalUserAccountDelegationsAllowed |리소스 응용 프로그램이 신뢰할 수 있는 것인지 여부와 외부 사용자 계정에 대한 위임 항목을 만들 수 있는지 여부를 나타내는 플래그입니다. |
| GroupMembershipClaims |hello 그룹 구성원 자격 클레임 정책입니다. |
| PublicClient |Hello 클라이언트 비밀 유지할 수 없는 경우 (즉, oauth 2.0에 기밀 클라이언트) |
| RecordConsentConditions |유형의 조건이 동의 hello에 정의 된 대로 계약 조건: 없음 (0) SilentConsentForPartnerManagedApp(1) 합니다. 이 값은 hello Graph API 스키마에 표시 되며 테 넌 트 관리자 설정/변경할 수만 있습니다. |
| RequiredResourceAccess |Hello RequiredResourceAccess 속성의 값의 XML 콘텐츠입니다. |
| WebApp |True인 경우 이 응용 프로그램이 웹앱임을 나타냅니다. |
| WwwHomepage |hello 기본 웹 페이지입니다. |

## <a name="update-role-attributes"></a>"역할 업데이트" 특성
| 특성 | 설명 |
| --- | --- |
| AppAddress |hello 집합이 tooa 서비스 사용자를 할당 된 주소 (Url 리디렉션). |
| BelongsToFirstLoginObjectSet |True 인 경우,이 개체가 toohello 집합이 새 테 넌 트의 첫 번째 admin 님 안녕하세요의 필요한 tooenable 로그인 개체에 속해 있음을 나타냅니다. |
| Builtin |개체의 수명을 hello hello 시스템에 의해 소유 하는지 여부를 나타냅니다. |
| 설명 |Hello 개체에 대 한 설명이 포함 된 구를 사람이 읽을 수 있습니다. |
| displayName |개체에 대 한 hello 표시 이름 |
| MailNickname |주소록 개체에 대 한 모니커, 일반적으로 전자 메일 이름 앞에 hello hello 부분 "@" 기호입니다. |
| RoleDisabled |액세스 검사의 목적을 위해 hello 역할을 무시할지 여부를 나타냅니다. |
| RoleTemplateId |Hello 역할 템플릿의 id입니다. |
| ServiceInfo |서비스 관련 MOAC 및/또는 다른 서비스 인스턴스는 사용할 수 있는 정보를 프로 비전 (hello 같거나 다른 데이터 집합의 서비스 형식). |
| TaskSetScopeReference |Role 또는 RoleTemplate과 연결된 TaskSet 및 Scope의 집합을 식별합니다. |
| ValidationError |Hello 속성이 나 개체 관리자 작업 tooresolve에서 링크에 대 한 일시적이 지 않은, 서비스 관련 오류를 설명 하는 페더레이션된 서비스에서 게시 정보입니다. |
| WellKnownObject |미리 정의된 집합 중 하나로 지정하여 디렉터리 개체를 표시합니다. |

## <a name="update-role-definition-attributes"></a>"역할 정의 업데이트" 특성
| 특성 | 설명 |
| --- | --- |
| AssignableScopes |이 RoleDefinition tooa 보안 사용자를 할당할 때 참조할 수 있는 권한 부여 범위의 컬렉션입니다. |
| displayName |개체에 대 한 hello 표시 이름 |
| GrantedPermissions |이 RoleDefinition에 의해 부여된 권한입니다. |

## <a name="update-administrative-unit-attributes"></a>“관리 장치 업데이트” 특성
| 특성 | 설명 |
| --- | --- |
| 설명 |이 속성은 관리 단위에 대 한 hello 설명을 변경 하는 경우 업데이트 됩니다. |
| displayName |이 속성은 관리 단위의 hello 이름을 변경할 때 업데이트 됩니다. |

## <a name="update-company-attributes"></a>"회사 업데이트" 특성
| 특성 | 설명 |
| --- | --- |
| AllowedDataLocation |회사의 사용자는 hello에 사용자를 프로 비전 toobe 수 위치입니다. |
| AuthorizedServiceInstance |서비스 인스턴스 toowhich 계획의 이름은 배포할 수 있습니다. |
| DirSyncEnabled |동기화가 권한이 있는 (고객, 온-프레미스) 디렉터리에서 발생하는지 여부를 나타냅니다. |
| DirSyncStatus |이 테 넌 트 컨텍스트에서 주소 주소록 개체의 동기화는 신뢰할 수 있는 (고객, 온-프레미스)에서 발생 하는지 여부를 나타냅니다. directory; hello 회사 개체에 대 한 DirSyncEnabled 속성에 대 한 확장입니다. |
| DirSyncFeatures |Hello 테 넌 트에 대 한 사용 가능한 상태 이며 사용할 수 없는 디렉터리 동기화 기능 집합의 비트 플래그 tookeep 추적 합니다. |
| DirectoryFeatures |활성화/비활성화 디렉터리 기능입니다. |
| DirSyncConfiguration |모든 디렉터리 동기화 구성 특정 toohello 현재 테 넌 트를 포함합니다. |
| displayName |개체에 대 한 hello 표시 이름 |
| IsMnc |부울 플래그 집합 너무 "true"입니다. hello 회사 hello 다국적 기업의 기능에 대해 활성화 됩니다. |
| ObjectSettings |Hello 개체의 적용 가능한 toohello 범위 설정의 컬렉션입니다. |
| PartnerCommerceUrl |URL toohello 파트너의 상거래 사이트입니다. |
| PartnerHelpUrl |URL toohello 파트너의 도움말 사이트입니다. |
| PartnerSupportEmail |URL toohello 파트너의 지원 전자 메일입니다. |
| PartnerSupportTelephone |URL toohello 파트너의 지원 전화 합니다. |
| PartnerSupportUrl |URL toohello 파트너의 지원 사이트입니다. |
| StrongAuthenticationDetails |TooStrongAuthentication 관련 세부 정보입니다. |
| StrongAuthenticationPolicy |Hello 회사에 대 한 강력한 인증 정책입니다. |
| TechnicalNotificationMail |전자 메일 주소 toonotify 기술 문제 tooa 회사와 관련 됩니다. |
| TelephoneNumber |Hello ITU 권장 E.123 준수 하는 전화 번호입니다. |
| TenantType |테 넌 트의 hello 유형입니다. 이 값을 지정 하지 않으면 테 넌 트 hello는 회사입니다. 그렇지 않은 경우 가능한 값은 MicrosoftSupport (0), SyndicatePartner (1), BreadthPartner (2) BreadthPartnerDelegatedAdmin (3) ResellerPartnerDelegatedAdmin (4) ValueAddedResellerPartnerDelegatedAdmin (5)입니다. |
| VerifiedDomain |DNS 도메인 이름 집합을 바인딩된 tooa 회사입니다. |

## <a name="update-domain-attributes"></a>"도메인 업데이트" 특성
| 특성 | 설명 |
| --- | --- |
| 기능 |있는 경우에 비트 플래그 hello 도메인의 hello 기능을 설명 합니다. |
| 기본값 |Hello 도메인 hello 기본값; 인지를 나타냅니다. 예를 들어 hello 기본 UserPrincipalName 접미사 MOAC에 새 사용자를 만들 때. |
| Initial |OCP 하 여 할당 된 hello 도메인 hello hello 회사에 대 한 초기 도메인 인지를 나타냅니다. hello 초기 도메인은 Microsoft Online 도메인;의 고유 하위 도메인 e.g.contoso3.microsoftonline.com 합니다. |
| LiveType |Hello 해당 Windows Live 네임 스페이스에 있는 경우의 형식입니다. |
| 이름 |Hello 끝점에 대 한 식별자입니다. |
| PasswordNotificationWindowDays |암호 만료 hello 사용자 일 전에 수가 hello 알림이 전송 됩니다. |
| PasswordValidityPeriodDays |암호를 변경 해야 할 전에 적합 일 hello 수입니다. |

감사 레코드는 많은 규정 준수 규칙의 필수 컨트롤입니다. 준수 규정 hello Azure Active Directory 감사 보고서 toomeet를 사용 하 여 고객에 대 한 것이 좋습니다 해당 hello 고객 제출 hello 고객의 hello 복사본과 함께이 도움말 항목의 복사본을 내보낸 toohelp hello 보고서에 설명 하는 감사 보고서 세부 정보입니다. Hello 감사자 toounderstand hello 규정 준수 규칙에 맞는 Azure 현재 싶으면, 직접 hello 감사자 toohello [준수 페이지](https://azure.microsoft.com/support/trust-center/compliance/) hello Microsoft Azure 보안 센터의 합니다.

