---
title: "aaaAzure Active Directory Reporting 알림"
description: "어떻게 toouse hello 의심 스러운 로그인에 대 한 Azure Active Directory reporting 알림 기능입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a>Azure Active Directory Reporting 알림
## <a name="what-reports-generate-email-notifications"></a>어떤 보고서가 전자 메일 알림을 생성하나요?
이때 보고서 트리거 활동에에서 비정상적인 로그인을 hello만 전자 메일 알림입니다.

## <a name="what-is-an-irregular-sign-in"></a>"비정상적인 로그인"이란 무엇일까요?
비정상적인 로그인은 기계 학습 알고리즘을 결합 한 비정상적인 로그인 위치와 장치를 사용 하는 "이동 불가능" 상태의 hello 기준에 의해 식별 된 로그인입니다. 이 해커가이 계정을 사용 하 여 toosign 노력해 왔습니다 나타낼 수 있습니다.

## <a name="who-receives-hello-email-notifications"></a>Hello 전자 메일 알림을 받는 사람?
hello 메일이 tooall 전역 관리자에 게는 Active Directory Premium 라이선스가 할당 된 전송 됩니다. 제공 된다는 tooensure, 보냅니다 toohello 관리자 대체 전자 메일 주소로 합니다. 관리자가 포함 되어야 aad-alerts-noreply@mail.windowsazure.com 누락 되지 hello 전자 메일 수신 허용 목록에 있습니다.

## <a name="how-often-are-these-emails-sent"></a>이러한 전자 메일은 얼마나 자주 전송되나요?
지난 30 일 동안 hello에 10 개의 새 비정상적인 로그인 활동 발생 하거나 hello 마지막 전자 메일을 보낸 후 더 작은 경우 hello 메일이 전송 됩니다.

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a>Hello 전자 메일에 언급 된 hello 보고서에 액세스 하려면 어떻게 해야 합니까?
Hello 링크를 클릭할 때 hello Azure 클래식 포털 내에서 보고서 페이지 리디렉션된 toohello 됩니다. 순서로 tooaccess hello 보고서 toobe 모두 사용 해야 합니다.

* Azure 구독의 관리자 또는 공동 관리자
* Hello 디렉터리의 전역 관리자는 Active Directory Premium 라이선스가 할당 합니다. 자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.

## <a name="can-i-turn-off-these-emails"></a>이러한 전자 메일을 끌 수 있나요?
예, 알림 표시 하지 tooturn 관련 hello Azure 클래식 포털 내에서 tooanomalous 로그인을 클릭 **구성**를 선택한 후 **비활성화 된** hello에서 **알림**섹션.

## <a name="whats-next"></a>다음 단계
* 사용 가능한 보안, 감사 및 작업 보고서는 [Azure AD 보안, 감사 및 작업 보고서](active-directory-view-access-usage-reports.md) 확인
* [Azure Active Directory Premium 시작](active-directory-get-started-premium.md)
* [회사 브랜딩 tooyour 로그인 및 액세스 패널 페이지 추가](active-directory-add-company-branding.md)

