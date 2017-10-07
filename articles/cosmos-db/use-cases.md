---
title: "aaaCommon 사례와 시나리오를 사용 하 여 Azure Cosmos db | Microsoft Docs"
description: "Hello 상위 5 개 사례를 사용 하 여 Azure Cosmos DB에 대 한 알아봅니다: 사용자 생성 콘텐츠, 이벤트 로깅, 카탈로그 데이터, 사용자 기본 설정 데이터 및 인터넷 IoT (사물)."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: eca68a58-1a8c-4851-8cf8-6e4d2b889905
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: mimig
ms.openlocfilehash: 115a418e7b18d5033c4d7e64591bf302aea0190b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="common-azure-cosmos-db-use-cases"></a>일반적인 Azure Cosmos DB 사용 사례
이 문서에서는 Azure Cosmos DB의 몇 가지 일반적인 사용 사례를 간략하게 설명합니다.  이 문서에서 권장 하는 hello Cosmos DB와 함께 응용 프로그램을 개발할 때 시작 지점으로 사용 됩니다.   

이 문서를 읽은 후 다음 질문 수 tooanswer hello 수 있습니다. 

* Hello Azure Cosmos DB에 대 한 일반적인 사용 사례는 무엇입니까?
* 소매 응용 프로그램에 대 한 Azure Cosmos DB를 사용 하 여 hello 장점은 무엇입니까?
* 데이터 저장소로 Azure Cosmos DB를 사용 하 여 인터넷 IoT (사물) 시스템에 대 한 hello 장점은 무엇입니까?
* 웹 및 모바일 응용 프로그램에 대 한 Azure Cosmos DB를 사용 하 여 hello 장점은 무엇입니까?

## <a name="introduction"></a>소개
[Azure Cosmos DB](../cosmos-db/introduction.md)는 전 세계에 배포된 Microsoft 데이터베이스 서비스입니다. hello 서비스는 디자인 된 tooallow 고객 tooelastically (및 독립적으로) 지리적 영역 수 전체 처리량 및 저장소의 크기를 조정 합니다. Azure Cosmos 데이터베이스 hello 시장 오늘 toooffer 포괄적인 hello 첫 번째 세계적으로 분산 된 데이터베이스 서비스는 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/cosmos-db/) 처리량, 대기 시간, 가용성 및 일관성을 포괄 합니다. 

