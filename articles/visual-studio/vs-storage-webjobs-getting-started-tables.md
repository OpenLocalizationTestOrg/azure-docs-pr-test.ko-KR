---
title: "Azure 저장소 연결 된 Visual Studio 서비스 (WebJob 프로젝트의 경우)와 aaaGetting 시작 됨"
description: "연결 된 서비스를 Visual Studio를 사용 하 여 tooa 저장소 계정을 연결 후 Visual Studio에서 Azure Webjob 프로젝트를 Azure 테이블 저장소를 사용 하 여 tooget을 시작 하는 방법"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 80d9f8d8b493ce612623dfed7e89325fb154a1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a>Azure 저장소 시작(Azure WebJob 프로젝트)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>개요
이 문서에서는 C# 코드 예제에서 보여 주는 보여 어떻게 toouse hello Azure WebJobs SDK 버전을 제공 합니다. Azure 테이블 저장소 서비스 hello로 1.x 합니다. hello 코드 예제는 hello 사용 [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) 버전 1.x 합니다.

hello Azure 테이블 저장소 서비스 사용 하면 많은 양의 구조화 된 데이터를 toostore 있습니다. hello 서비스는 내부 및 외부 hello Azure 클라우드에서 인증 된 호출을 허용 하는 NoSQL 데이터 저장소입니다. Azure 테이블은 구조화된 비관계형 데이터를 저장하는 데 적합합니다.  자세한 내용은 [.NET을 사용하여 Azure 테이블 저장소 시작](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) 을 참조하세요.

일부 hello 코드 조각 표시 hello **테이블** 호출 된 함수를 수동으로, 즉, hello 트리거 특성 중 하나를 사용 하 여에 사용 된 특성입니다.

## <a name="how-tooadd-entities-tooa-table"></a>어떻게 tooadd 엔터티 tooa 테이블
tooadd 엔터티 tooa 테이블을 사용 하 여 hello **테이블** 특성이 **ICollector<T> ** 또는 **IAsyncCollector<T> ** 매개 변수 위치 **T** hello 스키마를 지정 하려는 tooadd hello 엔터티. hello 특성 생성자 hello 테이블의 hello 이름을 지정 하는 문자열 매개 변수를 사용 합니다.

hello 다음 코드 샘플 추가 **사람** 라는 엔터티 tooa 테이블 *수신*합니다.

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() {
                        PartitionKey = "Test",
                        RowKey = i.ToString(),
                        Name = "Name" }
                    );
            }
        }

일반적으로 함께 사용 하면 형식 hello **ICollector** 에서 파생 **TableEntity** 구현 또는 **ITableEntity**, 하지만 필요 하지 않습니다. Hello 다음 중 하나 **사람** 클래스 hello 앞에 표시 된 hello 코드와 작업 **수신** 메서드.

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

원하는 경우 toowork hello Azure 저장소 API 사용 하 여 직접 추가할 수 있습니다는 **CloudStorageAccount** toohello 메서드 서명 매개 변수입니다.

## <a name="real-time-monitoring"></a>실시간 모니터링
데이터 수신 함수 종종 많은 양의 데이터를 처리 하기 때문에 hello WebJobs SDK 대시보드 실시간 모니터링 데이터를 제공 합니다. hello **호출 로그** 섹션에서 설명 하겠습니다 hello 함수가 실행 되 고 계속 하는 경우.

![수신 함수 실행](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

hello **호출 정보** 페이지 hello 함수의 진행률 (작성 하는 엔터티의 수)를 보고 실행 되 고 기회 tooabort을 제공 하는 동안 것입니다.

![수신 함수 실행](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

Hello 함수 완료 되 면 hello **호출 정보** 페이지 hello 작성 된 행 수를 보고 합니다.

![수신 함수 완료](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a>어떻게 tooread 테이블에서 여러 엔터티
tooread 테이블을 사용 하 여 hello **테이블** 특성이 **IQueryable<T> ** 매개 변수를 입력할 수 있는 **T** 에서 파생 **TableEntity**구현 또는 **ITableEntity**합니다.

hello 다음 코드 샘플을 읽고 hello에서 모든 행을 로그 **수신** 테이블:

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}",
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <a name="how-tooread-a-single-entity-from-a-table"></a>어떻게 tooread 테이블에서 단일 엔터티
한 **테이블** 특성 생성자 toobind tooa 단일 테이블 엔터티를 원하는 때 hello 파티션 키와 행 키를 지정할 수 있는 두 개의 추가 매개 변수를 사용 합니다.

hello 다음 코드 샘플 행을 읽고 테이블에 대 한는 **사람** 엔터티의 파티션 키와 행 키 값에 기반 큐 메시지에 수신:  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


hello **사람** 이 예제는 클래스에 tooimplement 없는 **ITableEntity**합니다.

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a>어떻게 toouse hello.NET 저장소 API를 테이블로 직접 toowork
Hello를 사용할 수도 있습니다 **테이블** 특성이 **CloudTable** 개체 작업 테이블을 보다 더 유연 합니다.

hello 다음 코드 예제는 **CloudTable** tooadd 단일 엔터티 toohello 개체 *수신* 테이블입니다.

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

방법에 대 한 자세한 내용은 toouse hello **CloudTable** 개체, 참조 [.NET을 사용 하 여 Azure 테이블 저장소 시작](../storage/storage-dotnet-how-to-use-tables.md)합니다.

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a>Hello 큐 방법 tooarticle에서 포함 된 관련된 항목
어떻게 toohandle 테이블 처리도 트리거된 큐 메시지 또는 WebJobs에 대 한 SDK 시나리오에 대 한 정보에 대 한 특정 tootable 참조 처리 [연결 된 서비스 (WebJob 프로젝트)를 Azure 큐 저장소 및 Visual Studio 시작 ](../storage/vs-storage-webjobs-getting-started-queues.md).

## <a name="next-steps"></a>다음 단계
이 문서에서 코드를 제공 하는 방법을 보여 주는 샘플 toohandle Azure 테이블 작업에 대 한 일반적인 시나리오입니다. Azure WebJobs toouse 및 hello WebJobs SDK를 참조 하는 방법에 대 한 자세한 내용은 [Azure WebJobs 설명서 리소스](http://go.microsoft.com/fwlink/?linkid=390226)합니다.

