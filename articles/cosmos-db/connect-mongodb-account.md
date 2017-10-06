---
title: "Cosmos DB Azure 계정에 대 한 연결 문자열 aaaMongoDB | Microsoft Docs"
description: "어떻게 tooconnect MongoDB 앱 tooan Azure Cosmos DB는 MongoDB 연결 문자열을 사용 하 여을 계정에 대해 알아봅니다."
keywords: "MongoDB 연결 문자열"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a>MongoDB 응용 프로그램 tooAzure Cosmos DB에 연결
어떻게 tooconnect MongoDB 앱 tooan Azure Cosmos DB는 MongoDB 연결 문자열을 사용 하 여을 계정에 대해 알아봅니다. Azure Cosmos DB 데이터베이스 hello 데이터로 사용할 수 있습니다 MongoDB 앱에 대 한 저장소입니다. 

이 자습서에서는 두 가지 방법으로 tooretrieve 연결 문자열 정보를 제공합니다.

- [hello quick start 메서드](#QuickstartConnection),.NET, Node.js, MongoDB 셸, Java, 및 Python 드라이버와 함께 사용 하기 위해
- [사용자 지정 연결 문자열 방법을 hello](#GetCustomConnection), 다른 드라이버와 함께 사용 하기 위해

## <a name="prerequisites"></a>필수 조건

- Azure 계정. Azure 계정이 없으면 지금 [무료 Azure 계정](https://azure.microsoft.com/free/)을 만듭니다. 
- Azure Cosmos DB 계정. 자세한 내용은 [.net MongoDB API 웹 응용 프로그램을 빌드 및 Azure 포털 hello](create-mongodb-dotnet.md)합니다.

## <a id="QuickstartConnection"></a>빠른 시작 hello를 사용 하 여 hello MongoDB 연결 문자열을 가져옵니다.
1. 인터넷 브라우저를 toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello에 **Azure Cosmos DB** 블레이드에서 MongoDB 계정에 대 한 선택 hello API입니다. 
3. Hello 계정 블레이드의 hello 왼쪽된 창에서 클릭 **퀵 스타트**합니다. 
4. 플랫폼(**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**)을 선택합니다. 드라이버나 도구가 목록에 없더라도 계속해서 더 많은 연결 코드 조각을 문서화하므로 걱정하지 마세요. 원하는에 아래 의견을 보내주세요. toosee 합니다. toolearn 어떻게 toocraft 자체 연결 읽을 [hello 계정 연결 문자열 정보를 가져올](#GetCustomConnection)합니다.
5. 복사한 hello 코드 조각 MongoDB 앱에 붙여 넣습니다.

    ![빠른 시작 블레이드](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a>Hello MongoDB 연결 문자열 toocustomize 가져오기
1. 인터넷 브라우저를 toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello에 **Azure Cosmos DB** 블레이드에서 MongoDB 계정에 대 한 선택 hello API입니다. 
3. Hello 계정 블레이드의 hello 왼쪽된 창에서 클릭 **연결 문자열**합니다. 
4. hello **연결 문자열** 블레이드를 엽니다. Preconstructed 연결 문자열을 포함 하 여 MongoDB에 대 한 드라이버를 사용 하 여 모든 hello 정보 필요한 tooconnect toohello 계정을에 있습니다.

    ![연결 문자열 블레이드](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>연결 문자열 요구 사항
> [!Important]
> Azure Cosmos DB에는 엄격한 보안 요구 사항과 표준이 있습니다. Azure Cosmos DB 계정에는 *SSL*을 통한 인증 및 보안 통신이 필요합니다. 
>
>

Azure Cosmos DB 지원 hello 표준 MongoDB 연결 문자열 URI 형식으로 두 가지 특정 요구 사항: Azure Cosmos DB 계정 인증 및 SSL 통해 보안 통신에 필요 합니다. 따라서 hello 연결 문자열 형식은 다음과 같습니다.

    mongodb://username:password@host:port/[database]?ssl=true

이 문자열의 hello 값 hello에서 사용할 수 있는 **연결 문자열** 블레이드 앞에 표시 된:

* Username(필수): Azure Cosmos DB 계정 이름
* Password(필수): Azure Cosmos DB 계정 암호
* 호스트 (필수): hello Azure Cosmos DB 계정의 FQDN입니다.
* Port(필수): 10255
* 데이터베이스 (옵션): hello 데이터베이스 연결 hello를 사용 합니다. Hello 기본 데이터베이스 "test"가 없는 데이터베이스를 제공 하는 경우
* ssl=true(필수)

예를 들어 hello에 표시 된 hello 계정 **연결 문자열** 블레이드입니다. 유효한 연결 문자열은 다음과 같습니다.

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[MongoChef를 사용 하 여](mongodb-mongochef.md) MongoDB 계정에 대 한 Azure Cosmos DB API를 사용 합니다.
* MongoDB에 대 한 확인 하 여 hello Azure Cosmos DB API를 탐색 [샘플](mongodb-samples.md)합니다.
