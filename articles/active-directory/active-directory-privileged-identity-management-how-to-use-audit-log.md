---
title: "Azure AD Privileged Identity Management에서 aaaHow toouse hello 감사 로그 | Microsoft Docs"
description: "Toouse hello 감사 hello Azure Privileged Identity Management 확장에 로그인 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a>PIM의 hello 감사 로그를 사용 하 여
지정 된 기간 내에서 모든 hello 사용자 할당 및 활성화 hello Privileged Identity Management (PIM) 감사 로그 toosee를 사용할 수 있습니다. 테 넌 트 관리자, 최종 사용자 및 동기화 작업을 포함 하 여 활동의 toosee hello 완전 한 감사 내역을 원하는 경우에 hello을 사용할 수 있습니다 [Azure Active Directory 액세스 및 사용 보고서.](active-directory-view-access-usage-reports.md)

## <a name="navigate-toohello-audit-log"></a>Toohello 감사 로그를 이동 합니다.
Hello에서 [Azure 포털](https://portal.azure.com) 대시보드, 선택 hello **Azure AD Privileged Identity Management** 응용 프로그램입니다. 여기에서 클릭 하 여 hello 감사 로그에 액세스 **권한 있는 역할을 관리할** > **감사 기록** hello PIM 대시보드에.

## <a name="hello-audit-log-graph"></a>hello 감사 로그 그래프
선 그래프의 hello 감사 로그 tooview hello 총 활성화 수, 하루에 최대 활성화 및 하루 평균 정품 인증을 사용할 수 있습니다.  또한 hello 감사 기록에 역할이 둘 이상 있는 경우 역할별 hello 데이터 필터링 할 수 있습니다.

사용 하 여 hello **시간**, **동작**, 및 **역할** 단추 toosort hello 로그 합니다.

## <a name="hello-audit-log-list"></a>hello 감사 로그 목록
hello hello 감사 로그 목록에 열이 됩니다.

* **요청자에 게** -hello 요청한 사용자에 게 역할 활성화 hello 또는 변경 합니다.  "Azure 시스템" hello 값을 사용 하는 경우 자세한 내용은 hello Azure 감사 로그를 확인 합니다.
* **사용자** -hello 사용자를 활성화 하거나 tooa 역할을 지정 합니다.
* **역할** -hello 역할 할당 또는 hello 사용자가 활성화 합니다.
* **동작** -hello 요청자에 의해 수행 된 hello 작업 합니다. 여기에는 할당, 할당 해제, 활성화 또는 비활성화가 포함될 수 있습니다.
* **시간** -hello 동작이 발생 한 경우.
* **추론** -텍스트 활성화 하는 동안 hello 이유 필드에 입력 된 경우에 여기 표시 됩니다.
* **만료** - 역할의 활성화에만 관련이 있습니다.

## <a name="filter-hello-audit-log"></a>Hello 감사 로그를 필터링 합니다.
Hello를 클릭 하 여 hello 감사 로그에 표시 되는 hello 정보를 필터링 할 수 있습니다 **필터** 단추입니다.  hello **업데이트 차트 매개 변수 블레이드** 표시 됩니다.

Hello 필터를 설정한 후 클릭 **업데이트** hello 로그에서 toofilter hello 데이터입니다.  Hello 데이터가 바로 표시 되지 않으면, hello 페이지를 새로 고칩니다.

### <a name="change-hello-date-range"></a>Hello 날짜 범위를 변경 합니다.
사용 하 여 hello **오늘**, **지난 주**, **지난 달**, 또는 **사용자 지정** hello 감사 로그의 toochange hello 시간 범위는 단추입니다.

Hello를 선택 하는 경우 **사용자 지정** 단추를 제공 됩니다는 **에서** 날짜 필드와 **를** 날짜 필드 toospecify hello 로그에 대 한 날짜 범위입니다.  MM/DD/YYYY 형식으로 hello 날짜를 입력 하거나 hello 클릭 **달력** 아이콘 hello 날짜는 달력에서 선택 합니다.

### <a name="change-hello-roles-included-in-hello-log"></a>Hello 로그에 포함 된 hello 역할 변경
선택 하거나 선택 취소할 hello **역할** 로그 hello에서 다음 tooeach 역할 tooinclude 확인란을 선택 하거나 제외 합니다.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

