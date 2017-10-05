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
ms.openlocfilehash: ba7b36e654aa0bf3b74d42a2b0ae96ae2a9b6241
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Azure AD 암호 관리에 대한 보고 옵션

배포 후에 여러 조직에서는 SSPR을 실제로 사용하는 방법 및 경우를 알아보고자 합니다. Azure AD는 준비된 보고서를 사용하여 질문에 대답하는 보고 기능을 제공하고 적절하게 허가받은 경우 사용자 지정 쿼리를 만들도록 할 수 있습니다.

[Azure Portal](https://portal.azure.com/)에 있는 보고서에서는 다음과 같은 질문에 대답할 수 있습니다.

> [!NOTE]
> 사용자는 [전역 관리자](active-directory-assign-admin-roles.md#assign-or-remove-administrator-roles)여야 하며 적어도 한 번 감사 로그를 방문하여 조직을 대신하여 이 데이터를 수집하기 위해 옵트인해야 합니다. 이렇게 할 때까지는 조직의 데이터가 수집되지 않습니다.

* 얼마나 많은 사람들이 암호 재설정을 위해 등록합니까?
* 누가 암호 재설정을 위해 등록합니까?
* 사람들이 등록하는 데이터는 무엇입니까?
* 지난 7일 동안 얼마나 많은 사람들이 자신의 암호를 재설정했습니까?
* 사용자나 관리자가 자신의 암호를 재설정하는 가장 일반적인 방법은 무엇입니까?
* 암호 재설정을 시도할 때 사용자나 관리자가 직면하는 공통적인 문제는 무엇입니까?
* 어느 관리자가 자신의 암호를 자주 재설정합니까?
* 암호 재설정에 대해 의심스러운 활동이 있습니까?

## <a name="how-to-view-password-management-reports-in-the-azure-portal"></a>Azure Portal에서 암호 관리 보고서를 보는 방법

Azure Portal 환경에서 암호 재설정 및 암호 재설정 등록 활동을 볼 수 있는 향상된 방법이 있습니다.  아래 단계에 따라 암호 재설정 및 암호 재설정 등록 이벤트를 확인합니다.

1. [**portal.azure.com**](https://portal.azure.com)으로 이동합니다.
2. 기본 Azure Portal의 왼쪽 탐색 창에서 **추가 서비스** 메뉴를 클릭합니다.
3. 서비스 목록에서 **Azure Active Directory**를 검색하고 선택합니다.
4. Azure Active Directory 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.
5. [사용자 및 그룹] 탐색 메뉴에서 **감사 로그** 탐색 항목을 클릭합니다. 그러면 디렉터리의 모든 사용자에 대해 발생하는 감사 이벤트가 모두 표시됩니다. 이 보기를 필터링하여 암호 관련 이벤트를 모두 볼 수도 있습니다.
6. 이 보기를 암호 재설정 관련 이벤트로만 필터링하려면 블레이드 위쪽의 **필터** 단추를 클릭합니다.
7. **필터** 메뉴에서 **범주** 드롭다운을 선택하고, **셀프 서비스 암호 관리** 범주 유형으로 변경합니다.
8. 필요에 따라 관심 있는 특정 **활동**을 선택하여 목록을 추가로 필터링합니다.

## <a name="how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api"></a>Azure AD 보고서 및 이벤트 API에서 암호 관리 이벤트를 검색하는 방법

Azure AD 보고서 및 이벤트 API는 암호 재설정 및 암호 재설정 등록 보고서에 포함된 모든 정보를 검색하도록 지원하고 있습니다. 이 API를 사용하면 개별 암호 재설정 및 암호 재설정 등록 이벤트를 다운로드하여 선택한 보고 기술과 통합할 수 있습니다.

### <a name="how-to-get-started-with-the-reporting-api"></a>보고 API를 시작하는 방법

이 데이터에 액세스하려면 작은 앱 또는 스크립트를 작성하여 서버에서 검색해야 합니다. [Azure AD Reporting API를 시작하는 방법을 알아봅니다](active-directory-reporting-api-getting-started.md)

작동하는 스크립트가 있으면 다음으로 시나리오에 맞게 검색할 수 있는 암호 재설정 및 등록 이벤트를 검사하려 합니다.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): 암호 재설정 이벤트에 대해 사용 가능한 열을 나열합니다.
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): 암호 재설정 등록 이벤트에 대해 사용 가능한 열을 나열합니다.

### <a name="reporting-api-data-retrieval-limitations"></a>보고 API 데이터 검색 제한

현재 Azure AD 보고서 및 이벤트 API는 **지난 30일 동안** [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) 및 [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) 유형의 최대 **75,000개의 개별 이벤트**를 검색합니다.

이 창에서 미치지 않는 데이터를 검색하거나 저장해야 하는 경우 외부 데이터베이스에서 이 데이터를 유지하고 API를 사용하여 그 결과인 델타를 쿼리하는 것이 좋습니다. 조직에서 SSPR을 사용하기 시작할 때 이 데이터를 검색하고 외부에서 유지한 다음이 시점에서 델타를 계속 추적하는 것이 좋습니다입니다.

## <a name="how-to-download-password-reset-registration-events-quickly-with-powershell"></a>PowerShell을 사용하여 암호 다시 설정 등록 이벤트를 빠르게 다운로드하는 방법

Azure AD 보고서 및 이벤트 API를 직접 사용하는 것 외에도 디렉터리의 최근 등록 이벤트에 다음 PowerShell 스크립트를 사용할 수 있습니다. 이 PowerShell 스크립트는 최근 등록한 사람을 확인하거나 암호 다시 설정 롤아웃이 예상대로 수행되도록 하려는 경우에 유용합니다.

* [Azure AD SSPR 등록 활동 PowerShell 스크립트](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

### <a name="description-of-report-columns-in-azure-portal"></a>Azure Portal의 보고서 열 설명

다음 목록에서는 각 보고서의 열에 대해 자세히 설명합니다.

* **사용자** – 암호 재설정 등록 작업을 시도한 사용자입니다.
* **역할** – 디렉터리에서 사용자의 역할입니다.
* **날짜 및 시간** – 시도한 날짜 및 시간입니다.
* **등록된 데이터** – 암호 재설정 등록 중 사용자가 제공한 인증 데이터입니다.

### <a name="description-of-report-values-in-azure-portal"></a>Azure Portal의 보고서 값 설명

다음 테이블에서 각 열에 대해 허용되는 다른 값을 설명합니다.

| 열 | 허용되는 값과 해당 의미 |
| --- | --- |
| 등록된 데이터 |**대체 전자 메일** – 인증하는 데 사용자가 사용한 대체 전자 메일 또는 인증 전자 메일<p><p>**사무실 전화** – 인증하는 데 사용자가 사용한 사무실 전화<p>**휴대폰** – 인증하는 데 사용자가 사용한 휴대폰 또는 인증 전화<p>**보안 질문** – 인증하는 데 사용자가 사용한 보안 질문<p>**위의 조합(예: 대체 전자 메일 + 휴대폰)** – 2개의 게이트 정책이 지정되고 암호 재설정 요청을 인증하는 데 사용자가 사용한 두 메서드를 표시합니다. |

## <a name="view-password-reset-activity-in-the-classic-portal"></a>클래식 포털에서 암호 다시 설정 활동 보기

이 보고서는 조직 내에서 발생한 모든 암호 재설정 시도를 보여줍니다.

* **최대 시간 범위**: 30일
* **최대 행 수**: 75,000개
* **다운로드 가능**: 예, CSV 파일을 통해

### <a name="description-of-report-columns-in-azure-classic-portal"></a>Azure 클래식 포털의 보고서 열 설명

다음 목록에서는 각 보고서의 열에 대해 자세히 설명합니다.

1. **사용자** – 암호 재설정 작업을 시도한 사용자(사용자가 암호를 재설정할 때 제공되는 사용자 ID 필드에 따라).
2. **역할** – 디렉터리에서 사용자의 역할입니다.
3. **날짜 및 시간** – 시도한 날짜 및 시간입니다.
4. **사용된 메서드** –이 재설정 작업에 사용자가 사용한 인증 메서드입니다.
5. **결과** – 암호 재설정 작업의 결과입니다.
6. **세부 정보** – 암호 재설정 결과로 왜 이 값이 생성되었는지에 대한 자세한 설명입니다.  또한 예기치 않은 오류를 해결하기 위해 수행할 수 있는 완화 단계를 포함합니다.

### <a name="description-of-report-values-in-azure-classic-portal"></a>Azure 클래식 포털의 보고서 값 설명

다음 테이블에서 각 열에 대해 허용되는 다른 값을 설명합니다.

| 열 | 허용되는 값과 해당 의미 |
| --- | --- |
| 사용된 메서드 |**대체 전자 메일** – 인증하는 데 사용자가 사용한 대체 전자 메일 또는 인증 전자 메일<p>**사무실 전화** – 인증하는 데 사용자가 사용한 사무실 전화<p>**휴대폰** – 인증하는 데 사용자가 사용한 휴대폰 또는 인증 전화<p>**보안 질문** – 인증하는 데 사용자가 사용한 보안 질문<p>**위의 조합(예: 대체 전자 메일 + 휴대폰)** – 2개의 게이트 정책이 지정되고 암호 재설정 요청을 인증하는 데 사용자가 사용한 두 메서드를 표시합니다. |
| 결과 |**중단됨** – 사용자가 암호 재설정을 시작하지만 완료하지 않고 중간에서 중단됩니다.<p>**차단됨** -사용자의 계정이 암호 재설정 페이지를 사용하거나 24시간 동안 너무 여러 번 단일 암호 재설정 게이트를 사용하여 암호를 재설정할 수 없습니다.<p>**취소됨** – 사용자가 암호 재설정을 시작했지만 취소 단추를 클릭하여 도중 세션을 취소했습니다. <p>**연결된 관리자** – 세션 중 사용자가 해결할 수 없는 문제가 생겨 사용자가 암호 재설정 작업을 완료하는 대신 “관리자에게 문의” 링크를 클릭했습니다.<p>**실패함** – 사용자가 기능을 사용하도록 구성되지 않았기 때문에 암호를 재설정할 수 없습니다(라이선스 없음, 누락된 인증 정보, 암호 관리 온-프레미스지만 쓰기 저장이 꺼져 있음).<p>**성공함** - 암호가 재설정되었습니다. |
| 세부 정보 |아래 테이블을 참조하세요. |

### <a name="allowed-values-for-details-column"></a>세부 정보 열에 대해 허용되는 값

다음은 암호 재설정 활동 보고서를 사용하는 경우 예상할 수 있는 결과 형식 목록입니다.

| 세부 정보 | 결과 형식 |
| --- | --- |
| 사용자가 전자 메일 확인 옵션을 완료한 후 중단함 |Abandoned |
| 사용자가 모바일 SMS 확인 옵션을 완료한 후 중단함 |Abandoned |
| 사용자가 모바일 음성 통화 확인 옵션을 완료한 후 중단함 |Abandoned |
| 사용자가 사무실 음성 통화 확인 옵션을 완료한 후 중단함 |Abandoned |
| 사용자가 보안 질문 옵션을 완료한 후 중단함 |Abandoned |
| 사용자가 사용자 ID를 입력한 후 중단함 |Abandoned |
| 사용자가 전자 메일 확인 옵션을 시작한 후 중단함 |Abandoned |
| 사용자가 모바일 SMS 확인 옵션을 시작한 후 중단함 |Abandoned |
| 사용자가 모바일 음성 통화 확인 옵션을 시작한 후 중단함 |Abandoned |
| 사용자가 사무실 음성 통화 확인 옵션을 시작한 후 중단함 |Abandoned |
| 사용자가 보안 질문 옵션을 시작한 후 중단함 |Abandoned |
| 사용자가 새 암호를 선택하기 전에 중단함 |Abandoned |
| 사용자가 새 암호를 선택하는 중에 중단함 |Abandoned |
| 사용자가 너무 많은 잘못된 SMS 확인 코드를 입력하여 24시간 동안 차단됨 |Blocked |
| 사용자가 너무 많이 모바일 음성 인증을 시도하여 24시간 동안 차단됨 |Blocked |
| 사용자가 너무 많이 사무실 음성 인증을 시도하여 24시간 동안 차단됨 |Blocked |
| 사용자가 너무 많이 보안 질문에 답변을 시도하여 24시간 동안 차단됨 |Blocked |
| 사용자가 너무 많이 전화번호 확인을 시도하여 24시간 동안 차단됨 |Blocked |
| 사용자가 필수 인증 방법을 전달하기 전에 취소함 |Canceled |
| 사용자가 새 암호를 전송하기 전에 취소함 |Canceled |
| 사용자 전자 메일 확인 옵션을 시도한 후 관리자에 문의함 |Contacted admin |
| 사용자가 모바일 SMS 확인 옵션을 시도한 후 관리자에 문의함 |Contacted admin |
| 사용자가 모바일 음성 통화 확인 옵션을 시도한 후 관리자에 문의함 |Contacted admin |
| 사용자가 사무실 음성 통화 확인 옵션을 시도한 후 관리자에 문의함 |Contacted admin |
| 사용자가 보안 질문 확인 옵션을 시도한 후 관리자에 문의함 |Contacted admin |
| 이 사용자에 대한 암호 재설정이 사용되지 않습니다. 이를 해결하려면 구성 탭에서 암호 재설정 사용합니다. |Failed |
| 사용자에게 라이선스가 없습니다. 이를 해결하기 위해 사용자에게 라이선스를 추가할 수 있습니다. |Failed |
| 사용자가 쿠키를 사용하지 않고 장치에서 다시 설정하려고 시도함 |Failed |
| 사용자의 계정에 정의된 인증 메서드가 부족합니다. 이를 해결하려면 인증 정보를 추가합니다. |Failed |
| 사용자의 암호는 관리 대상 온-프레미스입니다. 이를 해결하려면 암호 쓰기 저장을 사용하도록 설정할 수 있습니다. |Failed |
| 온-프레미스 암호 재설정 서비스에 접근할 수 없습니다. 동기화 컴퓨터의 이벤트 로그를 확인합니다. |Failed |
| 사용자의 온-프레미스 암호를 재설정하는 중에 문제가 발생했습니다. 동기화 컴퓨터의 이벤트 로그를 확인합니다. |Failed |
| 이 사용자는 암호 재설정 사용자 그룹의 멤버가 아닙니다. 이를 해결하려면 해당 그룹에 이 사용자를 추가합니다. |Failed |
| 암호 재설정은 이 테넌트에 대해 완전히 비활성화되었습니다. 이를 해결하려면 [여기](http://aka.ms/ssprtroubleshoot) 를 참조하세요. |Failed |
| 사용자가 성공적으로 암호를 재설정함 |Succeeded |

## <a name="self-service-password-management-activity-types"></a>셀프 서비스 암호 관리 활동 유형

다음 활동 유형은 **셀프 서비스 암호 관리** 감사 이벤트 범주에 표시됩니다.  각각에 대한 설명은 다음과 같습니다.

* [**셀프 서비스 암호 다시 설정에서 차단**](#activity-type-blocked-from-self-service-password-reset) - 사용자가 암호를 다시 설정하거나 특정 게이트를 사용하거나 24시간 이내에 총 6회 이상 전화 번호의 유효성을 검사하려고 했음을 나타냅니다.
* [**암호 변경(셀프 서비스)**](#activity-type-change-password-self-service) - 사용자가 자발적으로 또는 강제로(만료로 인해) 암호 변경을 수행했음을 나타냅니다.
* [**암호 재설정(관리자)**](#activity-type-reset-password-by-admin) - 관리자가 Azure Portal에서 사용자를 대신하여 암호를 재설정했음을 나타냅니다.
* [**암호 재설정(셀프 서비스)**](#activity-type-reset-password-self-service) - 사용자가 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com)에서 자신의 암호를 성공적으로 재설정했음을 나타냅니다.
* [**셀프 서비스 암호 재설정 흐름 활동 진행률**](#activity-type-self-serve-password-reset-flow-activity-progress) - 암호 재설정 프로세스의 일부로 사용자가 진행하는 각각의 특정 단계(예: 특정 암호 재설정 인증 게이트 전달)를 나타냅니다.
* [**사용자 계정 잠금 해제(셀프 서비스)**](#activity-type-unlock-user-account-self-service) - 사용자가 재설정 기능 없이 AD 계정 잠금 해제를 사용하여 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com)에서 자신의 암호를 재설정하지 않고 Active Directory 계정을 성공적으로 잠금 해제했음을 나타냅니다.
* [**사용자가 셀프 서비스 암호 재설정 등록**](#activity-type-user-registered-for-self-service-password-reset) - 사용자가 현재 지정된 테넌트 암호 재설정 정책에 따라 자신의 암호를 재설정하는 데 필요한 모든 정보를 등록했음을 나타냅니다.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>활동 유형: 셀프 서비스 암호 다시 설정에서 차단

다음 목록에서는 이 활동에 대해 자세히 설명합니다.

* **활동 설명** – 사용자가 암호를 다시 설정하거나 특정 게이트를 사용하거나 24시간 이내에 총 6회 이상 전화 번호의 유효성을 검사하려고 했음을 나타냅니다.
* **활동 행위자** - 추가 다시 설정 작업을 수행할 수 없도록 제한된 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **활동 대상** - 추가 다시 설정 작업을 수행할 수 없도록 제한된 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ - 사용자가 추가 다시 설정을 수행하거나 추가 인증 방법을 시도하거나 다음 24시간 동안 전화 번호의 유효성을 추가로 검사할 수 없도록 제한되었음을 나타냅니다.
* **활동 상태 실패 이유** - 해당 없음

### <a name="activity-type-change-password-self-service"></a>활동 유형: 암호 변경(셀프 서비스)

다음 목록에서는 이 활동에 대해 자세히 설명합니다.

* **활동 설명** – 사용자가 자발적으로 또는 강제로(만료로 인해) 암호 변경을 수행했음을 나타냅니다.
* **활동 행위자** - 자신의 암호를 변경한 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **활동 대상** - 자신의 암호를 변경한 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ - 사용자가 자신의 암호를 성공적으로 변경했음을 나타냅니다.
  * _실패_ - 사용자가 자신의 암호를 변경하지 못했음을 나타냅니다. 행을 클릭하면 **활동 상태 이유** 범주가 표시되어 실패한 원인에 대해 자세히 알아볼 수 있습니다.
* **활동 상태 실패 이유** - 
  * _FuzzyPolicyViolationInvalidPassword_ - 사용자가 Microsoft의 차단 암호 검색 기능으로 인해 너무 흔하거나 특히 약한 것으로 식별되어 자동으로 차단되는 암호를 선택했습니다.

### <a name="activity-type-reset-password-by-admin"></a>활동 유형: 암호 다시 설정(관리자)

다음 목록에서는 이 활동에 대해 자세히 설명합니다.

* **활동 설명** – 관리자가 Azure Portal에서 사용자를 대신하여 암호를 재설정했음을 나타냅니다.
* **활동 행위자** - 다른 최종 사용자 또는 관리자를 대신하여 암호를 재설정한 관리자입니다. 전역 관리자, 암호 관리자, 사용자 관리자 또는 기술 지원팀 관리자여야 합니다.
* **활동 대상** - 자신의 암호를 다시 설정한 사용자입니다. 최종 사용자 또는 다른 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ - 관리자가 사용자의 암호를 성공적으로 다시 설정했음을 나타냅니다.
  * _실패_ - 관리자가 사용자의 암호를 변경하지 못했음을 나타냅니다. 행을 클릭하면 **활동 상태 이유** 범주가 표시되어 실패한 원인에 대해 자세히 알아볼 수 있습니다.

### <a name="activity-type-reset-password-self-service"></a>활동 유형: 암호 다시 설정(셀프 서비스)

다음 목록에서는 이 활동에 대해 자세히 설명합니다.

* **활동 설명** – 사용자가 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com)에서 자신의 암호를 성공적으로 재설정했음을 나타냅니다.
* **활동 행위자** - 자신의 암호를 재설정한 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **활동 대상** - 자신의 암호를 재설정한 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ - 사용자가 자신의 암호를 성공적으로 재설정했음을 나타냅니다.
  * _실패_ - 사용자가 자신의 암호를 재설정하는 데 실패했음을 나타냅니다. 행을 클릭하면 **활동 상태 이유** 범주가 표시되어 실패한 원인에 대해 자세히 알아볼 수 있습니다.
* **활동 상태 실패 이유** -
  * _FuzzyPolicyViolationInvalidPassword_ - 관리자가 Microsoft의 차단 암호 검색 기능으로 인해 너무 흔하거나 특히 약한 것으로 식별되어 자동으로 차단되는 암호를 선택했습니다.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>활동 유형: 셀프 서비스 암호 다시 설정 흐름 활동 진행률

다음 목록에서는 이 활동에 대해 자세히 설명합니다.

* **활동 설명** – 암호 다시 설정 프로세스의 일부로 사용자가 진행하는 각각의 특정 단계(예: 특정 암호 다시 설정 인증 게이트 전달)를 나타냅니다.
* **활동 행위자** - 암호 다시 설정 흐름의 일부를 수행한 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **활동 대상** - 암호 다시 설정 흐름의 일부를 수행한 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ - 사용자가 암호 다시 설정 흐름의 특정 단계를 성공적으로 완료했음을 나타냅니다.
  * _실패_ - 암호 다시 설정 흐름의 특정 단계가 실패했음을 나타냅니다. 행을 클릭하면 **활동 상태 이유** 범주가 표시되어 실패한 원인에 대해 자세히 알아볼 수 있습니다.
* **허용되는 활동 상태 이유**
  * [모든 허용되는 다시 설정 활동 상태 이유](#allowed-values-for-details-column)에 대해서는 아래 표를 참조하세요.

### <a name="activity-type-unlock-user-account-self-service"></a>활동 유형: 사용자 계정 잠금 해제(셀프 서비스)

다음 목록에서는 이 활동에 대해 자세히 설명합니다.

* **활동 설명** – 사용자가 재설정 기능 없이 AD 계정 잠금 해제를 사용하여 [Azure AD 암호 재설정 포털](https://passwordreset.microsoftonline.com)에서 자신의 암호를 재설정하지 않고 Active Directory 계정을 성공적으로 잠금 해제했음을 나타냅니다.
* **활동 행위자** - 자신의 암호를 재설정하지 않고 계정을 잠금 해제한 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **활동 대상** - 자신의 암호를 재설정하지 않고 계정을 잠금 해제한 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ - 사용자가 자신의 계정을 성공적으로 잠금 해제했음을 나타냅니다.
  * _실패_ - 사용자가 자신의 계정을 잠금 해제하지 못했음을 나타냅니다. 행을 클릭하면 **활동 상태 이유** 범주가 표시되어 실패한 원인에 대해 자세히 알아볼 수 있습니다.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>활동 유형: 사용자가 셀프 서비스 암호 다시 설정 등록

다음 목록에서는 이 활동에 대해 자세히 설명합니다.

* **활동 설명** – 사용자가 현재 지정된 테넌트 암호 재설정 정책에 따라 자신의 암호를 재설정하는 데 필요한 모든 정보를 등록했음을 나타냅니다. 
* **활동 행위자** - 암호 다시 설정을 등록한 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **활동 대상** - 암호 다시 설정을 등록한 사용자입니다. 최종 사용자 또는 관리자일 수 있습니다.
* **허용되는 활동 상태**
  * _성공_ - 사용자가 현재 정책에 따라 암호 재설정에 성공적으로 등록했음을 나타냅니다. 
  * _실패_ - 사용자가 암호 다시 설정을 등록하지 못했음을 나타냅니다. 행을 클릭하면 **활동 상태 이유** 범주가 표시되어 실패한 원인에 대해 자세히 알아볼 수 있습니다. 참고 - 사용자가 자신의 암호를 재설정할 수 없다는 것이 아니라 등록 프로세스를 완료하지 못한 것입니다. 올바른 계정에 확인되지 않은 데이터(예: 유효성이 검사되지 않은 전화 번호)가 있는 경우 이 전화 번호를 확인하지 않아도 해당 계정을 계속 사용하여 암호를 다시 설정할 수 있습니다. 자세한 내용은 [사용자가 등록하면 어떻게 되나요?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)를 참조하세요.

## <a name="next-steps"></a>다음 단계

다음 링크는 Azure AD를 사용한 암호 재설정에 대한 추가 정보를 제공합니다.

* [사용자 관리 감사 로그로 바로 가기](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit) - 테넌트의 사용자 관리 감사 로그로 직접 이동합니다.
* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터**](active-directory-passwords-data.md) - 암호 관리에 필요한 데이터 및 사용 방식을 이해
* [**롤아웃**](active-directory-passwords-best-practices.md) - 여기서 제공하는 지침을 사용하여 배포 계획을 세우고 사용자에게 SSPR 배포
* [**사용자 지정**](active-directory-passwords-customize.md) - 회사 SSPR 경험의 모양과 느낌을 사용자 지정.
* [**기술 심층 분석**](active-directory-passwords-how-it-works.md) - 작동 방식을 이해하기 위해 심층 분석
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? - 많은 분들이 항상 묻는 질문에 대한 답변입니다.
* [**문제 해결**](active-directory-passwords-troubleshoot.md) - SSPR의 일반적인 문제 해결 방법 알아보기
* [**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정
