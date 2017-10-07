---
title: "aaaAzure 함수 개요 | Microsoft Docs"
description: "이해 방법을 toouse Azure 함수 toooptimize 분 후에 비동기 작업입니다."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 668f9055a007fee662a4c7ec774d3c0a1d847800
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-functions"></a>소개 tooAzure 함수  
Azure 함수 hello 클라우드에서 쉽게 소량의 코드 또는 "기능"을 실행 하기 위한 솔루션을입니다. 전체 응용 프로그램이 나 hello 인프라 toorun에 대 한 걱정 없이, hello 문제에 대 한 필요한 hello 코드만 작성할 수 있습니다. 함수는 개발 생산성을 높일 수 있으며 C#, F#, Node.js, Python, PHP 등의 원하는 개발 언어를 사용할 수 있습니다. 필요에 따라 Azure tooscale를 신뢰 하 고 코드를 실행 하는 hello 시간만 비용을 지불 합니다. Azure Functions를 사용하면 Microsoft Azure에서 서버를 사용하지 않는 응용 프로그램을 개발할 수 있습니다.

이 항목에서는 Azure Functions에 대한 간략한 개요를 제공합니다. Toojump 오른쪽 사용할 Azure 함수 시작 하는 경우 시작 [사용자 첫 번째 Azure 함수를 만들어](functions-create-first-azure-function.md)합니다. 함수에 대 한 자세한 기술 정보를 찾고 hello 참조 [개발자 참조](functions-reference.md)합니다.

## <a name="features"></a>기능
Azure Functions의 몇 가지 주요 기능은 다음과 같습니다.

