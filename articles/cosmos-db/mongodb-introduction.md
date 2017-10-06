---
title: "Cosmos DB 소개 tooAzure: MongoDB에 대 한 API | Microsoft Docs"
description: "짧은 대기 시간 사용 하 여 JSON 문서 쿼리 massive 볼륨이 hello 인기 OSS MongoDB Api 한 Azure Cosmos DB toostore를 사용 하는 방법을 배웁니다."
keywords: "MongoDB 정의"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: anhoh
ms.openlocfilehash: 1eb88014cc4809332e3f5c109a44a55814194934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-api-for-mongodb"></a>Cosmos DB 소개 tooAzure: MongoDB에 대 한 API

[Azure Cosmos DB](../cosmos-db/introduction.md)는 업무에 중요한 응용 프로그램에 대한 Microsoft의 전역 분산 다중 모델 데이터베이스 서비스입니다. Azure Cosmos DB에는 [턴키 글로벌 메일](distribute-data-globally.md), [처리량 및 저장소의 탄력적인 크기 조정을](partition-data.md) hello 99 번째 백분위 수 전 세계, 자리 밀리초 대기 [5 개 잘 정의 된 일관성 수준이](consistency-levels.md), 모두 만족할된 높은 가용성을 보장할 수 [업계를 주도하 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)합니다. Azure Cosmos DB [데이터를 자동으로 인덱싱됩니다](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) toodeal 스미카 및 인덱스 관리를 요구 하지 않고 있습니다. 또한 다중 모델 방식이며, 문서, 키-값, 그래프 및 열 형식 데이터 모델을 지원합니다. 

