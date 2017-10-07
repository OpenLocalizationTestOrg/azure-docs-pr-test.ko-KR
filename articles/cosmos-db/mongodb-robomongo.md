---
title: Azure Cosmos db Robomongo aaaUse | Microsoft Docs
description: "자세한 내용은 방법 toouse Azure Cosmos DB와 함께 Robomongo: MongoDB 계정에 대 한 API"
keywords: robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Azure Cosmos DB: MongoDB API 계정으로 Robomongo 사용
Azure Cosmos DB tooconnect tooan: Robomongo를 사용 하 여 MongoDB 계정에 대 한 API를 수행 해야 합니다.

* [Robomongo](https://robomongo.org/) 다운로드 및 설치
* Azure Cosmos DB: MongoDB API 계정의 [연결 문자열](connect-mongodb-account.md) 정보가 필요합니다.

## <a name="connect-using-robomongo"></a>Robomongo를 사용하여 연결
tooadd Azure Cosmos DB: MongoDB 계정 toohello Robomongo MongoDB 연결에 대 한 API hello 다음 단계를 수행 합니다.

1. Azure Cosmos DB 검색: hello 지침을 사용 하 여 MongoDB 계정 연결 정보에 대 한 API [여기](connect-mongodb-account.md)합니다.

    ![Hello 연결 문자열 블레이드의 스크린 샷](./media/mongodb-robomongo/connectionstringblade.png)
2. *Robomongo.exe* 실행

3. 아래 hello 연결 단추를 클릭 **파일** toomanage 연결 합니다. 클릭 **만들기** hello에 **MongoDB 연결** hello를 열 수 있는 창을 **연결 설정을** 창.

4. Hello에 **연결 설정을** 창에서 이름을 선택 합니다. 그런 다음 hello 찾을 **호스트** 및 **포트** 에 입력 하 고 1 단계에서 연결 정보를에서 만든 **주소** 및 **포트**각각 .

    ![연결을 관리 하는 Robomongo hello 스크린 샷](./media/mongodb-robomongo/manageconnections.png)
5. Hello에 **인증** 탭을 클릭 **수행 인증**합니다. 그런 다음 데이터베이스(기본값은 *관리자*), **사용자 이름** 및 **암호**를 입력합니다.
**사용자 이름** 및 **암호**는 모두 1단계의 연결 정보에서 찾을 수 있습니다.

    ![Hello Robomongo 인증 탭 스크린 샷](./media/mongodb-robomongo/authentication.png)
6. Hello에 **SSL** 탭 **SSL 사용 되는 프로토콜**, 다음 hello 변경 **인증 방법을** 너무**자체 서명 된 인증서**합니다.

    ![Hello Robomongo SSL 탭 스크린 샷](./media/mongodb-robomongo/SSL.png)
7. 마지막으로, 클릭 **테스트** 수 tooconnect 다음 있는지 tooverify **저장**합니다.

## <a name="next-steps"></a>다음 단계
* Azure Cosmos DB: MongoDB API [샘플](mongodb-samples.md)을 살펴봅니다.
