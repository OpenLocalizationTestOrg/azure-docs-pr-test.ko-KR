---
title: "Azure MFA에 대 한 aaaAccess 및 사용 보고서 | Microsoft Docs"
description: "Toouse Azure Multi-factor Authentication 기능-보고서 hello 하는 방법을 설명 합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication에서 보고서
Azure Multi-Factor Authentication은 사용자 및 사용자의 조직에서 사용할 수 있는 다양한 보고서를 제공합니다. 이러한 보고서는 hello Multi-factor Authentication 관리 포털을 통해 액세스할 수 있습니다. hello 다음은 hello 사용할 수 있는 보고서의 목록입니다.

| 보고서 | 설명 |
|:--- |:--- |
| 사용 |hello 사용의 전반적인 사용량, 사용자 요약 및 사용자 세부 정보 표시 정보를 보고합니다. |
| 서버 상태 |이 보고서는 사용자 계정과 연결 된 Multi-factor Authentication 서버 hello 상태를 표시 합니다. |
| 차단된 사용자 기록 |이러한 보고서의 요청 tooblock hello 기록 표시 또는 사용자를 차단 해제 합니다. |
| 무시된 사용자 기록 |사용자의 전화 번호에 대 한 요청 toobypass Multi-factor Authentication의 hello 기록을 표시합니다. |
| 사기 행위 경고 |지정한 hello 날짜 범위 동안 제출 된 사기 행위 경고 기록을 표시 합니다. |
| Queued |처리 및 해당 상태에 대해 대기 중인 보고서가 나열되어 있습니다. Hello 보고서 완료 되 면 링크 toodownload 또는 보기 hello 보고서가 제공 됩니다. |

## <a name="view-reports"></a>보고서 보기
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 왼쪽에서 Active Directory를 선택 합니다.
3. 인증 공급자를 사용하는지 여부에 따라 이 두 옵션 중 하나를 따릅니다.
   * **옵션 1**: hello Multi-factor Auth 공급자 탭을 클릭 합니다. MFA 공급자를 선택 하 고 hello 클릭 **관리** hello 아래쪽 단추입니다.
   * **옵션 2**: 디렉터리 및 이동 toohello 선택 **구성** 탭 합니다. Hello multi-factor authentication 섹션에서 선택 **서비스 설정 관리**합니다. Hello MFA 서비스 설정 페이지의 맨 아래 hello에 hello Go toohello 위의 포털 링크를 클릭 합니다.
4. Azure Multi-factor Authentication 관리 포털 hello hello에서 원하는 보고서 hello 유형을 선택 **보고서를 볼** hello 왼쪽 탐색의에서 섹션입니다.

<center>![클라우드](./media/multi-factor-authentication-manage-reports/report.png)</center>


**추가 리소스**

* [사용자](end-user/multi-factor-authentication-end-user.md)
* [MSDN에서 Azure Multi-Factor Authentication](https://msdn.microsoft.com/library/azure/dn249471.aspx)