![Azure Cosmos DB: MongoDB API](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Cosmos DB 데이터베이스 용으로 작성 된 앱에 대 한 hello 데이터 저장소로 사용할 수 있습니다 [MongoDB](https://docs.mongodb.com/manual/introduction/)합니다. 즉, 이제 MongoDB용으로 작성된 응용 프로그램이 기존 [드라이버](https://docs.mongodb.org/ecosystem/drivers/)를 사용하여 Cosmos DB와 통신하고 MongoDB 데이터베이스 대신 Cosmos DB 데이터베이스를 사용할 수 있습니다. 대부분의 경우에서 단순히 연결 문자열을 변경 하 여 MongoDB tooCosmos DB를 사용 하 여 전환할 수 있습니다. 이 기능을 사용 하 여 쉽게 작성할 수 있습니다 및 hello Azure에서에서 실행된 MongoDB 데이터베이스 응용 프로그램 Azure Cosmos DB 글로벌 배포와 함께 클라우드 및 [포괄적인 업계의 선두적인 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db), 친숙 한 toouse 줄이면서 기술 및 MongoDB에 대 한 도구입니다.


## <a name="what-is-hello-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>MongoDB 응용 프로그램에 대 한 Azure Cosmos DB를 사용 하는 hello 이점은 무엇입니까?

**탄력적으로 확장 가능한 처리량 및 저장소:** 쉽게 확장 하거나 MongoDB 데이터베이스 toomeet 아래로 응용 프로그램에 필요 합니다. 데이터는 예측 가능한 낮은 대기 시간을 위해 SSD(반도체 드라이브)에 저장됩니다. Cosmos DB 지원 toovirtually 확장할 수 있는 MongoDB 컬렉션 프로 비전 된 처리량 및 무제한 저장소 크기입니다. 응용 프로그램 증가에 따라 탄력적으로 Cosmos DB를 확장하고 매끄럽게 예측 가능한 성능을 얻을 수 있습니다. 

**다중 지역 복제:** Cosmos DB toodevelop 필요한 응용 프로그램에 대 한 전역 액세스 toodata 간 균형을 제공 하면서 있도록 MongoDB 계정과 관련 한 사용자 데이터 tooall 영역을 투명 하 게 복제 일관성, 가용성 및 성능 보장은 해당 포함 된 모두 합니다. Cosmos DB hello 전세계 멀티 호 밍 Api hello 기능 tooelastically 배율 처리량 및 저장소 지역 투명 한 장애 조치를 제공합니다. [데이터를 글로벌 배포](distribute-data-globally.md)에 대한 자세한 정보

**MongoDB 호환성**: 기존 MongoDB 전문 지식, 응용 프로그램 코드 및 도구를 사용할 수 있습니다. MongoDB를 사용 하 여 응용 프로그램을 개발 하 고 tooproduction 배포할지 전 세계적으로 분산된 Cosmos DB 서비스에 관리 되는 hello를 사용 하 여 완벽 하 게 합니다.

**서버 관리도 없고**: 없습니다 toomanage 고 MongoDB 데이터베이스의 크기를 조정 합니다. Cosmos DB 없는 toomanage 인프라 또는 가상 컴퓨터 사용자가 직접 즉 완전히 관리 되는 서비스입니다. Cosmos DB는 30개 이상의 [Azure 지역](https://azure.microsoft.com/regions/services/)에서 사용할 수 있습니다.

**튜닝할 수 있는 일관성 수준:** 5에서 Select 일관성 수준 tooachieve 일관성과 성능 간에 최적의 균형을 잘 정의 합니다. 쿼리 및 읽기 작업에 대해 Cosmos DB는 강력, 제한된 부실, 세션, 일관된 접두사, 최종의 5가지 일관성 수준을 제공합니다. 이러한 세부적인, 잘 정의 된 일관성 수준 toomake 사운드 간의 장단점 일관성, 가용성 및 대기 시간을 허용 합니다. 자세한 내용을 알아보세요 [toomaximize 가용성 및 성능 수준 일관성을 사용 하 여](consistency-levels.md)합니다.

**자동 인덱싱을**: 기본적으로 Cosmos DB 자동으로 MongoDB 데이터베이스에서 문서 내에서 모든 hello 속성 인덱스 예상 되거나 않는 스키마 또는 보조 인덱스의 만들기 필요 합니다.

**엔터프라이즈급** -Azure Cosmos DB 지역 및 영역 오류의 hello 표면에서 여러 로컬 복제본 toodeliver 99.99% 가용성 및 데이터 보호를 지원 합니다. Azure Cosmos DB에는 엔터프라이즈급 [규정 준수 인증서](https://www.microsoft.com/trustcenter) 및 보안 기능이 있습니다. 

Scott Hanselman과 Azure Cosmos DB 수석 엔지니어링 관리자 Kirill Gavrylyuk이 진행하는 이 Azure Friday 비디오를 통해 자세한 내용을 알아보세요.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Azure-Cosmos-DB/player]
> 

## <a name="how-tooget-started"></a>Tooget 시작 하는 방법

Hello MongoDB 퀵 스타트 toocreate Cosmos DB 계정 및 따르거나 프로그램 기존 Mongo DB 응용 프로그램 toouse Cosmos DB 마이그레이션 새 빌드:

* [기존 Node.js MongoDB 웹앱 마이그레이션](create-mongodb-nodejs.md)
* [.NET 및 Azure 포털 hello MongoDB API 웹 응용 프로그램을 빌드하십시오.](create-mongodb-dotnet.md)
* [Java 및 Azure 포털 hello MongoDB API 콘솔 응용 프로그램 빌드](create-mongodb-java.md)

## <a name="next-steps"></a>다음 단계

Azure Cosmos DB MongoDB API에 대 한 정보는 전체 Azure Cosmos DB 설명서 hello에 통합 되어 있지만 시작 하는 몇 가지 포인터 tooget 다음과 같습니다.

* Hello에 따라 [tooa MongoDB 계정을 연결](connect-mongodb-account.md) 자습서 toolearn 어떻게 tooget 계정 연결 문자열 정보입니다.
* Hello에 따라 [Azure Cosmos DB와 함께 사용 하 여 MongoChef](mongodb-mongochef.md) 자습서 toolearn 어떻게 toocreate Azure Cosmos DB 데이터베이스 및 MongoChef에서 MongoDB 응용 프로그램 간의 연결입니다.
* Hello에 따라 [MongoDB에 대 한 프로토콜 지원 포함 데이터 tooAzure Cosmos DB 마이그레이션할](mongodb-migrate.md) 자습서 tooimport MongoDB 데이터베이스에 대 한 사용자 데이터 tooan API입니다.
* 사용 하 여 계정을 MongoDB에 대 한 tooan API 연결 [Robomongo](mongodb-robomongo.md)합니다.
* 개수 RUs hello로 사용 하는 작업에 알아봅니다 [GetLastRequestStatistics 명령 및 Azure 포털 메트릭 hello](request-units.md#GetLastRequestStatistics)합니다.
* 너무 방법에 대해 알아봅니다[세계적으로 분산 된 응용 프로그램에 대 한 읽기 기본 설정을 구성](../cosmos-db/tutorial-global-distribution-mongodb.md)합니다.
