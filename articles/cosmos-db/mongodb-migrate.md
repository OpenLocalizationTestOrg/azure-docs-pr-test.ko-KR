---
title: "aaaUse mongoimport 및와 mongorestore MongoDB에 대 한 Azure Cosmos DB API hello | Microsoft Docs"
description: "자세한 내용은 방법 toouse mongoimport 및 mongorestore tooimport 데이터 tooan API MongoDB 계정에 대 한"
keywords: mongoimport, mongorestore
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
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 921354bc7b09a076a73e0cbf5e4aabcc9e83d5a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a>Azure Cosmos DB: MongoDB 데이터 가져오기 

MongoDB tooan MongoDB에 대 한 hello API로 사용 하기 위해 Azure Cosmos DB 계정에서에서 toomigrate 데이터를 다음과 같이합니다.

* 다운로드 *mongoimport.exe* 또는 *mongorestore.exe* hello에서 [MongoDB 다운로드 센터](https://www.mongodb.com/download-center)합니다.
* [MongoDB API 연결 문자열](connect-mongodb-account.md)을 가져옵니다.

데이터를 가져오는 경우 Azure Cosmos DB hello 사용 하 여 MongoDB와 계획 toouse에서, hello를 사용 해야 [데이터 마이그레이션 도구](import-data.md) tooimport 데이터입니다.

이 자습서에서는 hello 다음 작업 방법을 배웁니다.

> [!div class="checklist"]
> * 연결 문자열 검색
> * mongoimport를 사용하여 MongoDB 데이터 가져오기
> * mongorestore를 사용하여 MongoDB 데이터 가져오기

## <a name="prerequisites"></a>필수 조건

* 처리량을 증가: hello 시간은 데이터 마이그레이션 hello 양을 컬렉션을 설정 하는 처리량에 따라 다릅니다. 더 큰 데이터 마이그레이션에 대 한 있는지 tooincrease hello 처리량 수 있습니다. Hello 마이그레이션을 마친 후 hello 처리량 toosave 비용을 절감 합니다. Hello에서 처리량을 증가 하는 방법에 대 한 자세한 내용은 [Azure 포털](https://portal.azure.com), 참조 [성능 수준 및 가격 책정 계층에 Azure Cosmos DB](performance-levels.md)합니다.

* SSL 사용: Azure Cosmos DB에는 엄격한 보안 요구 사항과 표준이 있습니다. 계정을 사용 하 여 상호 작용할 때 있는지 tooenable SSL 수 있습니다. hello 문서의 나머지 부분 hello의에서 hello 절차는 어떻게 mongoimport 및 mongorestore에 대 한 SSL tooenable 합니다.

## <a name="find-your-connection-string-information-host-port-username-and-password"></a>연결 문자열 정보(호스트, 포트, 사용자 이름 및 암호) 찾기

1. Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 창에서 클릭 hello **Azure Cosmos DB** 항목입니다.
2. Hello에 **구독** 창에서 계정 이름을 선택 합니다.
3. Hello에 **연결 문자열** 블레이드에서 클릭 **연결 문자열**합니다.  
hello toosuccessfully 해야 하는 모든 hello 정보를 포함 하는 창 오른쪽 tooyour 계정을 연결 하세요.

    ![연결 문자열 블레이드](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a>Mongoimport를 사용 하 여 MongoDB에 대 한 데이터 toohello API 가져오기

tooimport 데이터 tooyour Azure Cosmos DB 계정 서식 파일을 다음 hello를 사용 합니다. 입력 *호스트*, *username*, 및 *암호* hello 값을 특정 tooyour 계정을 가진 합니다.  

템플릿:

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

예제:  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a>Mongorestore를 사용 하 여 MongoDB에 대 한 데이터 toohello API 가져오기

MongoDB 계정에 대 한 toorestore 데이터 tooyour API 템플릿을 tooexecute hello 가져오는 다음 hello를 사용 합니다. 입력 *호스트*, *username*, 및 *암호* hello 값을 특정 tooyour 계정을 가진 합니다.

템플릿:

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

예제:

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a>성공적인 마이그레이션 가이드

1. 컬렉션을 미리 만들어 크기 조정:
        
    * 기본적으로 Azure Cosmos DB는 1,000RU(요청 단위)로 새 MongoDB 컬렉션을 프로비전합니다. Mongoimport, mongorestore, 또는 mongomirror를 사용 하 여 hello 마이그레이션을 시작 하기 전에 hello에서 모든 컬렉션을 만들고 미리 [Azure 포털](https://portal.azure.com) 또는 MongoDB 드라이버 및 도구입니다. 컬렉션 10GB 보다 큰 경우 확인 되었는지 toocreate는 [컬렉션 분할/분할](partition-data.md) 적절 한 분할 키가 있는 합니다.

    * Hello에서 [Azure 포털](https://portal.azure.com), 단일 파티션 컬렉션에 대해 1, 000 RUs 및 hello 마이그레이션에 대 한 분할 된 컬렉션에 대해 2500 RUs에서 컬렉션의 처리량을 증가 합니다. 처리량이 늘어나며 hello, 조정을 방지 하 고 마이그레이션할 짧은 시간 내에 사용할 수 있습니다. Azure Cosmos DB에서 대금 매시간 hello 마이그레이션 toosave 비용 직후 hello 처리량을 줄일 수 있습니다.

2. 단일 문서 쓰기에 대 한 대략적인 RU 충전 hello를 계산 합니다.

    a. MongoDB 셸 hello에서 tooyour Azure Cosmos DB MongoDB 데이터베이스를 연결 합니다. 지침을 찾을 수 있습니다 [MongoDB 응용 프로그램 tooAzure Cosmos DB 연결](connect-mongodb-account.md)합니다.
    
    b. MongoDB 셸 hello에서 샘플 문서 중 하나를 사용 하 여 샘플 insert 명령을 실행 합니다.
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    c. ```db.runCommand({getLastRequestStatistics: 1})```를 실행하고 다음과 같은 응답을 수신합니다.
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    d. Hello 요청 충전을 기록해 둡니다.
    
3. 사용자 컴퓨터 toohello Cosmos DB Azure 클라우드 서비스에서에서 hello 대기 시간을 결정 합니다.
    
    a. 이 명령을 사용 하 여 hello MongoDB 셸에서에서 자세한 로깅을 설정합니다```setVerboseShell(true)```
    
    b. Hello 데이터베이스에 대해 간단한 쿼리를 실행: ```db.coll.find().limit(1)```합니다. 다음과 같은 응답을 수신합니다.

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. 중복 된 문서가 없는 hello 마이그레이션 tooensure 전에 삽입 하는 hello 문서를 제거 합니다. 다음 명령을 사용하여 문서를 제거할 수 있습니다. ```db.coll.remove({})```

5. 대략적인 hello 계산 *batchSize* 및 *numInsertionWorkers* 값:

    * 에 대 한 *batchSize*, 나누기 hello 총 RUs hello RUs 3 단계에서 단일 문서 쓰기 프로그램에서 사용 하 여 사용자를 프로 비전 합니다.
    
    * Hello 계산 되는 경우 *batchSize* < 24 =으로 해당 번호를 사용 하면 *batchSize* 값입니다.
    
    * Hello 계산 되는 경우 *batchSize* > 24, 집합 hello *batchSize* 값 too24 합니다.
    
    * *numInsertionWorkers*의 경우 *numInsertionWorkers =  (프로비전된 처리량 * 초 단위 대기 시간)/(배치 크기 * 단일 쓰기에 사용한 RU)* 수식을 사용합니다.
        
    |속성|값|
    |--------|-----|
    |batchSize| 24 |
    |프로비전된 RU | 10000 |
    |대기 시간 | 0.100s |
    |1개 문서 쓰기에 대해 청구된 RU | 10RU |
    |numInsertionWorkers | ? |
    
    *numInsertionWorkers = (10000 RU x 0.1s) / (24 x 10 RU) = 4.1666*

6. Hello 최종 마이그레이션 명령을 실행 합니다.

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a>다음 단계

Toohello 다음 자습서를 진행 하 고 알아볼 수 있습니다 어떻게 tooquery Azure Cosmos DB를 사용 하 여 MongoDB 데이터입니다. 

> [!div class="nextstepaction"]
>[어떻게 tooquery MongoDB 데이터?](../cosmos-db/tutorial-query-mongodb.md)
