---
title: "aaaAzure Active Directory 보고서 대기 시간이 | Microsoft Docs"
description: "Azure 포털에서 tooshow 이벤트를 보고 하는 데 걸리는 시간의 hello 크기에 대 한 자세한 내용은"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a>Azure Active Directory 보고 대기 시간

와 [보고](active-directory-preview-explainer.md) hello Azure Active Directory 환경을 어떻게 진행 되는 toodetermine 필요한 모든 hello 정보를 가져옵니다. hello Azure 포털에서에서 위로 데이터 tooshow 대기 시간 이라고 보고 하는 데 걸리는 시간 hello 크기입니다. 

이 항목에서는 hello Azure 포털의에서 모든 보고 범주 hello에 대 한 hello 대기 시간 정보를 나열 합니다. 


## <a name="activity-reports"></a>작업 보고서

활동 보고에는 다음 두 가지 영역이 있습니다.

- **로그인 활동** – 관리 되는 응용 프로그램 및 사용자 로그인 활동의 hello 사용에 대 한 정보
- **감사 로그** - 사용자 및 그룹 관리, 관리되는 응용 프로그램 및 디렉터리 활동에 대한 시스템 활동 정보

다음 표에서 hello 활동 보고서에 대 한 hello 대기 시간 정보를 나열 합니다.

| 보고서 | 최소 | 평균 | 최대 |
| :-- | --- | --- | --- |
| 감사 로그             | 30분  | 45분 | 1시간     |
| 로그인               | 15분  | 15분 | 2시간*   |

>[!NOTE]
> 레거시 office 응용 프로그램에서 가져온 일부 로그인 활동 데이터를 보고 데이터 tooshow hello에 대 한 too8 시간 걸릴 수 있습니다. 


## <a name="security-reports"></a>보안 보고서

보안 보고에는 다음 두 가지 영역이 있습니다.

- **위험한 로그인** -위험한 로그인이 사용자 계정의 hello 정당한 소유자가 아닌 사용자에 의해 수행 된 로그인 시도에 대 한 표시기입니다. 
- **위험 플래그가 지정된 사용자** - 위험한 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다. 

다음 표에서 hello 보안 보고서에 대 한 hello 대기 시간 정보를 나열 합니다.

| 보고서 | 최소 | 평균 | 최대 |
| :-- | --- | --- | --- |
| 위험에 노출된 사용자          | 5분   | 15분  | 2시간  |
| 위험한 로그인         | 5분   | 15분  | 2시간  |

## <a name="risk-events"></a>위험 이벤트

Azure Active Directory 적응 컴퓨터 학습 알고리즘 및 추론 toodetect 의심 스러운 동작을 관련된 tooyour 사용자 계정을 사용 합니다. 검색된 각 의심스러운 동작은 위험 이벤트라는 레코드에 저장됩니다.

다음 표에서 hello 위험 이벤트에 대 한 hello 대기 시간 정보를 나열 합니다.

| 보고서 | 최소 | 평균 | 최대 |
| :-- | --- | --- | --- |
| 익명 IP 주소에서 로그인 |5분 |15분 |2시간 |
| 알 수 없는 위치에서 로그인 |5분 |15분 |2시간 |
| 자격 증명이 손실된 사용자 |2시간 |4시간 |8시간 |
| 이동 불가능 tooatypical 위치 |5분 |1시간 |8시간  |
| 감염된 장치에서 로그인 |2시간 |4시간 |8시간  |
| 의심스러운 작업이 있는 IP 주소에서 로그인 |2시간 |4시간 |8시간  |



## <a name="next-steps"></a>다음 단계

Hello Azure 포털에서에서 hello 활동 보고서에 대 한 자세한 tooknow, 참조:

- [Hello Azure Active Directory 포털의 로그인 활동 보고서](active-directory-reporting-activity-sign-ins.md)
- [감사 hello Azure Active Directory 포털에서 활동 보고서](active-directory-reporting-activity-audit-logs.md)

Hello Azure 포털에서에서 hello 보안 보고서에 대 한 자세한 tooknow, 참조:

- [Hello Azure Active Directory 포털에서 위험 보안 보고서에 있는 사용자](active-directory-reporting-security-user-at-risk.md)
- [Hello Azure Active Directory 포털에서 위험한 로그인 보고서](active-directory-reporting-security-risky-sign-ins.md)

Tooknow 위험 이벤트에 대 한 자세한 참조 [Azure Active Directory 위험 이벤트](active-directory-reporting-risk-events.md)합니다.
