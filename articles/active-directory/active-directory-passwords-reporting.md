---
title: "보고: Azure AD SSPR | Microsoft Docs"
description: "Azure AD 셀프 서비스 암호 재설정 이벤트에 대한 보고"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: af65b9be1e00c2819431694a5b0064b97b9e1867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Azure AD 암호 관리에 대한 보고 옵션

대부분의 조직에서는 원하는 tooknow 어떻게 또는 SSPR 실제로 사용 중인 경우 배포를 게시 합니다. Azure AD에는 적절 하 게 사용 허가 하는 경우 사용 하면 toocreate 사용자 지정 쿼리 및 보고 기능을 사용 하 여 tooanswer 질문 하는 데 도움이 고정 보고서를 제공 합니다.

hello 다음과 같은 질문에 대답할 수 있습니다 [Azure 포털] hello에 존재 하는 보고서에서 (https://portal.azure.com/).

> [!NOTE]
> 여야 [전역 관리자](active-directory-assign-admin-roles.md#assign-or-remove-administrator-roles) 및 해야 옵트인이 사용자 조직을 대신 하 여 수집 된 데이터 toobe 방문 hello 보고 탭 이나 감사 하 여 로그에 한 번 이상. 이렇게 할 때까지는 조직의 데이터가 수집되지 않습니다.

* 얼마나 많은 사람들이 암호 재설정을 위해 등록합니까?
* 누가 암호 재설정을 위해 등록합니까?
* 사람들이 등록하는 데이터는 무엇입니까?
* 얼마나 많은 사람들이 지난 7 일 hello에 암호를 다시 설정
* 어떤 hello 가장 일반적인 방법 사용자 또는 관리자 tooreset 자신의 암호를 사용?
* 사용자 또는 관리자 얼굴 toouse 암호 재설정을 시도할 때 문제 공통 무엇 인가요?
* 어느 관리자가 자신의 암호를 자주 재설정합니까?
* 암호 재설정에 대해 의심스러운 활동이 있습니까?

## <a name="how-tooview-password-management-reports-in-hello-azure-portal"></a>Tooview 암호 관리 hello Azure 포털에서에서 보고 하는 방법

Azure 포털 환경 hello에는 향상 된 방식으로 tooview 암호 재설정 및 암호 재설정 등록 활동을 개가 있습니다.  Toofind hello 암호 재설정 및 암호 재설정 등록 이벤트 아래 hello 단계를 수행 합니다.

1. 너무 이동[**portal.azure.com**](https://portal.azure.com)
2. Hello 클릭 **더 많은 서비스** hello 기본 Azure 포털 왼쪽 탐색 메뉴
3. 검색할 **Azure Active Directory** 에 서비스 목록이 hello 및 선택
4. 클릭 **사용자 및 그룹** hello Azure Active Directory 탐색 메뉴에서
5. Hello 클릭 **감사 로그** hello 사용자 및 그룹 탐색 메뉴에서 탐색 항목입니다. 이렇게 하면 모든 hello 사용자 디렉터리에 대해 발생 하는 hello 감사 이벤트의 모든. 이 보기 toosee 모든 hello 암호 관련 이벤트에도 필터링 할 수 있습니다.
6. toofilter이 tooonly hello 암호 재설정 보기 관련된 이벤트를 hello 클릭 **필터** hello hello 블레이드 위쪽에 단추입니다.
7. Hello에서 **필터** 메뉴에서 선택 hello **범주** 드롭다운에서 toohello 변경 **셀프 서비스 암호 관리** 범주 유형입니다.
8. Hello 별을 선택 하 여 필요에 따라 추가 필터 hello 목록 **활동** 관심 있는

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>Azure AD 보고서 및 이벤트 API에서 tooretrieve 암호 관리 이벤트 hello 하는 방법

hello Azure AD 보고서 및 이벤트 API 암호 재설정 및 암호 재설정 등록 보고서에 포함 된 모든 hello 정보 검색을 지원 합니다. 이 API를 사용 하 여 개별 암호 재설정을 다운로드할 수 있습니다 및 암호는 통합에 대 한 등록 이벤트가 보고 기술을 선택한 hello로 다시 설정 합니다.

### <a name="how-tooget-started-with-hello-reporting-api"></a>Tooget 보고 API hello로 시작 하는 방법

tooaccess이이 데이터는 작은 응용 프로그램 toowrite 필요 하거나 tooretrieve 스크립트 서버에서 합니다. [Tooget를 어떻게 시작 hello Azure AD Reporting API에 알아봅니다](active-directory-reporting-api-getting-started.md)합니다.

작동 하는 스크립트를 만든 후 다음 tooexamine hello 암호 재설정 및 등록 이벤트를 검색할 수 있습니다 toomeet 시나리오에이 좋습니다.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): 암호 다시 설정 이벤트에 대해 사용할 수 있는 hello 열 나열
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): 암호 재설정 등록 이벤트에 사용할 수 있는 hello 열 나열

### <a name="reporting-api-data-retrieval-limitations"></a>보고 API 데이터 검색 제한

현재 Azure AD 보고서 hello 및 이벤트 API 너무 검색**사람들이 75000 개별 이벤트** 의 hello [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) 및 [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) 형식 스패닝 hello **지난 30 일 동안**합니다.

Tooretrieve 필요 하거나이 창의 초과 하 여 데이터를 저장할 경우 외부 데이터베이스에 유지 하 고 발생 하는 hello API tooquery hello 델타를 사용 하는 것이 좋습니다. 권장 하는 것은 toobegin SSPR을 사용 하 여 조직에서 시작 하 고 외부적으로 유지 한 다음이 지점에서 tootrack hello 델타를 앞으로 계속이 데이터를 검색 합니다.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Toodownload 암호 다시 설정 하는 PowerShell 사용 하 여 신속 하 게 등록 이벤트

또한 toousing hello Azure AD 보고서 및 이벤트 API 직접, PowerShell 스크립트 toorecent 등록 이벤트 아래 hello 디렉터리에 사용할 수도 있습니다. 이 toosee 최근에 등록에 원하는 경우에 유용 하거나 tooensure 암호 재설정 출시를 예상 대로 수행 되 게 합니다.

* [Azure AD SSPR 등록 활동 PowerShell 스크립트](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

### <a name="description-of-report-columns-in-azure-portal"></a>Azure Portal의 보고서 열 설명

hello 다음 목록에서는 각 hello 보고서 열을 자세히 설명 합니다.

* **사용자** – hello 려 한 사용자가 암호 재설정 등록 작업입니다.
* **역할** – hello 디렉터리에 hello 사용자의 hello 역할입니다.
* **날짜 및 시간** – hello의 날짜 및 시간 hello 시도 합니다.
* **등록 된 데이터** – 암호 중에 제공 된 어떤 인증 데이터 hello 사용자 등록을 재설정 합니다.

### <a name="description-of-report-values-in-azure-portal"></a>Azure Portal의 보고서 값 설명

hello 다음 표에서 각 열에 대해 허용 되는 hello 서로 다른 값.

| 열 | 허용되는 값과 해당 의미 |
| --- | --- |
| 등록된 데이터 |**암호 확인용 메일** – 사용 되는 사용자 대체 전자 메일 또는 인증 전자 메일 tooauthenticate<p><p>**사무실 전화**– 사무실 전화 tooauthenticate를 사용 하는 사용자<p>**휴대폰** -사용자 휴대폰 또는 인증 전화 tooauthenticate 사용<p>**보안 질문** – 사용 되는 사용자 보안 질문 tooauthenticate<p>**어떠한 조합의 (예: 암호 확인용 메일 + 휴대폰) 위에 hello** – 2 개의 게이트 정책이 지정 되 고 두 가지 방법이 사용 되는 사용자 tooauthentication hello를 표시 하는 경우에 발생가 암호 재설정 요청 합니다. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>암호 재설정 활동 hello 클래식 포털에서 보기

이 보고서는 조직 내에서 발생한 모든 암호 재설정 시도를 보여줍니다.

* **최대 시간 범위**: 30일
* **최대 행 수**: 75,000개
* **다운로드 가능**: 예, CSV 파일을 통해

### <a name="description-of-report-columns-in-azure-classic-portal"></a>Azure 클래식 포털의 보고서 열 설명

hello 다음 목록에서는 각 hello 보고서 열을 자세히 설명 합니다.

1. **사용자** – hello 려 한 사용자가 암호 재설정 작업 (hello 사용자 tooreset 암호를 제공 하는 경우에 제공 하는 hello 사용자 ID 필드에 기반).
2. **역할** – hello 디렉터리에 hello 사용자의 hello 역할입니다.
3. **날짜 및 시간** – hello의 날짜 및 시간 hello 시도 합니다.
4. **메서드 사용** – 인증 방법을 hello 사용자의 사용이 재설정 작업에 대 한 합니다.
5. **결과** – hello 결과인 hello 암호 재설정 작업 합니다.
6. **세부 정보** – 이유 hello 암호 재설정의 hello 세부 정보에서 수행한 hello 값에서 발생 했습니다.  또한 예기치 않은 오류가 tooresolve를 수행할 수 있는 완화 단계를 포함 합니다.

### <a name="description-of-report-values-in-azure-classic-portal"></a>Azure 클래식 포털의 보고서 값 설명

hello 다음 표에서 각 열에 대해 허용 되는 hello 서로 다른 값.

| 열 | 허용되는 값과 해당 의미 |
| --- | --- |
| 사용된 메서드 |**암호 확인용 메일** – 사용 되는 사용자 대체 전자 메일 또는 인증 전자 메일 tooauthenticate<p>**사무실 전화** – 사무실 전화 tooauthenticate를 사용 하는 사용자<p>**휴대폰** – 사용자 휴대폰 또는 인증 전화 tooauthenticate 사용<p>**보안 질문** – 사용 되는 사용자 보안 질문 tooauthenticate<p>**어떠한 조합의 (예: 암호 확인용 메일 + 휴대폰) 위에 hello** – 2 개의 게이트 정책이 지정 되 고 두 가지 방법이 사용 되는 사용자 tooauthentication hello를 표시 하는 경우에 발생가 암호 재설정 요청 합니다. |
| 결과 |**중단됨** – 사용자가 암호 재설정을 시작하지만 완료하지 않고 중간에서 중단됩니다.<p>**차단** – 사용자의 계정이 금지 toouse 암호 tooattempting toouse hello 암호 재설정 페이지 인해 재설정 되었습니다. 또는 너무 여러 번 24 시간 동안에서에서 단일 암호 재설정 게이트<p>**취소** – 사용자가 암호 재설정을 시작 했지만 hello 취소 단추 toocancel hello 세션 도중 클릭 한 다음 <p>**관리자에 연결할** – hello 암호 재설정 흐름 hello 사용자 hello 끝내 지 않고 "관리자에 게 문의" 링크를 클릭 합니다. 하므로, 사용자는 해결할 수 없는 자신의 세션 중에 문제가 발생 했습니다<p>**실패** – hello 사용자가 구성 된 toouse hello 기능 (예를 들어 라이선스, 누락 된 인증 정보, 암호 관리 되는 온-프레미스 없지만 쓰기 저장 해제 됨) 때문에 사용자가 수 tooreset 암호를 없습니다.<p>**성공함** - 암호가 재설정되었습니다. |
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
| Hello 필요한 인증 방법을 통과 하기 전에 사용자를 취소 했습니다. |Canceled |
| 사용자가 새 암호를 전송하기 전에 취소함 |Canceled |
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

## <a name="self-service-password-management-activity-types"></a>셀프 서비스 암호 관리 활동 유형

hello에 hello 활동 유형만 표시 **셀프 서비스 암호 관리** audit 이벤트 범주입니다.  각각에 대한 설명은 다음과 같습니다.

* [**셀프 서비스 암호 재설정에서 차단** ](#activity-type-blocked-from-self-service-password-reset) -사용자가 tooreset 암호를 나타냅니다. 특정 게이트를 사용 하거나 24 시간 동안의 총 5 개의 시간 전화 번호를 확인 합니다.
* [**암호 (셀프 서비스)를 변경** ](#activity-type-change-password-self-service) -사용자는 자발적 수행 하거나 강제로 적용 나타냅니다 (due tooexpiry) 암호를 변경 합니다.
* [**(관리자)가 암호 재설정** ](#activity-type-reset-password-by-admin) -관리자가 암호 재설정 hello Azure 포털에서에서 사용자를 대신해 서 수행을 나타냅니다.
* [**암호 재설정 (셀프 서비스)** ](#activity-type-reset-password-self-service) -사용자 hello에서 암호를 성공적으로 다시 나타냅니다 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com)합니다.
* [**셀프 서비스 암호 재설정 흐름 활동 진행률** ](#activity-type-self-serve-password-reset-flow-activity-progress) -hello 암호의 일부 프로세스를 다시 설정 하는 대로 각 특정 단계 (예: 특정 암호를 전달 인증 게이트 다시 설정)을 통해 진행 되는 사용자를 나타냅니다.
* [**사용자 계정 (셀프 서비스)를 잠금 해제** ](#activity-type-unlock-user-account-self-service) -사용자 잠금을 해제 했습니다. Active Directory 계정으로 hello에서 자신의 암호를 재설정 하지 않고 나타냅니다 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com) 를 사용 하 여 기능을 다시 설정 하지 않으면 hello AD 계정의 잠금을 해제 합니다.
* [**사용자 셀프 서비스 암호 재설정에 등록** ](#activity-type-user-registered-for-self-service-password-reset) -사용자가 모든 필요한 hello 정보 toobe 수 tooreset 등록 나타냅니다 hello에 따라 해당 암호는 현재 테 넌 트 암호 재설정 정책을 지정 합니다.

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
* **작업 자가** -hello 사용자가 자신의 암호를 변경 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **작업 대상** -hello 사용자가 자신의 암호를 변경 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ - 사용자가 자신의 암호를 성공적으로 변경했음을 나타냅니다.
  * _오류_ -사용자가 암호를 toochange 실패 했음을 나타냅니다. 클릭 하 여 hello 행 있습니다 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다.
* **활동 상태 실패 이유** - 
  * _FuzzyPolicyViolationInvalidPassword_ -hello 사용자 tooMicrosoft의 암호 검색 사용 금지 기능이 너무 일반적 또는 특히 취약 toobe 찾기 인해 자동으로 금지 된 암호를 선택 합니다.

### <a name="activity-type-reset-password-by-admin"></a>활동 유형: 암호 다시 설정(관리자)

hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 관리자가 암호 재설정 hello Azure 포털에서에서 사용자를 대신해 서 수행을 나타냅니다.
* **작업 자가** -hello 암호를 재설정 대신 다른 최종 사용자나 관리자가 관리자에 게 있습니다. 전역 관리자, 암호 관리자, 사용자 관리자 또는 기술 지원팀 관리자여야 합니다.
* **작업 대상** -hello 사용자 암호 다시 설정 되었습니다. 최종 사용자 또는 다른 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ - 관리자가 사용자의 암호를 성공적으로 다시 설정했음을 나타냅니다.
  * _오류_ -관리자가 사용자의 암호 toochange 실패 했음을 나타냅니다. 클릭 하 여 hello 행 있습니다 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다.

### <a name="activity-type-reset-password-self-service"></a>활동 유형: 암호 다시 설정(셀프 서비스)

hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 사용자 hello에서 암호를 성공적으로 다시 나타냅니다 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com)합니다.
* **작업 자가** -hello 사용자에 게 암호를 재설정 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **작업 대상** -hello 사용자에 게 암호를 재설정 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ - 사용자가 자신의 암호를 성공적으로 재설정했음을 나타냅니다.
  * _오류_ -사용자가 자신의 고유 암호 tooreset 실패 했음을 나타냅니다. 클릭 하 여 hello 행 있습니다 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다.
* **활동 상태 실패 이유** -
  * _FuzzyPolicyViolationInvalidPassword_ -admin 님 안녕하세요 tooMicrosoft의 암호 검색 사용 금지 기능이 너무 일반적 또는 특히 취약 toobe 찾기 인해 자동으로 금지 된 암호를 선택 합니다.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>활동 유형: 셀프 서비스 암호 다시 설정 흐름 활동 진행률

hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 사용자 진행 (예: 전달 특정 암호 재설정 인증 게이트) hello 암호의 일부 프로세스를 다시 설정 하는 대로 각 특정 단계를 나타냅니다.
* **작업 자가** -hello 암호의 일부를 수행한 hello 사용자 흐름을 다시 설정 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **작업 대상** -hello 암호의 일부를 수행한 hello 사용자 흐름을 다시 설정 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ -hello 암호 재설정 흐름의 특정 단계를 성공적으로 완료 하는 사용자를 나타냅니다.
  * _오류_ -hello 암호의 특정 단계를 다시 설정 실패 흐름을 나타냅니다. 클릭 하 여 hello 행 있습니다 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다.
* **허용되는 활동 상태 이유**
  * [모든 허용되는 다시 설정 활동 상태 이유](#allowed-values-for-details-column)에 대해서는 아래 표를 참조하세요.

### <a name="activity-type-unlock-user-account-self-service"></a>활동 유형: 사용자 계정 잠금 해제(셀프 서비스)

hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 사용자 잠금을 해제 했습니다. Active Directory 계정으로 hello에서 자신의 암호를 재설정 하지 않고 나타냅니다 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com) hello AD 계정을 사용 하 여 다시 설정 하지 않고 잠금 해제 기능입니다.
* **작업 자가** -hello 사용자가 자신의 암호를 재설정 하지 않고 자신의 계정 잠금 해제 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **작업 대상** -hello 사용자가 자신의 암호를 재설정 하지 않고 자신의 계정 잠금 해제 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ - 사용자가 자신의 계정을 성공적으로 잠금 해제했음을 나타냅니다.
  * _오류_ -사용자가 자신의 계정 toounlock 실패 했음을 나타냅니다. 클릭 하 여 hello 행 있습니다 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>활동 유형: 사용자가 셀프 서비스 암호 다시 설정 등록

hello 목록 다음이 작업을 자세히 설명 합니다.

* **활동 설명** – 사용자가 모든 필요한 hello 정보 toobe 수 tooreset 등록 나타냅니다 hello에 따라 해당 암호는 현재 테 넌 트 암호 재설정 정책을 지정 합니다. 
* **작업 자가** -hello 사용자에 게 암호 재설정에 등록 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **작업 대상** -hello 사용자에 게 암호 재설정에 등록 합니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ -암호 재설정 hello 현재 정책에 따라에 성공적으로 등록 된 사용자를 나타냅니다. 
  * _오류_ -암호 재설정을 위해 사용자 실패 tooregister 나타냅니다. 클릭 하 여 hello 행 있습니다 toosee hello **활동 상태 설명** 범주 toolearn 이유 hello 오류가 발생 하는 방법에 대 한 자세한 합니다. 참고-이 사용자를 의미 하지는 없습니다 tooreset 자신의 암호를 정당한 hello 등록 프로세스 완료 되지 않았습니다. (예: 전화 번호를 유효성이 검사 되지 않은), 올바른 사용자 계정에 확인 되지 않은 데이터가 있는 경우이 전화 번호를 확인 하지 않았으며, 경우에 여전히를 사용할 수 있습니다 tooreset 암호입니다. 자세한 내용은 [사용자가 등록하면 어떻게 되나요?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)를 참조하세요.

## <a name="next-steps"></a>다음 단계

링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [바로 가기 toouser 관리 감사 로그](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit) -tooyour 테 넌 트의 사용자 관리 감사 로그 직접 이동
* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법
* [**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자
* [**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.
* [**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? -Tooask 항상 필요한 tooquestions 답변
* [**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다
* [**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정
