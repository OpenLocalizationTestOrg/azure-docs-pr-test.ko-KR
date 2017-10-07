---
title: "aaaLearn 어떻게 toouse hello 논리 앱에서 Twitter 커넥터 | Microsoft Docs"
description: "REST API 매개 변수를 사용하는 Twitter 커넥터 개요"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a>Hello Twitter 커넥터와 함께 시작
Hello Twitter 커넥터와 함께 다음 작업을 수행할 수 있습니다.

* 트윗 게시 및 트윗 가져오기
* 타임라인, 친구 및 팔로워 액세스
* 다른 동작 및 트리거 아래에 설명 된 hello를 수행  

toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다. [지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.  

## <a name="connect-tootwitter"></a>TooTwitter 연결
Toocreate 먼저 논리 앱에서 모든 서비스에 액세스 하기 전에 *연결* toohello 서비스입니다. [연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.  

### <a name="create-a-connection-tootwitter"></a>연결 tooTwitter 만들기
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a>Twitter 트리거 사용
트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다. [트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)

이 예제에서는 하겠습니다 어떻게 toouse hello **새 윗이 게시 될 때** #Seattle에 대 한 toosearch 트리거되며 #Seattle 있더라도 hello 텍스트 hello 윗을 Dropbox에 파일을 업데이트 합니다. 엔터프라이즈 예제에서는 회사의 hello 이름에 대 한 검색 하 고 hello 텍스트 hello 윗에서 SQL 데이터베이스 업데이트 수 있습니다.

1. 입력 *twitter* hello 논리 앱 디자이너에 hello 검색 상자에 다음 hello 선택 **Twitter-새 윗 게시 될 때** 트리거   
   ![Twitter 트리거 이미지 1](./media/connectors-create-api-twitter/trigger-1.png)  
2. 입력 *#Seattle* hello에 **검색 텍스트** 컨트롤  
   ![Twitter 트리거 이미지 2](./media/connectors-create-api-twitter/trigger-2.png) 

이 시점에서 다른 트리거 및 작업 hello 워크플로에서 hello에 대 한 실행을 시작 합니다 트리거 논리 앱 구성 되었습니다. 

> [!NOTE]
> 기능 논리 앱 toobe는, 하나 이상의 트리거와 작업을 하나 포함 해야 합니다. Hello 다음 섹션 tooadd 동작의에서 hello 단계를 수행 합니다.  
> 
> 

## <a name="add-a-condition"></a>조건 추가
50 개 이상의 사용자와 사용자 로부터 트 윗에만 관심이, 이후 후속 작업이 hello 수를 확인 하는 조건은 먼저 추가 해야 toohello 논리 앱.  

1. 선택 **+ 새 단계** tooadd hello 작업 원하는 tootake #Seattle 새 윗에서 발견 된 경우  
   ![Twitter 작업 이미지 1](../../includes/media/connectors-create-api-twitter/action-1.png)  
2. 선택 hello **조건 추가** 링크 합니다.  
   ![Twitter 조건 이미지 1](../../includes/media/connectors-create-api-twitter/condition-1.png)   
   Hello 열립니다 **조건** 제어와 같은 상태를 확인할 수는 위치 *같으면*, *는 보다 작은*, *보다 크면*, *포함*등입니다.  
   ![Twitter 조건 이미지 2](../../includes/media/connectors-create-api-twitter/condition-2.png)   
3. 선택 hello **값 선택** 제어 합니다.  
   이 컨트롤의 조건을 평가 tootrue 또는 false가 됩니다 hello 값으로 hello 속성 중 하나 이상을 트리거 하거나 모든 이전 작업에서에 선택할 수 있습니다.
   ![Twitter 조건 이미지 3](../../includes/media/connectors-create-api-twitter/condition-3.png)   
4. 선택 hello **...**  tooexpand hello 목록이 속성 사용할 수 있는 모든 hello 속성을 볼 수 있도록 합니다.        
   ![Twitter 조건 이미지 4](../../includes/media/connectors-create-api-twitter/condition-4.png)   
5. 선택 hello **후속 작업이 count** 속성입니다.    
   ![Twitter 조건 이미지 5](../../includes/media/connectors-create-api-twitter/condition-5.png)   
6. 공지 hello 후속 작업이 count 속성 hello 값 컨트롤에 포함 되었습니다.    
   ![Twitter 조건 이미지 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. 선택 **보다 크면** hello 연산자 목록에서 합니다.    
   ![Twitter 조건 이미지 7](../../includes/media/connectors-create-api-twitter/condition-7.png)   
8. Hello에 대 한 피연산자 hello 50 입력 *보다 크면* 연산자입니다.  
   hello 조건이 추가 됩니다. Hello를 사용 하 여 작업을 저장 **저장** 위의 hello 메뉴에 링크 합니다.    
   ![Twitter 조건 이미지 8](../../includes/media/connectors-create-api-twitter/condition-8.png)   

## <a name="use-a-twitter-action"></a>Twitter 작업 사용
동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다. [작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)  

트리거를 추가 하면 했으므로 다음 단계 tooadd hello 트리거가 여 hello 트 윗의 hello 내용으로 새 윗에서 게시 하는 동작을 수행 합니다. 이 연습의 목적 hello에 대 한가 50 개 이상의 후속 작업이 있는 사용자의 윗만 게시 됩니다.  

Hello 다음 단계에서 50 개 이상의 후속 작업이 가진 사용자가 게시 된 각 윗의 hello 속성 중 일부를 사용 하 여 트 윗 게시할 Twitter 동작을 추가 합니다.  

1. **작업 추가**를 선택합니다. 이렇게 하면 다른 동작 및 트리거를 검색할 수 있는 hello 검색 컨트롤을 열립니다.  
   ![Twitter 조건 이미지 9](../../includes/media/connectors-create-api-twitter/condition-9.png)   
2. 입력 *twitter* hello 검색 상자에 다음 hello 선택 **Twitter-여 트 윗 게시** 동작 합니다. Hello 열립니다 **여 트 윗 게시** 입력할 수 있는 모든 세부 사항을 게시 되는 hello 트 윗에 대 한 제어 합니다.      
   ![Twitter 작업 이미지 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)   
3. 선택 hello **텍스트 윗** 제어 합니다. 이전 동작 및 트리거 hello 논리 앱에서의 모든 출력에 표시 됩니다. 이러한 항목 중 하나를 선택할 수 있으며 hello 새 윗의 hello 윗 텍스트의 일부로 사용 합니다.     
   ![Twitter 작업 이미지 2](../../includes/media/connectors-create-api-twitter/action-2.png)   
4. **사용자 이름**을 선택합니다.   
5. 입력 *표시:* hello 윗 텍스트 컨트롤에 있습니다. 사용자 이름 바로 뒤에 나오도록 합니다.  
6. *트윗 텍스트*를 선택합니다.       
   ![Twitter 작업 이미지 3](../../includes/media/connectors-create-api-twitter/action-3.png)   
7. 작업 내용을 저장 하 고 워크플로 hello #Seattle hashtag tooactivate와 한 트 윗을 보낼 합니다.  


## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/twitterconnector/)합니다. 

## <a name="next-steps"></a>다음 단계
[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)

