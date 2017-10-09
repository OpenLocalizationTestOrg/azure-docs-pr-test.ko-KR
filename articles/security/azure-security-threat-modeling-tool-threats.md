---
title: "-Microsoft 위협 모델링 도구-aaaThreats Azure | Microsoft Docs"
description: "Hello Microsoft 위협 모델링 도구에 대 한 위협 범주 페이지에서 노출 하는 모든 범주를 포함 하 위협 생성 됩니다."
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
ms.openlocfilehash: 0bd51f81370b6385ff1ac9769e34fc089e1dfc9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-threats"></a>Microsoft 위협 모델링 도구 위협

hello 위협 모델링 도구에는 hello Microsoft SDL Security Development Lifecycle ()의 핵심 요소입니다. 소프트웨어를 통해 tooidentify 만드는 일 및 상대적으로 간편 하 고 비용 효율적인 tooresolve 있을 때 잠재적 보안 문제를 조기에 완화 합니다. 결과적으로, 개발의 hello 총 비용이 크게 감소합니다. 또한 hello 도구를 보다 쉽게 위협 모델링에 대 한 모든 개발자가 작성 및 위협 모델 분석에 명확한 지침을 제공 하 여을 염두에 비보안 전문가 함께 설계 합니다.

> Hello 방문  **[위협 모델링 도구](./azure-security-threat-modeling-tool.md)**  tooget 오늘 시작!

위협 모델링 도구 hello hello 아래 셰이프와 같은 특정 정보를 확인할 수 있습니다.

* 공격자가 수 hello 인증 데이터를 변경 하는 방법
* 공격자는 hello 사용자 프로필 데이터를 읽을 수 있으면 hello 영향 이란?
* Toohello 사용자 프로필 데이터베이스에 있어야 하는 경우 어떻게 됩니까?

## <a name="stride-model"></a>STRIDE 모델

이러한 종류의 뾰족한 질문, 다양 한 유형의 위협 분류 되 고 간소화 하 Microsoft 사용 하 여 hello STRIDE 모델을 작성 하는 toobetter 도움말 hello 전반적인 보안 대화입니다.

| Category | 설명 |
| -------- | ----------- |
| **스푸핑** | 사용자 이름 및 암호와 같은 다른 사용자의 인증 정보를 불법적으로 액세스하고 사용하는 경우를 나타냅니다. |
| **변조** | Hello 악성 데이터 수정을 작업이 포함 됩니다. 예로 무단된 변경한 hello 인터넷 등의 개방형 네트워크를 통한 두 컴퓨터 사이 전달 되는 데이터베이스 및 데이터를 변경할 때 hello에 보관 된 같은 toopersistent 데이터 |
| **거부** | 상대방은 모든 방식으로 tooprove 그렇지 않으면 없이 작업 수행을 거부 된 사용자와 연결 된-사용자가 없는 hello 기능 tootrace 금지 hello 작업 시스템에서 잘못 된 작업을 수행 하는 예를 들어 있습니다. Non-repudiation 시스템 toocounter 거부 위협의 toohello 능력을 나타냅니다. 예를 들어 항목을 구입 하는 사용자를 받 때 hello 항목에 대 한 toosign이 있을 수 있습니다. 사용 하 여 hello hello 사용자가 hello 패키지를 수신 하는 증명 정보로 수신을 서명 그런 다음 공급 업체 hello 수 있습니다. |
| **정보 공개** | Toohave 액세스 tooit 해서는 안 되는 정보 tooindividuals hello 노출 포함-예를 들어 사용자가 tooread 없었기 하는 파일의 hello 기능 액세스 권한이 부여 to, 또는 hello 두 컴퓨터 간에 전송 되는 침입자가 tooread 데이터의 기능 |
| **서비스 거부** | 서비스 거부 (dos) 공격 서비스 toovalid 사용자의 거부-예를 들어 함으로써 웹 서버 일시적으로 사용할 수 없거나 사용할 수 없게 됩니다. 특정 유형의 DoS 공격 으로부터 보호 해야 tooimprove 시스템 가용성 및 안정성을 간단히 위협 |
| **권한 상승** | 권한 없는 사용자 권한 있는 액세스 권한을 얻는 함으로써에 충분 한 액세스 toocompromise 여부나 한 hello 전체 시스템을 삭제 합니다. 권한 상승 위협 경우 공격자가 효과적으로 모든 시스템 방어에 침투 하 고 있는 자체를 위험한 상황을 실제로 hello 신뢰할 수 있는 시스템의 일부가 포함 |

## <a name="next-steps"></a>다음 단계

너무 계속**[위협 모델링 도구 완화](./azure-security-threat-modeling-tool-mitigations.md)**  toolearn hello 다양 한 방법으로 Azure는 이러한 위협을 완화할 수 있습니다.
