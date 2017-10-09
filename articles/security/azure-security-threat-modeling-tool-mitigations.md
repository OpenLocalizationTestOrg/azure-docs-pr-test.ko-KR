---
title: "-Microsoft 위협 모델링 도구-aaaMitigations Azure | Microsoft Docs"
description: "Hello Microsoft 위협 모델링 도구 강조 표시 가능한 해결 방법 toohello 노출 가장에 대 한 완화 페이지 위협 요소를 생성 합니다."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 000c0980d976b09fc9287e582e3776efaf7e390c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-mitigations"></a>Microsoft 위협 모델링 도구 해결 방법

hello 위협 모델링 도구에는 hello Microsoft SDL Security Development Lifecycle ()의 핵심 요소입니다. 소프트웨어를 통해 tooidentify 만드는 일 및 상대적으로 간편 하 고 비용 효율적인 tooresolve 있을 때 잠재적 보안 문제를 조기에 완화 합니다. 결과적으로, 개발의 hello 총 비용이 크게 감소합니다. 또한 hello 도구를 보다 쉽게 위협 모델링에 대 한 모든 개발자가 작성 및 위협 모델 분석에 명확한 지침을 제공 하 여을 염두에 비보안 전문가 함께 설계 합니다.

Hello 방문  **[위협 모델링 도구](./azure-security-threat-modeling-tool.md)**  tooget 오늘 시작!

## <a name="mitigation-categories"></a>해결 방법 범주

hello 위협 모델링 도구 완화 toohello hello 다음 구성 된 웹 응용 프로그램 보안 프레임에 따라 분류 됩니다.

| Category | 설명 |
| -------- | ----------- |
| **[감사 및 로깅](./azure-security-threat-modeling-tool-auditing-and-logging.md)** | 누가 언제 무엇을 했나요? 감사 및 로깅 기능이 toohow 응용 프로그램 레코드 보안 관련 이벤트를 참조 |
| **[인증](./azure-security-threat-modeling-tool-authentication.md)** | 당신은 누구인가요? 인증은 hello 프로세스 엔터티 일반적으로 사용자 이름 및 암호 같은 자격 증명을 통해 다른 엔터티의 hello id를 증명 하는 위치 |
| **[권한 부여](./azure-security-threat-modeling-tool-authorization.md)** | 어떻게 해야 합니까? 권한 부여는 응용 프로그램이 리소스 및 작업에 대한 액세스 제어를 제공하는 방법입니다. |
| **[통신 보안](./azure-security-threat-modeling-tool-communication-security.md)** | 누구에게 이야기하고 있나요? 통신 보안은 수행되는 모든 통신을 최대한 안전하게 유지합니다. |
| **[구성 관리](./azure-security-threat-modeling-tool-configuration-management.md)** | 응용 프로그램이 어떤 권한으로 실행되고 있나요? 어떤 데이터베이스에 연결되나요? 응용 프로그램이 어떤 방식으로 관리되나요? 이러한 설정은 어떻게 보호되나요? 구성 관리 toohow 참조 응용 프로그램에서 이러한 운영 문제를 처리 |
| **[암호화](./azure-security-threat-modeling-tool-cryptography.md)** | 비밀(기밀성)은 어떻게 유지하나요? 데이터 또는 라이브러리의 변조를 방지하려면 어떻게 하나요(무결성)? 암호로 강력하게 보호해야 하는 임의 값에 대해 시드를 제공하려면 어떻게 해야 하나요? 암호화 참조 toohow 기밀성과 무결성을 적용 하는 응용 프로그램 |
| **[예외 관리](./azure-security-threat-modeling-tool-exception-management.md)** | 응용 프로그램의 메서드 호출이 실패하면 응용 프로그램은 어떻게 하나요? 얼마나 많은 정보를 노출하고 있나요? 반환 합니까 친숙 한 오류 정보 tooend 사용자? 중요 한 예외 정보 백 toohello 호출자에 게 전달 합니까? 응용 프로그램이 정상적으로 실패하나요? |
| **[유효성 검사 입력](./azure-security-threat-modeling-tool-input-validation.md)** | 응용 프로그램에서 수신 하는 hello 입력이 유효 하 고 안전 하 게 보호는 어떻게 알 수 있을까요? 입력된 유효성 검사 의미 toohow 응용 프로그램 필터링, 삭제 또는 추가 처리 하기 전에 입력을 거부 합니다. 진입점을 통해 입력을 제한하고 종료 지점을 통과하는 출력을 인코딩하는 것이 좋습니다. 데이터베이스 및 파일 공유와 같은 원본의 데이터를 신뢰할 수 있나요? |
| **[중요 데이터](./azure-security-threat-modeling-tool-sensitive-data.md)** | 응용 프로그램은 중요한 데이터를 어떻게 처리하나요? 중요 한 데이터 참조 toohow hello 네트워크를 통해 메모리에 또는 영구 저장소에서 보호 해야 하는 모든 데이터를 처리 하는 응용 프로그램 |
| **[세션 관리](./azure-security-threat-modeling-tool-session-management.md)** | 응용 프로그램은 사용자 세션을 어떻게 처리하고 보호하나요? 세션 참조 tooa 일련의 사용자와 웹 응용 프로그램 간의 관련된 상호 작용 |

세션을 다음을 파악하는 데 도움이 됩니다.

* 여기서 hello 가장 일반적인 실수는
* 어디 hello 가장 조치 가능한 개선 되나요

결과적으로, 이러한 범주 toofocus를 사용 하 고 hello 입력된 유효성 검사, 인증 및 권한 부여 범주에서 발생 hello 가장 많이 사용 된 보안 문제를 알고 있는 경우 시작할 수 있습니다 수 있도록 보안 작업을 우선 순위를 지정 합니다. 자세한 내용은 **[이 특허 링크](https://www.google.com/patents/US7818788)**를 방문하세요.

## <a name="next-steps"></a>다음 단계

방문  **[위협 모델링 도구 위협](./azure-security-threat-modeling-tool-threats.md)**  toolearn에 더 알아봅니다 hello 위협 범주 hello 도구 toogenerate 디자인 위협 요소를 사용 합니다.
