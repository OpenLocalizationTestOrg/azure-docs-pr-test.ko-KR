---
title: "aaaAzure 이벤트 표 형태 개요"
description: "Azure Event Grid 및 해당 개념을 설명합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a>소개 tooAzure 이벤트 표 형태

Azure 이벤트 표 형태 이벤트 기반 아키텍처를 가진 응용 프로그램을 tooeasily 작성할 수 있습니다. Hello, toosubscribe 선택한 hello 이벤트 처리기 또는 WebHook 끝점 toosend hello 이벤트를 제공 하는 Azure 리소스를 선택 합니다. Event Grid는 기본적으로 저장소 Blob 및 리소스 그룹과 같은 Azure 서비스의 이벤트를 지원합니다. 또한 Event Grid는 사용자 지정 토픽 및 사용자 지정 웹후크를 사용하여 응용 프로그램 및 타사 이벤트에 대한 사용자 지정을 지원합니다. 

필터 tooroute 특정 이벤트 toodifferent 끝점, 멀티 캐스트 toomultiple 끝점을 사용할 수 있으며 이벤트 안정적으로 배달 되 고 있는지 확인 하십시오. Event Grid에는 기본적으로 사용자 지정 및 타사 이벤트를 지원합니다.

이벤트 표 형태 hello 미리 보기 릴리스에 대 한 지원 **westus2** 및 **westcentralus** 위치입니다. 다른 지역이 추가됩니다.

이 문서는 Azure Event Grid의 개요를 제공합니다. 이벤트 표 형태 시작 tooget 참조 [Azure 이벤트 표 형태를 사용자 지정 이벤트 만들기 및 경로](custom-event-quickstart.md)합니다.

![Event Grid 기능 모델](./media/overview/event-grid-functional-model.png)

현재, Blob Storage는 게시자로 공개적으로 사용할 수 없습니다.

## <a name="concepts"></a>개념

이제부터 살펴볼 Azure Event Grid의 5가지 개념은 다음과 같습니다.

* **이벤트** - 발생한 내용입니다.
* **이벤트 원본/게시자** -hello 이벤트 발생 하는 경우.
* **항목** -hello 게시자가 이벤트를 보낼 끝점입니다.
* **이벤트 가입** -hello 끝점 또는 기본 제공 메커니즘 tooroute 이벤트, 경우에 따라 toomultiple 처리기입니다. 구독도 처리기 toointelligently 필터 들어오는 이벤트에 의해 사용 됩니다.
* **이벤트 처리기** -앱 hello 또는 응답할 toohello 이벤트를 서비스 합니다.

이러한 개념에 대한 자세한 내용은 [Azure Event Grid의 개념](concepts.md)을 참조하세요.

## <a name="capabilities"></a>기능

다음은 이벤트 표 형태 Azure의 hello 주요 기능 중 일부입니다.

* **단순성** -Azure 리소스 tooany 이벤트 처리기 또는 끝점에서 tooaim 이벤트 가리키고 클릭 합니다.
* **고급 필터링** -이벤트에 대 한 필터 유형 또는 이벤트 게시 경로 tooensure 이벤트 처리기만 관련 이벤트를 수신 합니다.
* **팬 아웃** -여러 끝점 toohello 구독 동일한 이벤트 toosend 복사 hello 이벤트 tooas의 여러 위치 필요에 따라 합니다.
* **안정성** -이벤트가 전달 되는 지 수 백오프 tooensure로 재시도 24 시간제를 사용 합니다.
* **사용량 기준 과금 이벤트별** -지불 하는 hello 금액에 대 한 이벤트 표 형태를 사용 합니다.
* **높은 처리량** - 초당 수백만 개 이벤트 지원을 통해 Event Grid에서 대량 워크로드를 빌드합니다.
* **기본 제공 이벤트** - 리소스 정의 기본 제공 이벤트를 사용하여 신속하게 준비하고 실행합니다.
* **사용자 지정 이벤트** - Event Grid를 사용하여 사용자 앱의 사용자 지정 이벤트를 라우팅하고, 필터링하며, 안정적으로 배달합니다.

## <a name="built-in-publisher-and-handler-integration"></a>기본 제공 게시자 및 처리기 통합

Azure는 게시자 및 처리기를 모두 포함한 다양한 서비스를 사용하는 기본 제공 이벤트 지원을 제공합니다.

### <a name="publishers"></a>게시자

현재 hello 다음 Azure 서비스가 있는 이벤트 표 형태에 대 한 기본 제공 된 게시자 지원:

* 리소스 그룹(관리 작업)
* Azure 구독(관리 작업)
* Event Hubs
* 사용자 지정 토픽

올해 다른 Azure 서비스가 추가될 예정입니다.

### <a name="handlers"></a>처리기

현재 hello 다음 Azure 서비스가 있는 이벤트 표 형태에 대 한 기본 제공 처리기 지원: 

* Azure 기능
* Logic Apps
* Azure Automation
* 웹후크

