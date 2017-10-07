---
title: "aaaLearn 어떻게 toouse hello 논리 앱에서 FTP 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. TooFTP 서버 toomanage 파일을 연결 합니다. FTP 서버에서 파일 업로드, 업데이트, 가져오기 및 삭제와 같은 다양한 작업을 수행할 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a>Hello FTP 커넥터와 함께 시작
커넥터 toomonitor hello FTP 사용 하 여 관리 하 고 FTP 서버에서 파일을 만듭니다. 

toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다. [지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.

## <a name="connect-tooftp"></a>TooFTP 연결
Toocreate 먼저 논리 앱에서 모든 서비스에 액세스 하기 전에 *연결* toohello 서비스입니다. [연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.  

### <a name="create-a-connection-tooftp"></a>연결 tooFTP 만들기
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a>FTP 트리거 사용
트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다. [트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)  

> [!IMPORTANT]
> hello FTP 커넥터 hello 인터넷에서에서 액세스할 수 있으며가 FTP 서버 수동 모드 toooperate를 구성 해야 합니다. Hello FTP 커넥터는 또한 **암시적 FTPS (FTP SSL 통해)와 호환 되지 않는**합니다. hello FTP 커넥터 명시적 FTPS (FTP SSL 통한)을 지원합니다.  
> 
> 

이 예제에서는 하겠습니다 어떻게 toouse hello **FTP-파일을 추가 하거나 수정 하는 경우** 파일은 추가, 또는 FTP 서버에서 수정 될 때 tooinitiate 논리 앱 워크플로 트리거합니다. 엔터프라이즈 예를 들어 고객 으로부터 주문을 나타내는 새 파일에 대 한이 트리거 toomonitor FTP 폴더를 사용할 수 있습니다.  사용할 수 있습니다 다음 FTP 커넥터 작업 같은 **파일 콘텐츠를 가져옵니다.** tooget hello 내용의 hello 순서 추가 처리 및 orders 데이터베이스에 저장 합니다.

1. 입력 *ftp* hello 논리 앱 디자이너에 hello 검색 상자에 다음 hello 선택 **FTP-파일 추가 또는 수정 되 면** 트리거   
   ![FTP 트리거 이미지 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)  
   hello **파일 추가 또는 수정할 때** 제어 열립니다  
   ![FTP 트리거 이미지 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)  
2. 선택 hello **...**  hello hello 컨트롤의 오른쪽에 있습니다. Hello 폴더 선택 컨트롤을 열립니다.  
   ![FTP 트리거 이미지 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)  
3. 선택 hello  **>**  (오른쪽 화살표) 새롭거나 수정 된 파일에 대 한 toomonitor 되도록 toofind hello 폴더를 찾습니다. Hello 폴더를 선택 하 고 hello 폴더는 hello에 표시 된 **폴더** 제어 합니다.  
   ![FTP 트리거 이미지 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)   

이 시점에서 논리 앱 때 시작 될 hello 실행 하는 다른 트리거 및 hello 워크플로에서 작업 파일을 수정 또는 hello 특정 FTP 폴더에 생성 하는 트리거도 구성 되었습니다. 

> [!NOTE]
> 기능 논리 앱 toobe는, 하나 이상의 트리거와 작업을 하나 포함 해야 합니다. Hello 다음 섹션 tooadd 동작의에서 hello 단계를 수행 합니다.  
> 
> 

## <a name="use-a-ftp-action"></a>FTP 작업 사용
동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다. [작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)  

트리거를 추가 하면 했으므로 이러한 단계 tooadd을 hello 트리거가 여 hello 새롭거나 수정 된 파일의 hello 내용의 받을 작업을 수행 합니다.    

1. 선택 **+ 새 단계** tooadd hello hello 동작 tooget hello hello에 파일의 내용을 hello FTP 서버  
2. 선택 hello **동작 추가** 링크 합니다.  
   ![FTP 작업 이미지 1](./media/connectors-create-api-ftp/ftp-action-1.png)  
3. 입력 *FTP* toosearch 모든 작업에 대 한 관련 tooFTP 합니다.
4. 선택 **FTP-파일 내용을 가져오기** hello FTP 폴더에는 새로운 또는 수정 된 파일을 찾으면 동작 tootake hello으로 합니다.      
   ![FTP 작업 이미지 2](./media/connectors-create-api-ftp/ftp-action-2.png)  
   hello **파일 콘텐츠를 가져옵니다.** 제어 열립니다. **참고**: 있습니다 하지 않았으면 지금 이전에 FTP 서버 계정을 하 여 논리 앱 tooaccess tooauthorize 메시지 표시 됩니다.  
   ![FTP 작업 이미지 3](./media/connectors-create-api-ftp/ftp-action-3.png)   
5. 선택 hello **파일** 컨트롤 (아래에 있는 공백을 hello **파일***). 여기에서 사용할 수 있습니다 hello의 다양 한 속성이 hello FTP 서버에서 발견 된 hello 새롭거나 수정 된 파일에서.  
6. 선택 hello **콘텐츠 파일** 옵션입니다.  
   ![FTP 작업 이미지 4](./media/connectors-create-api-ftp/ftp-action-4.png)   
7. 해당 hello 나타내는 hello 컨트롤을 업데이트 **FTP-파일 내용을 가져오기** 작업 hello 받아볼 *콘텐츠 파일* hello FTP 서버에 hello 새롭거나 수정 된 파일의 합니다.      
   ![FTP 작업 이미지 5](./media/connectors-create-api-ftp/ftp-action-5.png)     
8. 작업을 저장 한 다음 파일 toohello FTP 폴더 tootest 워크플로에 추가 합니다.    

Hello 논리 앱 되었습니다이 시점에 구성 된 트리거 toomonitor로 폴더는 FTP 서버와 시작 hello 워크플로 새 파일 또는 hello FTP 서버에서 수정 된 파일을 찾으면 됩니다. 

또한 hello 논리 앱 hello 새롭거나 수정 된 파일의 동작 tooget hello 내용으로 구성 되어 했습니다.

이제 hello와 같은 다른 작업을 추가할 수 있습니다 [SQL Server-행 삽입](connectors-create-api-sqlazure.md) hello 새롭거나 수정 된 파일을 SQL 데이터베이스 테이블에 내용의 tooinsert hello 동작 합니다.  

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/ftpconnector/)합니다. 

## <a name="next-steps"></a>다음 단계
[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)

