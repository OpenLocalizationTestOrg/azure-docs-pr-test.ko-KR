---
title: "정보 얻기: Azure AD 암호 관리 보고서 | Microsoft Docs"
description: "이 문서에서는 toouse 조직에서 암호 관리 작업에 대 한 tooget 한 정보를 보고 하는 방법을 설명 합니다."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 1472b51d-53f4-4b0f-b1be-57f6fa88fa65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 90e0b8e621cdfe3e3a2f15df7b98115008855500
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-operational-insights-with-password-management-reports"></a>암호 관리와 함께 operational insights를 tooget 보고 하는 방법
> [!IMPORTANT]
> **로그인하는 데 문제가 있나요?** 그렇다면 [암호를 변경하고 재설정하는 방법은 다음과 같습니다](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
>
>

이 섹션에서는 Azure Active Directory를 사용 하는 방법을 설명 암호 관리 사용자 암호 재설정을 사용 하는 하 고 조직에서 변경 하는 방법을 tooview를 보고 합니다.

* [**암호 관리 보고서 개요**](#overview-of-password-management-reports)
* [**Tooview 암호 관리 hello 새 Azure 포털에서 보고 하는 방법**](#how-to-view-password-management-reports)
 * [디렉터리 역할 tooread 보고서 허용](#directory-roles-allowed-to-read-reports)
* [**셀프 서비스 암호 관리 활동 형식에서 hello 새 Azure 포털**](#self-service-password-management-activity-types)
 * [셀프 서비스 암호 다시 설정에서 차단](#activity-type-blocked-from-self-service-password-reset)
 * [암호 변경(셀프 서비스)](#activity-type-change-password-self-service)
 * [암호 다시 설정(관리자)](#activity-type-reset-password-by-admin)
 * [암호 다시 설정(셀프 서비스)](#activity-type-reset-password-self-service)
 * [셀프 서비스 암호 다시 설정 흐름 활동 진행률](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [사용자 계정 잠금 해제(셀프 서비스)](#activity-type-unlock-user-account-self-service)
 * [사용자가 셀프 서비스 암호 다시 설정 등록](#activity-type-user-registered-for-self-service-password-reset)
* [**Azure AD 보고서 및 이벤트 API에서 tooretrieve 암호 관리 이벤트 hello 하는 방법**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [보고 API 데이터 검색 제한](#reporting-api-data-retrieval-limitations)
* [**Toodownload 암호 다시 설정 하는 PowerShell 사용 하 여 신속 하 게 등록 이벤트**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**Tooview 암호 관리 hello 클래식 포털에서 보고 하는 방법**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**암호 재설정 등록 활동 hello 클래식 포털에서 조직에서 보기**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**암호 재설정 활동 hello 클래식 포털에서 조직에서 보기**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>암호 관리 보고서 개요
암호 재설정을 배포한 후 조직에서 사용 되 고 방법 toosee hello 가장 일반적인 다음 단계 중 하나입니다.  예를 들어, tooget 통찰력 수도 사용자가 암호 재설정 또는 암호 수를 등록 하는 방법으로 재설정 수행 되었는지를 hello 지난 며칠간 합니다.  다음은 일부의 hello에 존재 하는 hello 암호 관리 보고서와 함께 수 tooanswer 될 hello 일반적인 질문 [Azure 관리 포털](https://manage.windowsazure.com) 오늘:

* 얼마나 많은 사람들이 암호 재설정을 위해 등록합니까?
* 누가 암호 재설정을 위해 등록합니까?
* 사람들이 등록하는 데이터는 무엇입니까?
* 얼마나 많은 사람들이 지난 7 일 동안 hello에 암호를 다시 설정
* 어떤 hello 가장 일반적인 방법 사용자 또는 관리자 tooreset 자신의 암호를 사용?
* 사용자 또는 관리자 얼굴 toouse 암호 재설정을 시도할 때 문제 공통 무엇 인가요?
* 어느 관리자가 자신의 암호를 자주 재설정합니까?
* 암호 재설정에 대해 의심스러운 활동이 있습니까?

## <a name="how-tooview-password-management-reports"></a>Tooview 암호 관리를 보고 하는 방법
새 hello에 [Azure 포털](https://portal.azure.com) 하세요는 향상 된 방식으로 tooview 암호 재설정 및 암호 재설정 등록 활동 있다고 합니다.  다시 설정에서 새 hello 등록 이벤트 toofind hello 암호 재설정 및 암호 아래 hello 단계 수행 [Azure 포털](https://portal.azure.com):

1. 너무 이동[**portal.azure.com**](https://portal.azure.com)
2. Hello 클릭 **더 많은 서비스** hello 기본 Azure 포털 왼쪽 탐색 메뉴
3. 검색할 **Azure Active Directory** 에 서비스 목록이 hello 및 선택
4. 클릭 **사용자 및 그룹** hello Azure Active Directory 탐색 메뉴에서
5. Hello 클릭 **감사 로그** hello 사용자 및 그룹 탐색 메뉴에서 탐색 항목입니다. 이 안내해 모든 hello 사용자에 대해 hello 감사 이벤트 발생의 모든 디렉터리에서. 이 보기 toosee 모든 hello 암호 관련 이벤트에도 필터링 할 수 있습니다.
6. 이 보기 tooonly hello 암호 관리와 관련 된 toofilter 이벤트, 클릭 hello **필터** hello hello 블레이드 위쪽에 단추입니다.
7. Hello에서 **필터** 메뉴에서 선택 hello **범주** 드롭다운에서 toohello 변경 **셀프 서비스 암호 관리** 범주 유형입니다.
8. Hello 별을 선택 하 여 필요에 따라 추가 필터 hello 목록 **활동** 관심 있는
### <a name="direct-link-toouser-audit-blade"></a>직접 링크 tooUser 감사 블레이드
Tooyour 포털에 로그인 한 경우 다음과 같습니다 직접 링크 toohello 사용자 감사 블레이드 이러한 이벤트를 확인할 수 있습니다.

* [Toouser 관리 뷰를 직접 감사 이동](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-tooread-reports"></a>디렉터리 역할 tooread 보고서 허용
현재 hello 다음 디렉터리 역할을 읽을 수 있습니다 hello 클래식 Azure 포털에서 Azure AD 암호 관리 보고서:

* 전역 관리자

전에 수 tooread 이러한 보고서를 hello 회사의 전역 관리자 해야가 옵트인 적어도 한 번 탭 또는 감사 로그를 보고 하는 hello를 방문 하 여 hello 조직을 대신 하 여 검색할 데이터 toobe이에 대 한 합니다. 이렇게 할 때까지는 조직의 데이터가 수집되지 않습니다.

디렉터리 역할 및 있습니다 수에 대 한 참조를 tooread [Azure Active Directory에서 관리자 역할 할당](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles)합니다.

## <a name="self-service-password-management-activity-types"></a>셀프 서비스 암호 관리 활동 유형
hello에 hello 활동 유형만 표시 **셀프 서비스 암호 관리** audit 이벤트 범주입니다.  각각에 대한 설명은 다음과 같습니다.

* [**셀프 서비스 암호 재설정에서 차단** ](#activity-type-blocked-from-self-service-password-reset) -사용자가 tooreset 암호를 나타냅니다. 특정 게이트를 사용 하거나 24 시간 동안의 총 5 개의 시간 전화 번호를 확인 합니다.
* [**암호 (셀프 서비스)를 변경** ](#activity-type-change-password-self-service) -사용자는 자발적 수행 하거나 강제로 적용 나타냅니다 (due tooexpiry) 암호를 변경 합니다.
* [**(관리자)가 암호 재설정** ](#activity-type-reset-password-by-admin) -관리자가 암호 재설정 hello Azure 포털에서에서 사용자를 대신해 서 수행을 나타냅니다.
* [**암호 재설정 (셀프 서비스)** ](#activity-type-reset-password-self-service) -사용자는 성공적으로 hello에서 암호 재설정 나타냅니다 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com)합니다.
* [**자체 serve 암호 재설정 흐름 활동 진행률** ](#activity-type-self-serve-password-reset-flow-activity-progress) -hello 암호의 일부 프로세스를 다시 설정 하는 대로 각 특정 단계 (예: 특정 암호를 전달 인증 게이트 다시 설정)을 통해 진행 되는 사용자를 나타냅니다.
* [**사용자 계정 (셀프 서비스)를 잠금 해제** ](#activity-type-unlock-user-account-self-service) -사용자 잠금을 해제 했습니다. 해당 Active Directory 계정을 hello에서 자신의 암호를 재설정 하지 않고 나타냅니다 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com) hello를 사용 하 여 [재설정 하지 않고 AD 계정 잠금 해제](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) 기능입니다.
* [**사용자 셀프 서비스 암호 재설정에 등록** ](#activity-type-user-registered-for-self-service-password-reset) -사용자가 등록 모든 필요한 hello 정보 toobe 수 tooreset hello 현재 지정 된 테 넌 트 암호 재설정 정책에 따라 암호를 나타냅니다.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>활동 유형: 셀프 서비스 암호 다시 설정에서 차단
hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 나타냅니다 사용자 시도 tooreset 암호, 특정 게이트를 사용 하 여 또는 24 시간 동안의 총 5 개의 시간 전화 번호를 확인 합니다.
* **작업 자가** -수행할 추가 제한 되었다는 hello 사용자 작업을 다시 설정 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **작업 대상** -수행할 추가 제한 되었다는 hello 사용자 작업을 다시 설정 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
 * _성공_ -사용자가 조정 하는 모든 추가 재설정을 수행할 모든 추가 인증 방법을 시도 또는 다음 24 시간 동안 hello에 대 한 모든 추가 전화 번호 유효성을 검사 합니다.
* **활동 상태 실패 이유** - 해당 없음

### <a name="activity-type-change-password-self-service"></a>활동 유형: 암호 변경(셀프 서비스)
hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 사용자는 자발적 수행 하거나 강제로 적용 나타냅니다 (due tooexpiry) 암호를 변경 합니다.
* **작업 자가** -hello 사용자에 게 암호를 변경 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **작업 대상** -hello 사용자에 게 암호를 변경 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
 * _성공_ - 사용자가 자신의 암호를 성공적으로 변경했음을 나타냅니다.
 * _오류_ -사용자가 자신의 암호를 toochange 실패 했음을 나타냅니다. Hello 행을 클릭 하면 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다.
* **활동 상태 실패 이유** -
 * _FuzzyPolicyViolationInvalidPassword_ -hello 사용자는 너무 일반적 또는 특히 취약 toobe 찾기 tooMicrosoft의 암호 검색 사용 금지 기능이 인해 자동으로 금지 된 암호를 선택 합니다.

### <a name="activity-type-reset-password-by-admin"></a>활동 유형: 암호 다시 설정(관리자)
hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 관리자가 암호 재설정 hello Azure 포털에서에서 사용자를 대신해 서 수행을 나타냅니다.
* **작업 자가** -hello 암호를 재설정 대신 다른 최종 사용자 또는 관리자가 관리자에 게 있습니다. 전역 관리자, 암호 관리자, 사용자 관리자 또는 기술 지원팀 관리자여야 합니다.
* **작업 대상** -hello 사용자 암호 다시 설정 되었습니다. 최종 사용자 또는 다른 관리자일 수 있습니다.
* **허용되는 활동 상태**
 * _성공_ - 관리자가 사용자의 암호를 성공적으로 다시 설정했음을 나타냅니다.
 * _오류_ -관리자가 사용자의 암호 toochange 실패 했음을 나타냅니다. Hello 행을 클릭 하면 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다.

### <a name="activity-type-reset-password-self-service"></a>활동 유형: 암호 다시 설정(셀프 서비스)
hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 사용자는 성공적으로 hello에서 암호 재설정 나타냅니다 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com)합니다.
* **작업 자가** -hello 사용자가 자신의 암호를 재설정 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **작업 대상** -hello 사용자가 자신의 암호를 재설정 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
 * _성공_ - 사용자가 자신의 암호를 성공적으로 다시 설정했음을 나타냅니다.
 * _오류_ -는 사용자가 자신의 암호 tooreset 실패 했음을 나타냅니다. Hello 행을 클릭 하면 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다.
* **활동 상태 실패 이유** -
 * _FuzzyPolicyViolationInvalidPassword_ -admin 님 안녕하세요 tooMicrosoft의 암호 검색 사용 금지 기능이 너무 일반적 또는 특히 취약 toobe 찾기 인해 자동으로 금지 된 하는 암호를 선택 합니다.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>활동 유형: 셀프 서비스 암호 다시 설정 흐름 활동 진행률
hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 사용자 진행 (예: 전달 특정 암호 재설정 인증 게이트) hello 암호의 일부 프로세스를 다시 설정 하는 대로 각 특정 단계를 나타냅니다.
* **작업 자가** -hello 암호의 일부를 수행한 hello 사용자 흐름을 다시 설정 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **작업 대상** -hello 암호의 일부를 수행한 hello 사용자 흐름을 다시 설정 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
 * _성공_ -hello 암호 재설정 흐름의 특정 단계를 성공적으로 완료 하는 사용자를 나타냅니다.
 * _오류_ -hello 암호의 특정 단계를 다시 설정 실패 흐름을 나타냅니다. Hello 행을 클릭 하면 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다.
* **허용되는 활동 상태 이유**
 * [모든 허용되는 다시 설정 활동 상태 이유](#allowed-values-for-details-column)에 대해서는 아래 표를 참조하세요.

### <a name="activity-type-unlock-user-account-self-service"></a>활동 유형: 사용자 계정 잠금 해제(셀프 서비스)
hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 사용자 잠금을 해제 했습니다. 해당 Active Directory 계정을 hello에서 자신의 암호를 재설정 하지 않고 나타냅니다 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com) hello를 사용 하 여 [AD 계정 잠금 다시 설정 하지 않고 해제](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) 기능입니다.
* **작업 자가** -hello 사용자가 자신의 암호를 재설정 하지 않고 계정 잠금 해제 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **작업 대상** -hello 사용자가 자신의 암호를 재설정 하지 않고 계정 잠금 해제 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
 * _성공_ - 사용자가 자신의 계정을 성공적으로 잠금 해제했음을 나타냅니다.
 * _오류_ -된 사용자 실패 toounlock 자신의 계정을 나타냅니다. Hello 행을 클릭 하면 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>활동 유형: 사용자가 셀프 서비스 암호 다시 설정 등록
hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 사용자가 등록 모든 필요한 hello 정보 toobe 수 tooreset hello 현재 지정 된 테 넌 트 암호 재설정 정책에 따라 암호를 나타냅니다.
* **작업 자가** -hello 사용자에 게 암호 재설정에 등록 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **작업 대상** -hello 사용자에 게 암호 재설정에 등록 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
 * _성공_ -암호 재설정 hello 현재 정책에 따라에 성공적으로 등록 된 사용자를 나타냅니다.
 * _오류_ -암호 재설정을 위해 사용자 실패 tooregister 나타냅니다. Hello 행을 클릭 하면 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다. 참고-이 사용자를 의미 하지는 못할 tooreset 정당한 자신이 hello 등록 프로세스 완료 되지 않았습니다 자신의 암호입니다. (예: 전화 번호를 유효성이 검사 되지 않은), 올바른 사용자 계정에 확인 되지 않은 데이터가 있는 경우이 전화 번호를 확인 하지 않았으며, 경우에 여전히를 사용할 수 있습니다 tooreset 암호입니다. 자세한 내용은 [사용자가 등록하면 어떻게 되나요?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)를 참조하세요.

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>Azure AD 보고서 및 이벤트 API에서 tooretrieve 암호 관리 이벤트 hello 하는 방법
2015 년 8 월을 기준으로 hello Azure AD 보고서 및 이벤트 API 이제 지원 hello 암호 재설정 및 암호 재설정 등록 보고서에 포함 된 hello 정보를 모두 검색 합니다. 이 API를 사용 하 여 개별 암호 재설정을 다운로드할 수 있습니다 및 암호는 통합에 대 한 등록 이벤트가 보고 기술을 프로그램 choce의 hello로 다시 설정 합니다.

### <a name="how-tooget-started-with-hello-reporting-api"></a>Tooget 보고 API hello로 시작 하는 방법
tooaccess이이 데이터를 스크립트 tooretrieve 옮기거나 해야 toowrite는 작은 응용 프로그램 서버에서 합니다. [Tooget를 어떻게 시작 hello Azure AD Reporting API에 알아봅니다](active-directory-reporting-api-getting-started.md)합니다.

작동 하는 스크립트를 만든 후 다음 tooexamine hello 암호 재설정 및 등록 이벤트를 검색할 수 있습니다 toomeet 시나리오에이 좋습니다.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): 암호 다시 설정 이벤트에 대해 사용할 수 있는 hello 열 나열
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): 암호 재설정 등록 이벤트에 사용할 수 있는 hello 열 나열

### <a name="reporting-api-data-retrieval-limitations"></a>보고 API 데이터 검색 제한
현재 Azure AD 보고서 hello 및 이벤트 API 너무 검색**사람들이 75000 개별 이벤트** 의 hello [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) 및 [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) 형식 스패닝 hello **지난 30 일 동안**합니다.

Tooretrieve 필요 하거나이 창의 초과 하 여 데이터를 저장할 경우 외부 데이터베이스에 유지 하 고 발생 하는 hello API tooquery hello 델타를 사용 하는 것이 좋습니다. 가장 좋은 방법은 조직의 등록 프로세스를 다시 설정, 외부적으로 유지 한 다음이 지점에서 tootrack hello 델타를 앞으로 계속 toobegin 암호를 시작할 때이 데이터를 검색 합니다.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Toodownload 암호 다시 설정 하는 PowerShell 사용 하 여 신속 하 게 등록 이벤트
또한 toousing hello Azure AD 보고서 및 이벤트 API 직접, PowerShell 스크립트 toorecent 등록 이벤트 아래 hello 디렉터리에 사용할 수도 있습니다. 이 toosee 최근에 등록에 원하는 경우에 유용 하거나 tooensure 암호 재설정 출시를 예상 대로 수행 되 게 합니다.

* [Azure AD SSPR 등록 활동 PowerShell 스크립트](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-tooview-password-management-reports-in-hello-classic-portal"></a>Tooview 암호 관리 hello 클래식 포털에서 보고 하는 방법
아래의 hello 단계를 수행 하는 toofind hello 암호 관리 보고서:

1. Hello 클릭 **Active Directory** hello에서 확장 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 포털에 표시 되는 hello 목록에서 디렉터리를 선택 합니다.
3. Hello 클릭 **보고서** 탭 합니다.
4. Hello에서 **활동 로그** 섹션.
5. 어느 hello 선택 **암호 재설정 활동** 보고서 또는 hello **암호 재설정 등록 활동** 보고서입니다.

## <a name="view-password-reset-registration-activity-in-hello-classic-portal"></a>암호 재설정 등록 활동 hello 클래식 포털에서 보기
hello 암호 재설정 등록 활동 보고서는 모든 암호 재설정 등록이 조직에서 발생 한 보여 줍니다.  암호 재설정을 등록 하는 모든 등록 된 사용자는 성공적으로 인증 정보에 hello 암호 재설정 등록 포털에 대해이 보고서에 표시 됩니다 ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)).

* **최대 시간 범위**: 30일
* **최대 행 수**: 75,000개
* **다운로드 가능**: 예, CSV 파일을 통해

### <a name="description-of-report-columns"></a>보고서 열 설명
hello 다음 목록에서는 각 hello 보고서 열을 자세히 설명 합니다.

* **사용자** – hello 려 한 사용자가 암호 재설정 등록 작업입니다.
* **역할** – hello 디렉터리에 hello 사용자의 hello 역할입니다.
* **날짜 및 시간** – hello의 날짜 및 시간 hello 시도 합니다.
* **등록 된 데이터** – 암호 중에 제공 된 어떤 인증 데이터 hello 사용자 등록을 재설정 합니다.

### <a name="description-of-report-values"></a>보고서 값 설명
hello 다음 표에서 각 열에 대해 허용 되는 hello 서로 다른 값.

| 열 | 허용되는 값과 해당 의미 |
| --- | --- |
| 등록된 데이터 |**암호 확인용 메일** – 사용 되는 사용자 대체 전자 메일 또는 인증 전자 메일 tooauthenticate<p><p>**사무실 전화**– 사무실 전화 tooauthenticate를 사용 하는 사용자<p>**휴대폰** -사용자 휴대폰 또는 인증 전화 tooauthenticate 사용<p>**보안 질문** – 사용 되는 사용자 보안 질문 tooauthenticate<p>**어떠한 조합의 (예: 암호 확인용 메일 + 휴대폰) 위에 hello** – 2 개의 게이트 정책이 지정 되 고 두 가지 방법이 사용 되는 사용자 tooauthentication hello를 표시 하는 경우에 발생가 암호 재설정 요청 합니다. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>암호 재설정 활동 hello 클래식 포털에서 보기
이 보고서는 조직 내에서 발생한 모든 암호 재설정 시도를 보여줍니다.

* **최대 시간 범위**: 30일
* **최대 행 수**: 75,000개
* **다운로드 가능**: 예, CSV 파일을 통해

### <a name="description-of-report-columns"></a>보고서 열 설명
hello 다음 목록에서는 각 hello 보고서 열을 자세히 설명 합니다.

1. **사용자** – hello 려 한 사용자가 암호 재설정 작업 (hello 사용자 tooreset 암호를 제공 하는 경우에 제공 하는 hello 사용자 ID 필드에 기반).
2. **역할** – hello 디렉터리에 hello 사용자의 hello 역할입니다.
3. **날짜 및 시간** – hello의 날짜 및 시간 hello 시도 합니다.
4. **사용 된 메서드** – 인증 방법을 hello 사용자의 사용이 재설정 작업에 대 한 합니다.
5. **결과** – hello 암호의 hello 최종 결과 작업을 다시 설정 합니다.
6. **세부 정보** – 이유 hello 암호 재설정의 hello 세부 정보에서 수행한 hello 값에서 발생 했습니다.  또한 예기치 않은 오류가 tooresolve를 수행할 수 있는 완화 단계를 포함 합니다.

### <a name="description-of-report-values"></a>보고서 값 설명
hello 다음 표에서 각 열에 대해 허용 되는 hello 서로 다른 값.

| 열 | 허용되는 값과 해당 의미 |
| --- | --- |
| 사용된 메서드 |**암호 확인용 메일** – 사용 되는 사용자 대체 전자 메일 또는 인증 전자 메일 tooauthenticate<p>**사무실 전화** – 사무실 전화 tooauthenticate를 사용 하는 사용자<p>**휴대폰** – 사용자 휴대폰 또는 인증 전화 tooauthenticate 사용<p>**보안 질문** – 사용 되는 사용자 보안 질문 tooauthenticate<p>**어떠한 조합의 (예: 암호 확인용 메일 + 휴대폰) 위에 hello** – 2 개의 게이트 정책이 지정 되 고 두 가지 방법이 사용 되는 사용자 tooauthentication hello를 표시 하는 경우에 발생가 암호 재설정 요청 합니다. |
| 결과 |**중단됨** – 사용자가 암호 재설정을 시작하지만 완료하지 않고 중간에서 중단됩니다.<p>**차단** – 사용자의 계정이 금지 toouse 암호 tooattempting toouse hello 암호 재설정 페이지 인해 재설정 되었습니다. 또는 너무 여러 번 24 시간 동안에서에서 단일 암호 재설정 게이트<p>**취소** – 사용자가 암호 재설정을 시작 했지만 hello 취소 단추 toocancel hello 세션 도중 클릭 한 다음 <p>**관리자에 연결할** – hello 암호 재설정 흐름 hello 사용자 hello 끝내 지 않고 "관리자에 게 문의" 링크를 클릭 합니다. 하므로, 사용자는 해결할 수 없는 자신의 세션 중에 문제가 발생 했습니다<p>**실패** – hello 사용자가 구성 된 toouse hello 기능 (예: 라이선스 없음, 인증 정보, 암호 관리는 온-프레미스 되지만 쓰기 저장을 누락 해제 됨) 때문에 사용자가 수 tooreset 암호를 없습니다.<p>**성공함** - 암호가 재설정되었습니다. |
| 세부 정보 |아래 테이블을 참조하세요. |

### <a name="allowed-values-for-details-column"></a>세부 정보 열에 대해 허용되는 값
다음은 hello 목록이 재설정 활동 보고서 hello 암호를 사용 하는 경우 예상 결과 형식입니다.

| 세부 정보 | 결과 형식 |
| --- | --- |
| 사용자가 hello 전자 메일 확인 옵션을 완료 한 후 중단 됨 |Abandoned |
| 사용자가 hello 모바일 SMS 확인 옵션을 완료 한 후 중단 됨 |Abandoned |
| 사용자가 hello 모바일 음성 통화 확인 옵션을 완료 한 후 중단 됨 |Abandoned |
| 사용자가 hello 사무실 음성 통화 확인 옵션을 완료 한 후 중단 됨 |Abandoned |
| 사용자가 hello 보안 질문 옵션을 완료 한 후 중단 됨 |Abandoned |
| 사용자가 사용자 ID를 입력한 후 중단함 |Abandoned |
| 사용자가 hello 전자 메일 확인 옵션을 시작한 후 중단 됨 |Abandoned |
| 사용자가 hello 모바일 SMS 확인 옵션을 시작한 후 중단 됨 |Abandoned |
| 사용자가 hello 모바일 음성 통화 확인 옵션을 시작한 후 중단 됨 |Abandoned |
| 사용자 hello 사무실 음성 통화 확인 옵션을 시작한 후 중단 |Abandoned |
| 사용자가 hello 보안 질문 옵션을 시작한 후 중단 됨 |Abandoned |
| 사용자가 새 암호를 선택하기 전에 중단함 |Abandoned |
| 사용자가 새 암호를 선택하는 중에 중단함 |Abandoned |
| 사용자가 너무 많은 잘못된 SMS 확인 코드를 입력하여 24시간 동안 차단됨 |Blocked |
| 사용자가 너무 많이 모바일 음성 인증을 시도하여 24시간 동안 차단됨 |Blocked |
| 사용자가 너무 많이 사무실 음성 인증을 시도하여 24시간 동안 차단됨 |Blocked |
| 사용자는 tooanswer 보안 질문을 너무 많이 시도해 및 24 시간 동안 차단 됨 |Blocked |
| 사용자는 tooverify 전화 번호를 너무 많이 시도해 및 24 시간 동안 차단 됨 |Blocked |
| 사용자가 hello 필요한 인증 방법을 통과 하기 전에 취소 |Cancelled |
| 사용자가 새 암호를 전송하기 전에 취소함 |Cancelled |
| Hello 전자 메일 확인 옵션을 시도한 후 관리자에 대 한 사용자 연결 |Contacted admin |
| Hello 모바일 SMS 확인 옵션을 시도한 후 관리자에 대 한 사용자 연결 |Contacted admin |
| Hello 모바일 음성 통화 확인 옵션을 시도한 후 관리자에 대 한 사용자 연결 |Contacted admin |
| Hello 사무실 음성 통화 확인 옵션을 시도한 후 관리자에 대 한 사용자 연결 |Contacted admin |
| Hello 보안 질문 확인 옵션을 시도한 후 관리자에 대 한 사용자 연결 |Contacted admin |
| 이 사용자에 대한 암호 재설정이 사용되지 않습니다. 사용에서 암호 다시 설정을 hello 탭 tooresolve이 옵션을 구성합니다 |실패 |
| 사용자에게 라이선스가 없습니다. 이 라이선스 toohello 사용자 tooresolve를 추가할 수 있습니다. |실패 |
| 사용자 쿠키를 사용 하지 않고 장치에서 tooreset을 했습니다. |실패 |
| 사용자의 계정에 정의된 인증 메서드가 부족합니다. 이 인증 정보 tooresolve 추가 |실패 |
| 사용자의 암호는 관리 대상 온-프레미스입니다. 이 암호 쓰기 저장 tooresolve를 활성화할 수 있습니다. |실패 |
| 온-프레미스 암호 재설정 서비스에 접근할 수 없습니다. 동기화 컴퓨터의 이벤트 로그를 확인합니다. |실패 |
| Hello 사용자의 온-프레미스 암호를 재설정 하는 동안 문제가 발생 했습니다. 동기화 컴퓨터의 이벤트 로그를 확인합니다. |실패 |
| 이 사용자 hello 암호 재설정 사용자 그룹의 구성원이 아닙니다. 이 사용자 toothat 그룹 tooresolve이를 추가 합니다. |실패 |
| 암호 재설정은 이 테넌트에 대해 완전히 비활성화되었습니다. 참조 [여기](http://aka.ms/ssprtroubleshoot) tooresolve이 있습니다. |실패 |
| 사용자가 성공적으로 암호를 재설정함 |Succeeded |

## <a name="next-steps"></a>다음 단계
다음 링크 tooall hello의 Azure AD 암호 재설정 설명서 페이지는:

* **로그인하는 데 문제가 있나요?** 그렇다면 [암호를 변경하고 재설정하는 방법은 다음과 같습니다](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
* [**작동 방법** ](active-directory-passwords-how-it-works.md) -hello 서비스 및 6 개의 서로 다른 구성 요소 hello에 대 한 자세한 내용은 각 메서드의
* [**시작 하기** ](active-directory-passwords-getting-started.md) -자세한 방법을 tooallow tooreset 사용자가 클라우드 또는 온-프레미스 암호를 변경 하 고
* [**사용자 지정** ](active-directory-passwords-customize.md) -toocustomize hello 모양을 학습 및 동작의 hello 모양과 느낌이 tooyour 조직의 요구를 서비스
* [**모범 사례** ](active-directory-passwords-best-practices.md) -tooquickly 배포 하 고 효과적으로 조직에서 암호를 관리 하는 방법에 대해 알아봅니다
* [**FAQ** ](active-directory-passwords-faq.md) -toofrequently 질문과 답변
* [**문제 해결** ](active-directory-passwords-troubleshoot.md) -tooquickly hello 서비스 문제를 해결 하는 방법에 대해 알아봅니다
* [**자세한 내용은** ](active-directory-passwords-learn-more.md) -hello 서비스의 작동 방식을 기술 세부 정보 hello 심층적으로 이동
