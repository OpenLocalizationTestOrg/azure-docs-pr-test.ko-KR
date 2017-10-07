---
title: "aaaLearn 어떻게 toouse hello 논리 앱에서 SFTP 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. API tooSFTP toosend를 연결 하 고 파일을 받습니다. 파일 만들기, 업데이트, 가져오기 또는 삭제와 같은 다양한 작업을 수행할 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a>Hello SFTP 커넥터와 함께 시작
사용 하 여 hello SFTP 커넥터 tooaccess SFTP toosend 계정 및 파일을 수신 합니다. 파일 만들기, 업데이트, 가져오기 또는 삭제와 같은 다양한 작업을 수행할 수 있습니다.  

toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다. [지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.

## <a name="connect-toosftp"></a>TooSFTP 연결
Toocreate 먼저 논리 앱에서 모든 서비스에 액세스 하기 전에 *연결* toohello 서비스입니다. [연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.  

### <a name="create-a-connection-toosftp"></a>연결 tooSFTP 만들기
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>SFTP 트리거 사용
트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다. [트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)  

이 예제에서는 hello **SFTP-파일 추가 또는 수정 되 면** 파일은 추가, 또는 SFTP 서버에서 수정 될 때 트리거를 사용 하는 tooinitiate 논리 앱 워크플로 합니다. 또한 hello 새롭거나 수정 된 파일의 hello 내용을 확인 하 고 내용이 hello 내용을 사용 하기 전에 추출할 수를 나타내는 경우 의사 결정 tooextract hello 파일 하 게 하는 조건을 추가 합니다. 마지막으로 파일의 동작 tooextract hello 내용을 추가 하 고 hello SFTP 서버의 폴더에 추출 하는 hello 내용을 배치 합니다. 

엔터프라이즈 예를 들어 고객 주문을 나타내는 새 파일에 대 한이 트리거 toomonitor SFTP 폴더를 사용할 수 있습니다.  사용할 수 있습니다 다음 SFTP 커넥터 동작의 경우와 같은 **파일 콘텐츠를 가져옵니다.**, 추가 처리 및 orders 데이터베이스의 저장소에 대 한 hello 주문의 tooget hello 내용을 합니다.

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>조건 추가
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>SFTP 작업 사용
동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다. [작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/sftpconnector/)합니다.

## <a name="more-connectors"></a>추가 커넥터
Toohello 돌아가서 [Api 목록](apis-list.md)합니다.
