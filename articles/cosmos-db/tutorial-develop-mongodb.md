---
title: "MongoDB toobuild 웹 응용 프로그램에 대 한 API aaaUse Azure Cosmos DB | Microsoft Docs"
description: "MongoDB에 대 한 hello API를 사용 하는 온라인 데이터베이스 웹 앱을 만드는 Azure Cosmos DB 자습서입니다."
keywords: "MongoDB 예제"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 61a2ab3a-2fc3-4d49-a263-ed87c66628f6
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 6dfa7fef49fc53ea2fcfcfbad3b3fcf97ac18e94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a>Azure Cosmos DB:.NET을 사용 하 여 tooa MongoDB 앱 연결

Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다. 신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다. 

이 자습서에서는 방법을 사용 하 여 Azure Cosmos DB 계정을 toocreate hello Azure 포털 및 toocreate 데이터베이스 및 사용 하 여 컬렉션 toostore 데이터의 hello 설명 [MongoDB API](mongodb-introduction.md)합니다. 

이 자습서에서는 hello 다음 작업 방법을 배웁니다.

> [!div class="checklist"]
> * Azure Cosmos DB 계정 만들기 
> * 연결 문자열 업데이트
> * 가상 컴퓨터에 MongoDB 앱 만들기 


## <a name="create-a-database-account"></a>데이터베이스 계정 만들기

Hello Azure 포털에서에서 Azure Cosmos DB 계정을 만들어 보겠습니다.  

> [!TIP]
> * Azure Cosmos DB 계정이 이미 있나요? 이 경우 건너뛰고 너무[Visual Studio 솔루션 설정](#SetupVS)
> * Azure DocumentDB 계정이 있나요? 따라서 사용자 계정이 Azure Cosmos DB 계정인 이제 하 고 건너뛰어도 너무[Visual Studio 솔루션 설정](#SetupVS)합니다.  
> * Hello Azure Cosmos DB 에뮬레이터를 사용 하는 경우 hello 단계에 따르십시오 [Azure Cosmos DB 에뮬레이터](local-emulator.md) toosetup 에뮬레이터 hello 및 너무 건너 뛸[Visual Studio 솔루션 설정](#SetupVS)합니다. 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a>연결 문자열 업데이트

1. Hello hello에서 Azure 포털에서에서 **Azure Cosmos DB** 페이지 MongoDB 계정에 대 한 hello API를 선택 합니다. 
2. Hello 계정 블레이드의 hello 왼쪽된 모음에서 **퀵 스타트**합니다. 
3. 플랫폼(*.NET 드라이버*, *Node.js 드라이버*, *MongoDB 셸*, *Java 드라이버*, *Python 드라이버*)을 선택합니다. 드라이버나 도구가 목록에 없더라도 계속해서 더 많은 연결 코드 조각을 문서화하므로 걱정하지 마세요. 
4. 복사 및 hello 코드 조각 MongoDB 앱에 붙여넣기 toogo 준비 되 고 있습니다.

## <a name="set-up-your-mongodb-app"></a>MongoDB 앱 설치

Hello를 사용할 수 있습니다 [tooMongoDB 가상 컴퓨터에서 실행을 연결 하는 Azure에서 웹 앱을 만들](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tooquickly 설치 MongoDB 응용 프로그램을 최소한의 수정 자습서 (중 하나를 로컬로 또는 게시 된 tooan Azure 웹 앱)를 MongoDB 계정에 대 한 tooan API를 연결합니다.  

1. 하나의 수정 하지 않고도 hello 자습서를 수행 합니다.  Hello Dal.cs 코드를 다음 코드로 바꿉니다.

    ```csharp   
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;
    using System.Security.Authentication;
   
    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            //private MongoServer mongoServer = null;
            private bool disposed = false;
   
            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";
   
            // Default constructor.        
            public Dal()
            {
            }
   
            // Gets all Task items from hello MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }
   
            // Creates a Task and inserts it into hello collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }
   
            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
   
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            # region IDisposable
   
            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }
   
            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                    }
                }
   
                this.disposed = true;
            }
   
            # endregion
        }
    }
    ```

2. Hello 계정 설정에 따라 hello Dal.cs 파일에 있는 변수 hello Azure 포털의에서 hello 키 페이지에서 다음을 수정 합니다.

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. Hello 앱을 사용 하 여!

## <a name="clean-up-resources"></a>리소스 정리

것 toocontinue toouse이이 앱을 하는 경우 단계 toodelete hello Azure 포털에서에서이 자습서에서 만든 모든 리소스를 수행 하는 hello를 사용 합니다. 

1. Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다. 
2. 리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음 작업을 수행 하면:

> [!div class="checklist"]
> * Azure Cosmos DB 계정 만들기 
> * 연결 문자열 업데이트
> * 가상 컴퓨터에 MongoDB 앱 만들기

Toohello 다음 자습서를 진행 한 MongoDB 데이터 tooAzure Cosmos DB를 가져올 수 있습니다.  

> [!div class="nextstepaction"]
> [Azure Cosmos DB로 MongoDB 데이터 가져오기](mongodb-migrate.md)