* **언어 선택** - C#, F#, Node.js, Python, PHP, Batch, Bash 또는 기타 실행 파일을 사용하여 함수를 작성합니다.
* **사용량 기준 과금 기본 사용 가격 책정 모델** -지불 하는 hello에 대 한 데 걸린 시간 프로그램 코드를 실행 합니다. Hello 소비 호스팅 옵션 hello에 계획 참조 [섹션 가격](#pricing)합니다.  
* **고유한 종속성 가져오기** - Functions는 NuGet 및 NPM을 지원하므로 즐겨찾는 라이브러리를 사용할 수 있습니다.  
* **통합 보안** - Azure Active Directory, Facebook, Google, Twitter, Microsoft 계정 등의 OAuth 공급자를 사용하여 HTTP 트리거 함수를 보호합니다.  
* **통합 간소화** - Azure 서비스 및 SaaS(software-as-a-service) 제품을 손쉽게 활용합니다. Hello 참조 [통합 섹션](#integrations) 몇 가지 예제입니다.  
* **유연한 개발** -hello 포털에서 사용자 함수 바로 코드 또는 연속 통합을 설정 하 고 GitHub, Visual Studio Team Services 및 기타를 통해 코드 배포 [개발 도구를 지원](../app-service-web/web-sites-deploy.md#deploy-using-an-ide)합니다.  
* **오픈 소스** -hello 함수 런타임이 오픈 소스 및 [GitHub에서 사용할 수 있는](https://github.com/azure/azure-webjobs-sdk-script)합니다.  

## <a name="what-can-i-do-with-functions"></a>함수로 할 수 있는 작업은 무엇인가요?
Azure 함수는 데이터 처리를 위한 가장 좋은 방법, 사물 인터넷 (IoT) hello 및 간단한 Api 및 microservices 구축 작업 시스템을 통합 합니다. 이미지 또는 주문 처리, 파일 유지 관리 등의 작업에 대 한 또는 일정에 따라 toorun 원하는 모든 작업에 대 한 기능을 고려 합니다. 

함수는 템플릿 tooget을 hello 다음을 비롯 한 주요 시나리오를 시작 했을 제공 합니다.

* **BlobTrigger** -toocontainers 추가 될 때 프로세스 Azure 저장소 blob입니다. 이 함수를 이미지 크기 조정에 사용할 수 있습니다.
* **EventHubTrigger** -tooevents 배달 tooan Azure 이벤트 허브에 응답 합니다. 응용 프로그램 계측, 사용자 경험 또는 워크플로 처리 및 사물 인터넷(IoT) 시나리오에서 특히 유용합니다.
* **일반 웹후크** - 웹후크를 지원하는 모든 서비스의 웹후크 HTTP 요청을 처리합니다.
* **GitHub webhook** -GitHub 리포지토리에서 발생 하는 응답 tooevents 합니다. 예제를 보려면 [웹후크 또는 API 함수 만들기](functions-create-a-web-hook-or-api-function.md)를 참조하세요.
* **HTTPTrigger** -HTTP 요청을 사용 하 여 hello 코드 실행을 트리거합니다.
* **QueueTrigger** -Azure 저장소 큐에 도착 했을 때 toomessages 응답 합니다. 예를 들어 참조 [tooan Azure 서비스에 바인딩하는 Azure 함수를 만들](functions-create-an-azure-connected-function.md)합니다.
* **ServiceBusQueueTrigger** -Azure 서비스 또는 온-프레미스 서비스 수신 대기 toomessage 큐에서 사용자 코드 tooother 연결 합니다. 
* **ServiceBusTopicTrigger** -프로그램 코드 tooother Azure 서비스 또는 온-프레미스 서비스 tootopics 가입 하 여 연결 합니다. 
* **TimerTrigger** - 사전 정의된 일정에 따라 정리 또는 다른 배치 작업을 실행합니다. 예제를 보려면 [이벤트 처리 함수 만들기](functions-create-an-event-processing-function.md)를 참조하세요.

Azure 함수 지원 *트리거*, 어떤 가지 toostart 코드를 실행 하 고 *바인딩*, 있는 방법으로 toosimplify 코딩 하는 입력 및 출력 데이터에 대 한 합니다. Hello 트리거 및 Azure 함수에서 제공 되는 바인딩에 대 한 자세한 설명은 참조 하세요. [Azure 함수 트리거 및 바인딩 개발자 참조](functions-triggers-bindings.md)합니다.

## <a name="integrations"></a>통합
Azure Functions는 다양한 Azure 및 타사 서비스와 통합됩니다. 이러한 서비스는 함수 및 시작 실행을 트리거하거나 코드에 대한 입력 및 출력으로 사용할 수 있습니다. 서비스 통합을 수행 하는 hello Azure 함수에서 사용할 수 있습니다. 

* Azure Cosmos DB
* Azure 이벤트 허브 
* Azure 모바일 앱(테이블)
* Azure 알림 허브
* Azure Service Bus(큐 및 항목)
* Azure 저장소(Blob, 쿠, 테이블) 
* GitHub(웹후크)
* 온-프레미스(서비스 버스 사용)
* Twilio(SMS 메시지)

## <a name="pricing"></a>Functions 사용 비용
Azure 기능에는 두 종류의 가격 책정 모델 하나를 선택 hello 요구 사항에 가장 적합 합니다. 

* **소비 계획** -함수 실행 되며, Azure hello 필요한 계산 리소스를 모두 제공 합니다. 리소스 관리에 대 한 tooworry 및 코드를 실행 하는 hello 시간에 대 한 요금만 지불 합니다. 
* **앱 서비스 계획** - 웹, 모바일, API 앱 등의 함수를 실행합니다. 이미 다른 응용 프로그램에 대 한 앱 서비스 사용 하는 경우에 추가 비용 없이 계획 동일 hello에 함수를 실행할 수 있습니다. 

전체 가격 책정 정보 hello에서 사용할 수 있는 [함수 가격 페이지](https://azure.microsoft.com/pricing/details/functions/)합니다. 함수를 확장 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooscale Azure 함수](functions-scale.md)합니다.

## <a name="next-steps"></a>다음 단계
* [첫 번째 Azure Function 만들기](functions-create-first-azure-function.md)  
  시작 하 고 hello Azure 함수 퀵 스타트를 사용 하 여 첫 번째 함수를 만듭니다. 
* [Azure Functions 개발자 참조](functions-reference.md)  
  함수를 코딩 및 트리거 및 바인딩 정의 대 한 hello Azure 함수 런타임 및 참조 하는 방법에 대 한 자세한 기술 정보를 제공 합니다.
* [Azure Functions 테스트](functions-test-a-function.md)  
  함수를 테스트하는 다양한 도구와 기법을 설명합니다.
* [어떻게 tooscale Azure 함수](functions-scale.md)  
  Hello 소비 호스팅 계획 및 toochoose 오른쪽 계획 hello 하는 방법을 비롯 한 Azure 기능을 사용할 수 있는 서비스 계획에 설명 합니다. 
* [Azure 앱 서비스에 대해 자세히 알아보기](../app-service/app-service-value-prop-what-is.md)  
  Azure 기능 배포, 환경 변수 및 진단 유틸리티와 같은 핵심 기능에 대 한 hello Azure 앱 서비스 플랫폼을 활용 합니다. 

