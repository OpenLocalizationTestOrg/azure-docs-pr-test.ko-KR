---
title: "aaaAzure Active Directory Connect Health 작업"
description: "이 문서에서는 Azure AD Connect Health를 배포한 후 수행할 수 있는 추가 작업에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a>Azure Active Directory Connect Health 작업
이 항목에서는 hello 설명 다양 한 작업 (Azure AD) Azure Active Directory Connect Health를 사용 하 여 수행할 수 있습니다.

## <a name="enable-email-notifications"></a>메일 알림 사용
경고 id 인프라 정상 인지를 나타낼 때 hello Azure AD Connect Health 서비스 toosend 전자 메일 알림을 구성할 수 있습니다. 이 작업은 경고가 생성된 경우 및 해결된 경우에 수행됩니다.

![Azure AD Connect Health 메일 알림 설정 스크린샷](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> 메일 알림은 기본적으로 사용됩니다.
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a>tooenable Azure AD Connect Health 전자 메일 알림
1. 열기 hello **경고** 블레이드 tooreceive 전자 메일 알림을 사용 하도록 원하는 hello 서비스에 대 한 합니다.
2. Hello 작업 모음에서 클릭 **알림 설정**합니다.
3. Hello 전자 메일 알림 스위치에서 선택 **ON**합니다.
4. 모든 전역 관리자 tooreceive 전자 메일 알림을 hello 확인란을 선택 합니다.
5. 다른 전자 메일 주소에서 전자 메일 알림을 tooreceive 원한다 면 hello에 지정 **추가 전자 메일 받는 사람** 상자입니다. 이 목록에서 전자 메일 주소 tooremove hello 항목을 마우스 오른쪽 단추로 클릭 하 고 선택 **삭제**합니다.
6. toofinalize hello 변경을 클릭 **저장**합니다. 변경 내용은 저장한 후에만 적용됩니다.

## <a name="delete-a-server-or-service-instance"></a>서버 또는 서비스 인스턴스 삭제

어떤 경우에는 서버에서 모니터링 되 고 tooremove를 할 수 있습니다. 여기에 사용자의 할 tooknow tooremove hello Azure AD Connect Health 서비스에서 서버입니다.

서버를 삭제 하는 경우 hello 다음 고려해 야 합니다.

* 이 작업을 수행하면 해당 서버에서 추가 데이터 수집이 중지됩니다. 이 서버는 모니터링 서비스는 hello에서 제거 됩니다. 이 작업 후 없는 수 tooview 새 경고, 모니터링 또는이 서버에 대 한 사용 현황 분석 데이터입니다.
* 이 작업은 서버에서 Health Agent hello를 제거 하지 않습니다. 이 단계를 수행 하기 전에 hello Health Agent를 제거 하지 않은 오류 관련된 toohello Health Agent hello 서버에서 볼 수 있습니다.
* 이 작업에는 이미이 서버에서 수집 하는 hello 데이터 삭제 되지 않습니다. Hello Azure 데이터 보존 정책에 따라 해당 데이터를 삭제 합니다.
* 이 작업을 수행한 후 원하는 경우 toostart 모니터링 hello 동일한 서버 제거 하 고이 서버에서 Health Agent hello를 다시 설치 해야 듯이 합니다.

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a>toodelete hello Azure AD Connect Health 서비스에서 서버
AD FS(Active Directory Federation Services)용 Azure AD Connect Health 및 Azure AD Connect(동기화):

1. 열기 hello **서버** hello에서 블레이드 **서버 목록** 블레이드 hello 서버 이름 toobe를 선택 하 여 제거 합니다.
2. Hello에 **서버** 블레이드 hello 작업 모음에서 클릭 **삭제**합니다.
3. Hello 확인 상자에 hello 서버 이름을 입력 하 여 확인 합니다.
4. **삭제**를 클릭합니다.

Azure Active Directory Domain Services용 Azure AD Connect Health:

1. 열기 hello **도메인 컨트롤러** 대시보드 합니다.
2. 도메인 컨트롤러 toobe 선택 hello 제거 합니다.
3. Hello 작업 모음에서 클릭 **삭제 선택**합니다.
4. Hello 동작 toodelete hello 서버를 확인 합니다.
5. **삭제**를 클릭합니다.

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a>Azure AD Connect Health 서비스에서 서비스 인스턴스 삭제
경우에 따라 tooremove 서비스 인스턴스를 할 수 있습니다. 작업 필요 tooknow tooremove 서비스 인스턴스 hello Azure AD Connect Health 서비스에서 다음과 같습니다.

서비스 인스턴스를 삭제 하는 경우 hello 다음 고려해 야 합니다.

* 이 작업에서 서비스를 모니터링 하는 hello hello 현재 서비스 인스턴스를 제거 합니다.
* 이 작업을 제거 하거나이 서비스 인스턴스의 일부로 모니터링 않은 hello 서버 중 하나에서 hello Health Agent를 제거 하지 않습니다. 이 단계를 수행 하기 전에 hello Health Agent를 제거 하지 않은 오류 관련된 toohello Health Agent hello 서버에서 볼 수 있습니다.
* 이 서비스 인스턴스의 모든 데이터는 hello Azure 데이터 보존 정책에 따라 삭제 됩니다.
* 이 작업을 수행한 후 toostart hello 서비스를 모니터링 하려는 경우 제거 하 고 모든 hello 서버에서 Health Agent hello를 다시 설치 합니다. 이 작업을 수행한 후 toostart hello 동일한 서버를 다시 제거, 다시 설치 및 등록을 모니터링 하려는 경우 해당 서버에서 Health Agent hello 합니다.

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a>toodelete hello Azure AD Connect Health 서비스에서 서비스 인스턴스
1. 열기 hello **서비스** hello에서 블레이드 **서비스 목록** 블레이드 tooremove 원하는 hello 서비스 id (팜 이름)을 선택 하 여 합니다.
2. Hello에 **서버** 블레이드 hello 작업 모음에서 클릭 **삭제**합니다.
3. Hello 확인 상자에서 hello 서비스 이름을 입력 하 여 확인 (예: sts.contoso.com).
4. **삭제**를 클릭합니다.
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a>역할 기반 액세스 제어로 액세스 관리
[역할 기반 액세스 제어 (RBAC)](../role-based-access-control-configure.md) Azure AD Connect Health 액세스 toousers 및 전역 관리자가 아닌 다른 그룹을 제공 합니다. RBAC 역할 toohello 의도 한 사용자 및 그룹을 할당 하 고 hello toolimit 디렉터리 내에서 전역 관리자는 메커니즘을 제공 합니다.

### <a name="roles"></a>역할
Azure AD Connect Health hello 다음 기본 제공 역할을 지원 합니다.

| 역할 | 권한 |
| --- | --- |
| 소유자 |소유자 수 *액세스 관리* (예를 들어 역할 tooa 사용자 또는 그룹)를 할당 *모든 정보를 볼* (예를 들어 경고 보기) hello 포털에서 및 *설정을 변경* 드 ( 예를 들어 전자 메일 알림을) Azure AD Connect Health 내에서. <br>기본적으로 Azure AD 전역 관리자에게 이 역할이 할당되며, 이 설정은 변경할 수 없습니다. |
| 참여자 |참가자 수 *모든 정보를 볼* (예를 들어 경고 보기) hello 포털에서 및 *설정을 변경* (예를 들어 전자 메일 알림을) Azure AD Connect Health 내에서. |
| 읽기 권한자 |판독기 수 *모든 정보를 볼* (예를 들어 경고 보기)에서 Azure AD Connect Health 포털 hello에서에서 합니다. |

Hello 역할 hello 포털 환경에서 사용할 수 있는 경우에 Azure AD Connect Health를 내 없습니다 영향 tooaccess 있어야 하는 다른 역할 (예: 사용자 액세스 관리자가 또는 DevTest Labs 사용자).

### <a name="access-scope"></a>액세스 범위
Azure AD Connect Health는 다음 두 수준에서 액세스 관리를 지원합니다.

* **모든 서비스 인스턴스**:이 hello 대부분의 경우에서 경로 권장 합니다. Azure AD Connect Health에서 모니터링되는 모든 역할 유형에서 모든 서비스 인스턴스(예: AD FS 팜)에 대한 액세스를 제어합니다.
* **서비스 인스턴스**: 일부 경우에 따라 역할 유형 또는 서비스 인스턴스에 의해 toosegregate 액세스 해야 합니다. 이 경우 hello 서비스 인스턴스 수준에서 액세스를 관리할 수 있습니다.  

최종 사용자가 hello 디렉터리 또는 서비스에 액세스할 권한이 부여 되었는지 인스턴스 수준입니다.

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a>허용 사용자 또는 그룹 액세스 tooAzure AD Connect Health
hello 다음 단계에서는 tooallow 액세스 하는 방법
#### <a name="step-1-select-hello-appropriate-access-scope"></a>1 단계: hello 적절 한 액세스 범위를 선택 합니다.
hello에 대 한 사용자 액세스 tooallow *모든 서비스 인스턴스* Azure AD Connect Health를 Azure AD Connect Health에 주 블레이드를 열고 hello 내의 수준입니다.<br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a>2단계: 사용자 및 그룹 추가, 역할 할당
1. Hello에서 **구성** 섹션에서 클릭 **사용자**합니다.<br>
   ![사용자가 강조 표시된 Azure AD Connect Health RBAC 주 블레이드 스크린샷](./media/active-directory-aadconnect-health/RBAC_main_blade.png)
2. **추가**를 선택합니다.
3. Hello에 **역할 선택** 창 역할을 선택 합니다 (예를 들어 **소유자**).<br>
   ![Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_add.png)
4. Hello 이름 또는 대상으로 하는 hello 사용자 또는 그룹의 식별자를 입력 합니다. 하나 이상의 사용자 또는 그룹이 hello에서 선택할 수 있습니다 동시 합니다. **선택**을 클릭합니다.
   ![Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_select_users.png)
5. **확인**을 선택합니다.<br>
6. Hello 역할 할당이 완료 되 면 hello 사용자 및 그룹 hello 목록에 나타납니다.<br>
   ![새 사용자가 강조 표시된 Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_user_list.png)

Hello 사용자가 나열 하는 이제 하 고 액세스할 수 있는 그룹, tootheir 할당 된 역할에 따라 키를 누릅니다.

> [!NOTE]
> * 전역 관리자가 전체 액세스 tooall hello 작업 같으면 주도 전역 관리자 계정을 hello 목록 앞에 존재 하지 않는 있습니다.
> * hello 사용자 초대 기능은 Azure AD Connect Health 내에서 지원 되지 않습니다.
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a>사용자 또는 그룹을 사용 하 여 3 단계: 공유 hello 블레이드 위치
1. 사용 권한을 할당하면 사용자가 [여기](http://aka.ms/aadconnecthealth)로 이동하여 Azure AD Connect Health에 액세스할 수 있습니다.
2. Hello 블레이드에서 hello 사용자 hello 블레이드 또는 여러 부분을, toohello 대시보드를 고정할 수 있습니다. Hello를 클릭 하기만 하면 **Pin toodashboard** 아이콘입니다.<br>
   ![고정 아이콘이 강조 표시된 Azure AD Connect Health RBAC 고정 블레이드 스크린샷](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)

> [!NOTE]
> Hello 판독기 역할 할당의 사용자에 hello Azure Marketplace에서에서 수 tooget Azure AD Connect Health 확장명이 아닙니다. hello 사용자 hello 필요한 "만들기" 작업 toodo을 지금 수행할 수 없습니다. hello 사용자 이동 toohello 앞에 링크 하 여 toohello 블레이드에서 가져올 수 있습니다. 후속 사용에 대 한 hello 사용자 hello 블레이드 toohello 대시보드를 고정할 수 있습니다.
>
>

### <a name="remove-users-or-groups"></a>사용자 또는 그룹 제거
사용자 또는 그룹 추가 제거할 수 있습니다 tooAzure AD 상태 RBAC 연결 합니다. 단순히 hello 사용자 또는 그룹을 마우스 오른쪽 단추로 클릭 하 고 선택 **제거**합니다.<br>
![제거가 강조 표시된 Azure AD Connect Health RBAC 사용자 창 스크린샷](./media/active-directory-aadconnect-health/RBAC_remove.png)

[//]: # (End of RBAC section)

## <a name="next-steps"></a>다음 단계
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health 에이전트 설치](active-directory-aadconnect-health-agent-install.md)
* [AD FS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adfs.md)
* [동기화에 대한 Azure AD Connect Health 사용](active-directory-aadconnect-health-sync.md)
* [AD DS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health FAQ](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 버전 내역](active-directory-aadconnect-health-version-history.md)
