---
title: "논리 앱에서 aaaAdd hello OneDrive 커넥터 | Microsoft Docs"
description: "REST API 매개 변수를 사용 하는 hello OneDrive 커넥터 개요"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a>Hello OneDrive 커넥터와 함께 시작
TooOneDrive toomanage 업로드, get, 파일, 삭제 등을 포함 한 파일을 연결 합니다. 

OneDrive를 사용하여 다음과 같은 작업을 수행합니다. 

* OneDrive에서 파일을 저장하여 워크플로를 작성하거나 OneDrive의 기존 파일을 업데이트합니다. 
* 파일을 생성 하거나 OneDrive 내에서 업데이트 하는 경우 트리거 toostart 워크플로 사용 합니다.
* 파일을 삭제를 작업 toocreate 파일을 사용 합니다. 예를 들어 새 Office 365 전자 메일이 첨부 파일과 함께 수신되면(트리거) OneDrive에 새 파일을 만듭니다(작업).

이 항목에서는 방법을 toouse hello 논리 앱에서 OneDrive 커넥터 및 트리거 및 작업 그룹의 hello도 합니다.

논리 앱에 대해 자세히 toolearn 참조 [논리 앱 이란](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

## <a name="connect-tooonedrive"></a>TooOneDrive 연결
논리 앱에서 모든 서비스에 액세스 하기 전에 먼저 만들어야는 *연결* toohello 서비스입니다. 연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다. 예를 들어, tooconnect tooOneDrive 먼저 OneDrive *연결*합니다. toocreate 연결을 일반적으로 tooconnect를 원하는 tooaccess hello 서비스를 사용 하는 hello 자격 증명을 입력 합니다. 따라서 OneDrive를 사용 hello tooyour OneDrive 계정 toocreate hello 연결 시 자격 증명을 입력 합니다.

### <a name="create-hello-connection"></a>Hello 연결 만들기
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a>트리거 사용
트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다. 트리거 "서비스를 폴링하기" hello 간격 및 원하는 빈도 합니다. [트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)

1. Hello 논리 앱에서 "onedrive" tooget hello 트리거 목록을 입력 합니다.  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. **파일을 수정할 때**를 선택합니다. 연결이 이미 존재 하는 경우에 hello 선택 표시 단추 tooselect 폴더를 선택 합니다.
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    증명된 toosign 인 경우 hello 로그인 세부 정보 toocreate hello 연결에을 입력 합니다. [Hello 연결을 만들](connectors-create-api-onedrive.md#create-the-connection) 이 항목의 hello 단계를 소개 합니다. 
   
   > [!NOTE]
   > 이 예제에서는 hello 논리 앱 업데이트를 선택 하는 hello 폴더에 파일을 실행 합니다. 이 트리거의 toosee hello 결과 전자 메일을 보내는 다른 동작을 추가 합니다. 예를 들어 Office 365 Outlook hello 추가 *전자 메일 보내기* 파일 업데이트 될 때 전자 메일로 보내면 동작 합니다. 

3. 선택 hello **편집** 단추 및 hello 설정 **주파수** 및 **간격** 값입니다. 예를 들어 15 분 마다 hello 트리거 toopoll 하려는 경우 다음 설정 hello **주파수** 너무**분**, 및 집합 hello **간격** 너무**15**. 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. **저장** 변경 내용을 (hello 도구 모음의 왼쪽된 상단 모서리). 논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.

## <a name="use-an-action"></a>작업 사용
동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다. [작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)

1. Hello 더하기 기호를 선택 합니다. 여러 선택 항목을 참조 하십시오: **동작 추가**, **조건을 추가**, hello 중 하나 또는 **자세한** 옵션입니다.
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. **작업 추가**를 선택합니다.
3. Hello 텍스트 상자에 "onedrive" tooget hello 사용 가능한 모든 작업 목록을 입력 합니다.
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. 이 예제에서는 **OneDrive - 파일 만들기**를 선택합니다. 연결이 이미 존재 하는 경우 다음 hello 선택 **폴더 경로** tooput hello 파일, 입력 hello **파일 이름**, hello를 선택 하 고 **파일 콘텐츠** 원하는:  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    Hello 연결 정보에 대 한 메시지가 표시 되 면 hello, toocreate hello 연결 세부 정보를 입력 합니다. [Hello 연결을 만들](connectors-create-api-onedrive.md#create-the-connection) 이 항목에서 이러한 속성을 설명 합니다. 
   
   > [!NOTE]
   > 이 예제에서는 OneDrive 폴더에 새 파일을 만듭니다. 다른 트리거 toocreate hello OneDrive 파일에서 출력을 사용할 수 있습니다. 예를 들어 Office 365 Outlook hello 추가 *새 전자 메일 도착* 트리거. 다음 추가 hello OneDrive *파일 만들기* hello 첨부 파일 및 콘텐츠 형식 필드를 사용 하 여 OneDrive에 ForEach toocreate hello 새 파일 내에서 작업 합니다. 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. **저장** 변경 내용을 (hello 도구 모음의 왼쪽된 상단 모서리). 논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.


## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/onedriveconnector/)합니다.

## <a name="more-connectors"></a>추가 커넥터
Toohello 돌아가서 [Api 목록](apis-list.md)합니다.
