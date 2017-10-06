---
title: "Azure AD Connect Synchronization Service Manager 작업 | Microsoft Docs"
description: "Azure AD Connect에 대 한 hello 동기화 서비스 관리자의에서 작업 탭 hello를 이해 합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a>Hello 동기화 서비스 관리자가 작업 탭을 사용 하 여

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

작업 탭 hello hello 가장 최근 작업에서 hello 결과 보여 줍니다. 이 탭은 키 toounderstand 며 문제를 해결 합니다.

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a>Hello 작업 탭에 표시 하는 hello 정보 이해
hello 위쪽 절반 시간 순서에 따라 모든 실행을 보여 줍니다. 기본적으로 hello 작업 로그 정보를 유지 관리 hello에 대 한 지난 7 일 하지만 hello로이 설정을 변경할 수 있습니다 [스케줄러](active-directory-aadconnectsync-feature-scheduler.md)합니다. 성공 상태를 표시 하지 않는 모든 실행에 대 한 toolook을 원하는 합니다. Hello hello 머리글을 클릭 하 여 정렬을 변경할 수 있습니다.

hello **상태** 열이 hello 가장 중요 한 정보 및 실행에 대해 가장 심각한 문제를 hello 보여 줍니다. 간단히 요약 한 hello 가장 일반적인 상태 tooinvestigate 우선 순위 순서 대로 다음과 같습니다 (여기서 * 나타내는 여러 가지 가능한 오류 문자열)입니다.

| 가동 상태 | 주석 |
| --- | --- |
| stopped-* |hello 실행을 완료할 수 없습니다. 예를 들어 경우 hello 원격 시스템 다운 되어에 연결할 수 없습니다. |
| stopped-error-limit |5000개보다 많은 오류가 있습니다. 실행 하는 hello toohello 오류가 많이 인해 자동으로 중지 되었습니다. |
| completed-\*-errors |hello 실행을 완료 하지만 조사 해야 하는 오류 (미만 5000). |
| completed-\*-warnings |실행 하는 hello 완료 되었지만 일부 데이터가 예상 hello 상태에 있지 않습니다. 오류가 발생하는 경우 이 메시지는 일반적으로 증상일 뿐입니다. 오류를 해결할 때까지 경고를 조사하지 않습니다. |
| 성공 |문제가 없습니다. |

행을 선택 하면 hello 아래쪽의를 실행 하는 tooshow hello 세부 정보를 업데이트 합니다. toohello hello 아래쪽의 맨 왼쪽, 목록 라는 해야할 **단계 #**합니다. 이 목록은 각 도메인을 단계로 나타내는 포리스트에 여러 도메인이 있는 경우에만 표시됩니다. hello 도메인 이름은 hello 머리글 아래에서 찾을 수 있습니다 **파티션**합니다. 아래 **동기화 통계**, 처리 된 변경 내용 수 hello에 대 한 자세한 정보를 찾을 수 있습니다. Hello 링크 tooget hello 변경 개체의 목록을 클릭 수 있습니다. 오류가 있는 개체가 있으면 해당 오류는 **동기화 오류**아래에 표시됩니다.

자세한 내용은 [동기화되지 않는 개체 문제 해결](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