올해 다른 Azure 서비스가 추가될 예정입니다.

## <a name="what-can-i-do-with-event-grid"></a>Event Grid로 할 수 있는 작업은 무엇인가요?

Azure Event Grid는 서버를 사용하지 않는 작업 자동화 및 통합 작업을 크게 개선하는 여러 기능을 제공합니다. 

### <a name="serverless-application-architectures"></a>서버를 사용하지 않는 응용 프로그램 아키텍처

![서버를 사용하지 않는 응용 프로그램](./media/overview/serverless_web_app.png)

Event Grid는 데이터 원본과 이벤트 처리기를 연결합니다. 예를 들어 새 사진을 때마다 tooa blob 저장소 컨테이너를 추가 하는 서버가 없는 함수 toorun 이미지 분석 이벤트 표 형태 tooinstantly 트리거를 사용 합니다. 

### <a name="ops-automation"></a>작업 자동화

![작업 자동화](./media/overview/Ops_automation.png)

이벤트 표 형태 toospeed 자동화를 지원 하 고 정책 적용을 간소화 합니다. 예를 들어 Event Grid는 가상 컴퓨터가 만들어지거나 SQL Database가 실행되면 Azure Automation에 알릴 수 있습니다. 이러한 이벤트를 사용할 수 있습니다 tooautomatically에 있는지 확인 서비스 구성, 운영 도구, 태그 가상 컴퓨터 또는 작업 항목 파일에 메타 데이터를 배치 합니다.

### <a name="application-integration"></a>응용 프로그램 통합

![응용 프로그램 통합](./media/overview/app_integration.png)

Event Grid는 앱을 다른 서비스와 연결합니다. 예를 들어 사용자 지정 항목 toosend 응용 프로그램의 이벤트 데이터 tooEvent 눈금 및 라우팅, 고급, 신뢰할 수 있는 배달 활용 하기 위해 만들고 Azure와 직접 통합 합니다. 또는 코드를 작성 하지 않고도 어디에서 든 지 논리 앱 tooprocess 데이터와 이벤트 표 형태를 사용할 수 있습니다. 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a>Event Grid는 다른 Azure 통합 서비스와 어떻게 다릅니까?

Event Grid는 이벤트 구동, 반응성 프로그래밍을 사용할 수 있는 이벤트 백플레인입니다. Azure 서비스와 긴밀히 통합하고 타사 서비스와 통합할 수 있습니다. hello 이벤트 메시지 tooreact toochanges 서비스 및 응용 프로그램에 필요한 hello 정보를 포함 합니다. 이벤트 표 형태 데이터 파이프라인 아니며 hello 실제 업데이트 된 개체에 배달 하지 않습니다.

Service Bus는 트랜잭션, 순서 지정, 중복 검색 및 즉시 일관성을 필요로 하는 일반적인 엔터프라이즈 응용 프로그램에 적합합니다. Event Grid는 반응성 모델의 속도, 비율 크기 조정, 너비 및 저렴한 비용을 위해 고안되었습니다. 것은 적합된 tooserverless 아키텍처입니다.

Event Grid는 Logic Apps 및 Event Hubs와 같은 다른 Azure 서비스를 보완합니다. 이벤트 표 트리거 논리 앱 toobegin 워크플로 hello 합니다. 이벤트 허브 이벤트 표 형태 tooreact tooevents 이벤트 허브 캡처 및 데이터 유입과 변환 파이프라인 빌드를 사용 하 여 작동 합니다.

## <a name="how-much-does-event-grid-cost"></a>Event Grid의 비용은 얼마입니까?

Azure Event Grid는 이벤트별 요금 가격 책정 모델을 사용하므로 사용한 것에 대해서만 지불하면 됩니다.

이벤트 표 형태 비용이 백만 작업 ($0.30 미리 보기 중) 당 $0.60 하며 hello 매달 처음 100, 000 작업 자유롭게 있습니다. 작업은 이벤트 수신, 고급 일치, 배달 시도 및 관리 호출로 정의됩니다.  자세한 내용은 hello에서 확인할 수 있습니다 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/event-grid/)합니다.

## <a name="next-steps"></a>다음 단계

* [작성 하 고 toocustom 이벤트 가입](custom-event-quickstart.md) 고 hello Azure 이벤트 표 형태 퀵 스타트를 사용 하 여 사용자 고유의 사용자 지정 이벤트 tooany 끝점을 보내기 시작 합니다.
* [논리 앱을 사용 하 여 이벤트 처리기로](monitor-virtual-machine-changes-event-grid-logic-app.md) 이벤트 표 형태 사용 하 여 논리 앱 tooreact tooevents를 사용 하 여 응용 프로그램 빌드에 대 한 자습서 푸시됩니다.
* [Event Grid REST API 참조](/rest/api/eventgrid)  
  이벤트 구독을 관리 하기 위한 hello Azure 이벤트 표 형태에 대 한 자세한 기술 내용은 대 한 참조를 제공 라우팅 및 필터링 합니다.