hello Azure Cosmos DB 프로젝트 2011에서 같이 시작 "프로젝트 Florence" tooaddress 개발자-문제점 Microsoft 내부 대규모 인터넷 규모 응용 프로그램 때 직면 하는입니다. 이러한 문제는 고유 tooMicrosoft 응용 프로그램이 아니기, 하기로 결정 toomake Azure Cosmos DB 일반 공급 tooexternal 개발자의 hello 형태로 2015 관찰 [Azure DocumentDB](https://azure.microsoft.com/blog/documentdb-moving-to-general-availability/)합니다. hello 서비스 보편적 내부적으로 사용 되며 Microsoft 내의 및 개발자가 Azure 외부에서 사용 하는 hello 급성장 서비스 중 하나입니다. 

Azure Cosmos DB는 광범위한 응용 프로그램 및 사용 사례에서 사용되는, 전역으로 분산된 다중 모델 데이터베이스입니다. 에 대 한는 것이 좋습니다 [서버가 없는](http://azure.com/serverless) 낮은 밀리초 주문 응답 시간이 필요 하 고 신속 하 게 그리고 전 세계적으로 tooscale 필요한 응용 프로그램입니다. 여러 데이터 모델(키-값, 문서, 그래프 및 칼럼 형식) 및 [MongoDB](mongodb-introduction.md), [DocumentDB SQL](documentdb-introduction.md), [Gremlin](graph-introduction.md), [Azure Tables](table-introduction.md) 등의 많은 데이터 액세스용 API를 기본적으로, 그리고 확장 가능한 방식으로 지원합니다. 

hello Azure Cosmos DB의 글로벌 목표가 있는 고성능 응용 프로그램에 적합 하는 일부 특성에는 합니다.

* Azure Cosmos DB는 기본적으로 고가용성 및 확장성을 위해 데이터를 분할합니다. Azure Cosmos DB는 99.99%의 가용성, 처리량, 짧은 대기 시간 및 일관성을 보장합니다.
* Azure Cosmos DB에는 낮은 대기 시간의 응답 시간(밀리초)을 지원하는 SSD 지원 저장소가 있습니다.
* Azure Cosmos DB는 최종, 일관된 접두사, 세션, 제한된 부실 등의 일관성 수준을 지원하므로 완전한 유연성과 성능 대비 낮은 비용이 제공됩니다. 수준 일관성에서 Azure Cosmos DB만큼 큰 유연성을 제공하는 데이터베이스 서비스는 없습니다. 
* Azure Cosmos DB에는 저장소 및 처리량을 독립적으로 측정하는, 유연하고 데이터 친화적인 가격 책정 모델이 있습니다.
* Azure Cosmos DB의 예약 된 처리량 모델 toothink을 hello 기반 하드웨어의 CPU/메모리/IOPs 대신 읽기/쓰기 수 있습니다.
* Azure Cosmos DB 디자인 하면 toomassive 요청 볼륨의 크기를 조정 hello 일별 요청 수조의의 순서입니다.

이러한 특성은 웹, 모바일, 하는 데에서 유용 게임 및 IoT 응용 프로그램을 짧은 응답 시간 하며 toohandle 읽기 및 쓰기의 양이 필요 합니다.

## <a name="iot-and-telematics"></a>IoT 및 텔레매틱스
IoT 사용 사례는 일반적으로 데이터를 수집, 처리 및 저장하는 방법에서 일부 패턴을 공유합니다.  첫째, 이러한 시스템 로캘 다양 한 장치 센서에서 데이터의 tooingest 버스트 필요 합니다. 다음으로 이러한 시스템을 처리 하 고 스트리밍 데이터 tooderive 실시간 정보를 분석 합니다. hello 데이터는 다음 일괄 처리 분석에 대 한 toocold 저장소에 보관 합니다. Microsoft Azure 제품은 Azure Cosmos DB, Azure Event Hubs, Azure Stream Analytics, Azure Notification Hub, Azure Machine Learning, Azure HDInsight 및 PowerBI를 비롯한 IoT 사용 사례에 적용할 수 있는 다양한 서비스를 제공합니다. 

![Azure Cosmos DB IoT 참조 아키텍처](./media/use-cases/iot.png)

Azure Event Hubs는 짧은 대기 시간으로 높은 처리량 데이터 수집을 제공하기 때문에 데이터 버스트를 수집할 수 있습니다. 실시간 통찰력에 대 한 처리 toobe는 수집 된 데이터에 대 한 실시간 분석 보내집니다 tooAzure 스트림 분석 될 수 있습니다. 임시 쿼리를 위해 데이터를 Azure Cosmos DB에 로드할 수 있습니다. Hello 데이터 Azure Cosmos DB에 로드 되 면 hello 데이터는 쿼리 준비 toobe입니다. 또한 새 데이터와 변경 내용 tooexisting 데이터 변경 피드를 읽을 수 있습니다. 변경 피드는 영구, 로그를 저장 하는 순서 대로 tooCosmos DB 컬렉션 변경만 추가 합니다. hello 모든 데이터 또는 Azure Cosmos DB에만 변경 내용이 toodata 실시간 분석의 일환으로 참조 데이터로 사용할 수 있습니다. 또한 데이터 더욱 수 구체화 하 고 Pig, Hive, 또는 Map/Reduce 작업에 대 한 Azure Cosmos DB 데이터 tooHDInsight 연결에서 처리 합니다.  구체화 된 해당 데이터 로드 백 tooAzure Cosmos DB 보고 합니다.   

Azure Cosmos DB, EventHubs 스톰을 사용 하 여 샘플 IoT 솔루션에서 참조 hello [GitHub의 리포지토리 hdinsight-스톰-예제](https://github.com/hdinsight/hdinsight-storm-examples/)합니다.

IoT에 대 한 Azure 옵션에 대 한 자세한 내용은 참조 하십시오. [만들기 hello Your 사물 인터넷](http://www.microsoft.com/server-cloud/internet-of-things.aspx)합니다. 

## <a name="retail-and-marketing"></a>소매 및 마케팅
Azure Cosmos DB hello Windows 스토어 및 XBox Live 실행 하는 Microsoft의 전자 상거래 플랫폼에서 광범위 하 게 사용 됩니다. 또한 카탈로그 데이터를 저장 하 고 파이프라인을 처리 하는 순서로 소싱 이벤트에 대 한 hello 소매 업계에 사용 됩니다.

카탈로그 데이터 사용 시나리오에는 사용자, 장소 및 제품과 같은 엔터티의 특성 집합 저장 및 쿼리가 포함됩니다. 카탈로그 데이터의 몇 가지 예로 사용자 계정, 제품 카탈로그, IoT 장치 레지스트리, BOM 시스템 등이 있습니다. 다 수 toofit 응용 프로그램 요구 사항 시간이 지나면서 달라질 수 있으며,이 데이터에 대 한 특성입니다.

제품 카탈로그의 예로 자동차 부품 공급업체를 고려해 보세요. 모든 부분에서 모든 부분을 공유 하는 추가 toohello 공통 특성 마다 고유한 특성 있을 수 있습니다. 또한 특정 부분에 대 한 특성 hello 다음 새 모델 해제 될 때 연도 변경할 수 있습니다. Azure Cosmos DB는 유연한 스키마와 계층형 데이터를 지원하므로 제품 카탈로그 데이터를 저장하는 데 적합합니다.

![Azure Cosmos DB 소매 카탈로그 참조 아키텍처](./media/use-cases/product-catalog.png)

소싱 toopower 이벤트 기반 아키텍처를 사용 하 여 이벤트에 대 한 azure Cosmos DB는 대개 해당 [피드 변경](change-feed.md) 기능입니다. hello 변경 피드 다운스트림 microservices 기능 tooreliably hello 및 증분 읽기 삽입 및 업데이트 (예를 들어 주문 이벤트) tooan Azure Cosmos DB를 제공 합니다. 이 기능은 사용된 tooprovide 드라이브 주문 처리 워크플로의 많은 microservices 사이 및 상태 변경 이벤트에 대 한 메시지 브로커로 영구 이벤트를 저장할 수 있습니다 (으로 구현할 수 있는 [서버가 없는 Azure 함수](http://azure.com/serverless)).

![Azure Cosmos DB 주문 파이프라인 참조 아키텍처](./media/use-cases/event-sourcing.png)

뿐만 아니라 Azure Cosmos DB에 저장된 데이터는 Apache Spark 작업을 통해 빅 데이터 분석에 사용되는 HDInsight와 통합할 수 있습니다. Hello Azure Cosmos DB 용 Spark 커넥터에 대 한 세부 정보를 참조 하십시오. [Cosmos DB 및 HDInsight Spark 작업 실행](spark-connector.md)합니다.

## <a name="gaming"></a>게임
hello 데이터베이스 계층은 게임 응용 프로그램의 중요 한 구성입니다. 최신 게임 모바일/콘솔 클라이언트에서 그래픽 처리를 수행 하지만 사용자 지정 하는 hello 클라우드 toodeliver 고려 게임의 통계, 소셜 미디어 통합 및 높은 점수 순위표 콘텐츠와 같은 고. 게임은 종종 읽기에 대 한 단일 밀리초 대기 시간이 필요 하 고 흥미로운 게임에서 경험 tooprovide를 씁니다. 게임 데이터베이스 빠른 toobe 하며 게임 실행 하는 경우 새 및 기능 업데이트 하는 동안 요청 속도 수 toohandle massive 스파이크 여야 합니다.

Azure Cosmos DB와 같은 게임에서 사용 되 [데드 도보 hello: No 매뉴얼 토지](https://azure.microsoft.com/blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/) 여 [다음 게임](http://www.nextgames.com/), 및 [Halo 5: 보호자](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/)합니다. Azure Cosmos DB hello 다음 toogame 개발자 혜택을 제공 합니다.

* Azure Cosmos DB 크기가 조정 되는 성능 toobe를 사용 하면를 위나 아래로 탄력적으로 합니다. 이 통해 게임 toohandle 프로필 및 수십 개의에서 통계 업데이트의 단일 API 호출 하 여 동시 게이머 toomillions 합니다.
* 게임 중 모든 시퀀스 번호 보다 낮은 방지 하는 밀리초를 읽고 쓰는 toohelp azure Cosmos DB 지원 합니다.
* Azure Cosmos DB의 자동 인덱싱은 여러 속성에 대한 실시간 필터링을 지원합니다. 예를 들어 내부 플레이어 ID로 플레이어를 찾거나 GameCenter, Facebook, Google ID 또는 플레이드의 길드 멤버 자격에 따른 쿼리로 플레이어를 찾을 수 있습니다. 이는 복잡한 인덱싱을 작성하거나 인프라를 분할하지 않고도 가능합니다.
* 게임 내 채팅 메시지, 플레이어 길드 멤버 자격, 인증 완료할 높은 점수 순위표 소셜 그래프를 비롯 한 소셜 기능 유연한 스키마와 함께 보다 쉽게 tooimplement 됩니다.
* 관리 되는 플랫폼으로-서비스 (PaaS)로 azure Cosmos DB 필요한 최소한의 설치 및 관리 작업 tooallow 신속 하 게 반복 하 고 시간 toomarket를 줄입니다.

![Azure Cosmos DB 게임 참조 아키텍처](./media/use-cases/gaming.png)

## <a name="web-and-mobile-applications"></a>웹 및 모바일 응용 프로그램
Azure Cosmos DB는 일반적으로 웹 및 모바일 응용 프로그램 내에서 사용되며 소셜 상호 작용을 모델링하여 타사 서비스와 통합하고 풍부한 개인 설정 환경을 빌드하는 데 적합합니다. 빌드를 사용 하는 풍부한 iOS 및 Android 응용 프로그램 인기 있는 hello를 사용 하 여 hello Cosmos DB Sdk 수 [Xamarin 프레임 워크](mobile-apps-with-xamarin.md)합니다.  

### <a name="social-applications"></a>소셜 응용 프로그램
Azure Cosmos DB에 대 한 일반적인 사용 사례에서는 toostore 및 쿼리 사용자 생성 콘텐츠 (UGC) 웹, 모바일 및 소셜 미디어 응용 프로그램입니다. UGC의 몇 가지 예로 채팅 세션, 트윗, 블로그 게시물, 평가, 의견 등이 있습니다. 종종, 소셜 미디어 응용 프로그램에 UGC hello는 자유 형식 텍스트, 속성, 태그 및 고정 된 관계로 구조에 의해 제한 되지 않습니다는 관계의 blend입니다. 채팅 등의 콘텐츠, 설명 및 게시물 저장할 수 있습니다 Cosmos db에서 변환 또는 복합 개체 toorelational 매핑 계층을 요구 하지 않고.  추가 될 수 있습니다 하 든 개발자 따라서 신속 하 게 개발을 촉진 hello 응용 프로그램 코드에서 반복 하는 대로 toomatch 요구 사항을 쉽게 수정 하는 데이터 속성입니다.  

제 3 자 소셜 네트워크와 통합 하는 응용 프로그램에서 이러한 네트워크 toochanging 스키마 응답 해야 합니다. Cosmos DB에는 기본적으로 데이터가 자동으로 인덱싱될 데이터의 준비 toobe 언제 든 지 쿼리 됩니다. 이러한 응용 프로그램 이미 각각의 요구에 따라 hello 유연성 tooretrieve 프로젝션 합니다.

대부분의 hello 소셜 응용 프로그램 글로벌 규모에 실행 하 고 예측할 수 없는 사용 패턴을 제공 합니다. Hello 데이터 저장소의 크기를 조정 유연성은 hello 응용 프로그램 계층 toomatch 사용 필요를 따라 확장이 동일 하거나 유사 해야 합니다.  Cosmos DB 계정으로 데이터 파티션을 더 추가하여 규모를 확장할 수 있습니다.  또한 여러 지역에 추가 Cosmos DB 계정을 만들 수도 있습니다. Cosmos DB 서비스 지역 가용성은 [Azure 지역](https://azure.microsoft.com/regions/#services)을 참조하세요.

![Azure Cosmos DB 웹앱 참조 아키텍처](./media/use-cases/apps-with-global-reach.png)

### <a name="personalization"></a>개인 설정
오늘날 최신 응용 프로그램은 복잡한 뷰와 환경으로 제공됩니다. 이들은 toouser 기본 설정 또는 분위기 출장 및 요구 사항을 브랜드 동적 일반적으로입니다. 따라서 응용 프로그램 필요 toobe 수 tooretrieve 개인 설정 효과적으로 toorender UI 요소 및 환경을 신속 하 게 합니다. 

JSON, Cosmos DB에서 지원 되는 형식 레이아웃 데이터는 유효한 서식 toorepresent UI는은 간단 하지만 쉽게 해석할 수 JavaScript에서. Cosmos DB는 빠른 읽기 및 대기 시간이 짧은 쓰기를 허용하는 조정 가능한 일관성 수준을 제공합니다. 따라서 hello 네트워크를 통해 UI 레이아웃 데이터 Cosmos DB에서 JSON 문서는 효율적 tooget 사용자 개인된 설정을 포함 하 여이 데이터를 저장 합니다.

![Azure Cosmos DB 웹앱 참조 아키텍처](./media/use-cases/personalization.png)

## <a name="next-steps"></a>다음 단계
Azure Cosmos DB 시작 tooget 따라 우리의 [빠른 시작](create-documentdb-dotnet.md), 계정 및 Cosmos DB 시작을 만드는 과정을 안내 하 합니다. 

또는, tooread Cosmos DB를 사용 하는 고객에 대 한 자세한, 원하는 경우 hello 다음 고객 스토리를 사용할 수 있습니다.

* [Jet.com](https://jet.com). 전자 상거래도 전자 눈 hello 상위 자리, hello Microsoft 클라우드에서 실행, Cosmos DB 세계적인 규모에 활용 합니다.
* [Asos.com](http://www.asos.com/). Asos.com은 영국의 온라인 패션/미용 상점입니다. 청년층을 주 고객으로 하는 Asos는 850개 이상의 브랜드와 자체 의류 및 액세서리를 판매합니다.
* [Toyota](https://www.toyota.com/). Toyota Motor Corporation은 일본 자동차 제조업체입니다. Toyota는 글로벌 IoT 앱을 위해 Cosmos DB를 활용합니다.
* [Citrix](https://customers.microsoft.com/story/citrix). Citrix는 Azure Service Fabric 및 Azure Cosmos DB를 사용하여 Single-Sign-On 솔루션을 개발합니다.
* [TEXA](https://customers.microsoft.com/story/texaspa) 차량 소유자를 위한 TEXA의 혁신적인 IoT 솔루션은 시간, 비용, 휘발유 절감뿐 아니라 생명을 구하는 데에도 도움이 됩니다.
* [Domino's Pizza](https://www.dominos.com). Domino's Pizza Inc.는 미국 체인 피자점입니다.
* [Johnson Controls](http://www.johnsoncontrols.com). Johnson Controls는 150개 이상의 국가에서 다양한 고객에게 서비스를 제공하는 글로벌 분산 기술 및 다중 산업 리더입니다.
* [Microsoft Windows, Universal Store, Azure IoT Hub, Xbox Live 및 기타 인터넷 규모 서비스](https://azure.microsoft.com/blog/how-azure-documentdb-planet-scale-nosql-helps-run-microsoft-s-own-businesses/). Microsoft에서 Azure Cosmos DB를 사용하여 확장성이 뛰어난 서비스를 빌드하는 방법입니다.
* [Microsoft 데이터 및 분석 팀](https://customers.microsoft.com/story/microsoftdataandanalytics)합니다. Microsoft 데이터 및 분석 팀은 Azure Cosmos DB를 사용하여 글로벌 규모의 빅 데이터 컬렉션을 얻습니다.
* [Sulekha.com](https://customers.microsoft.com/story/sulekha-uses-azure-documentdb-to-connect-customers-and-businesses-across-india). Sulekha 인도 Azure Cosmos DB tooconnect 고객 및 비즈니스 사용합니다.
* [NewOrbit](https://customers.microsoft.com/story/neworbit-takes-flight-with-azure-documentdb). NewOrbit는 Azure Cosmos DB를 사용하여 비행합니다.
* [Affinio](https://customers.microsoft.com/doclink/affinio-switches-from-aws-to-azure-documentdb-to-harness-social-data-at-scale). Affinio는 AWS tooAzure 규모로 Cosmos DB tooharness 소셜 데이터에서에서 전환합니다.
* [Next Games](https://azure.microsoft.com//blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/). hello Walking 배달: No 매뉴얼 정 토지 게임 soars 너무 # 1에서 지 원하는 Azure Cosmos DB입니다.
* [Halo](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). Halo 5에서 Azure Cosmos DB를 사용하여 소셜 게임 플레이를 구현한 방식입니다.
* [Cortana 분석 갤러리](https://azure.microsoft.com/blog/cortana-analytics-gallery-a-scalable-community-site-built-on-azure-documentdb/). Cortana 분석 갤러리 - Azure Cosmos DB를 기반으로 하는 확장 가능한 커뮤니티 사이트입니다.
* [Breeze](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18602). 선도적인 통합자가 유연한 클라우드 기술을 사용하여 수분 내에 다국적 기업에 글로벌 통찰력을 제공합니다.
* [News Republic](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18639). 인텔리전스 toohello 뉴스 tooprovide 용도 대 한 정보 높은 거주자를 추가합니다. 
* [SGS International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18653). Hello 전세계 일관 된 색에 대 한 주요 카드 브랜드 tooSGS를 설정합니다. SG tooAzure 설정 됩니다.
* [Telenor](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18608). 전역 리더 Telenor 시작을 hello 속도가 클라우드 toomove hello를 사용합니다. 
* [XOMNI](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18667). 빠른 검색 및 hello 쉽게의 데이터 흐름에서 향후 실행 (hello)의 hello 저장소입니다.
* [Nucleo](https://customers.microsoft.com/story/azure-based-software-platform-breaks-down-barriers-bet). Azure 기반 소프트웨어 플랫폼은 비즈니스와 고객 간의 장벽을 없앱니다.
* [Weka](https://customers.microsoft.com/story/weka-smart-fridge-improves-vaccine-management-so-more-people-can-be-protected-against-diseases). Weka Smart Fridge는 보다 많은 사람들을 질병으로부터 보호할 수 있도록 개선된 백신 관리 기능을 제공합니다.
* [Orange Tribes](https://customers.microsoft.com/story/theres-more-to-that-food-app-than-meets-the-eye-or-the-mouth). 보다 많은 toothat 음식 앱 hello 눈 또는 hello 입 숨겨진 있습니다.
* [Real Madrid](https://customers.microsoft.com/story/real-madrid-brings-the-stadium-closer-to-450-million-f). 실제 마드리드 경기장 자세히 too450 백만 팬 속도 hello Microsoft 클라우드로 hello 세계 hello를 제공합니다.
* [Tuku](https://customers.microsoft.com/story/tuku-makes-car-buying-fun-with-help-from-azure-services). TUKU는 Azure 서비스의 도움으로 차를 구입하는 재미를 줍니다.
