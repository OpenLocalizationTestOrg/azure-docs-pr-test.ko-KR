---
title: "Azure 논리 앱에 aaaUse hello Slack 커넥터 | Microsoft Docs"
description: "TooSlack 논리 앱에 연결"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a>Hello Slack 커넥터와 함께 시작
Slack은 팀의 모든 통신을 한데 모아, 어디서나 즉시 검색 및 사용할 수 있는 팀 통신 도구입니다. 

논리 앱을 만들어 시작합니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.

## <a name="create-a-connection-tooslack"></a>연결 tooSlack 만들기
toouse hello Slack 커넥터를 처음 만들면는 **연결** 다음 이러한 속성에 대 한 hello 세부 정보를 제공 합니다. 

| 속성 | 필수 | 설명 |
| --- | --- | --- |
| 신뢰 |예 |Slack 자격 증명 제공 |

이러한 단계 toosign 여유 시간 및 완료 hello 구성의 hello 여유 시간에 따라 **연결** 논리 앱에서:

1. **되풀이**
2. **빈도**를 선택하고 **간격**을 입력합니다.
3. **작업 추가**를 선택합니다.  
   ![Slack 구성][1]  
4. Hello 검색 상자에 Slack을 입력 하 고 기다리는 hello 검색 tooreturn hello 이름에 Slack 가진 모든 항목
5. **Slack-메시지 게시**
6. 선택 **tooSlack 로그인**:  
   ![Slack 구성][2]
7. 사용자 자격 증명 Slack toosign tooauthorize hello 응용 프로그램에서 제공 합니다.    
   ![Slack 구성][3]  
8. 리디렉션된 tooyour 조직의 로그인 페이지 수. 있습니다 **권한 부여** 논리 앱과 함께 Slack toointeract:      
   ![Slack 구성][5] 
9. Hello 권한 부여가 완료 된 후 수 리디렉션된 tooyour 논리 앱 toocomplete hello를 구성 하 여 해당 **여유-모든 메시지를 가져오기** 섹션. 필요한 다른 트리거 및 작업을 추가합니다.  
   ![Slack 구성][6]
10. 작업을 선택 하 여 저장 **저장** 위의 hello 메뉴 모음의 합니다.

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/slack/)합니다.

## <a name="more-connectors"></a>추가 커넥터
Toohello 돌아가서 [Api 목록](apis-list.md)합니다.

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
