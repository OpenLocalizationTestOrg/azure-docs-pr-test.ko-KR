---
title: "aaaAzure Insights 원격 분석 데이터 모델 응용 프로그램 원격 분석 컨텍스트 | Microsoft Docs"
description: "Application Insights 원격 분석 컨텍스트 데이터 모델"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a>원격 분석 컨텍스트: Application Insights 데이터 모델

모든 원격 분석 항목에는 강력한 형식의 컨텍스트 필드가 있을 수 있습니다. 모든 필드는 특정 모니터링 시나리오를 지원합니다. Hello 사용자 지정 속성 컬렉션 toostore 사용자 지정 또는 응용 프로그램 관련 컨텍스트 정보를 사용 합니다.


##<a name="application-version"></a>응용 프로그램 버전

Hello 응용 프로그램 컨텍스트 필드의 정보는 항상 hello 원격 분석을 전송 하는 hello 응용 프로그램에 대 한 합니다. 응용 프로그램 버전은 hello 응용 프로그램 동작 및 해당 상관 관계 toohello 배포에 사용 되는 tooanalyze 추세 변경 합니다.

최대 길이: 1024


##<a name="client-ip-address"></a>클라이언트 IP 주소

hello hello 클라이언트 장치의 IP 주소입니다. IPv4 및 IPv6이 지원됩니다. 서비스에서 원격 분석을 보내면 hello 작업 hello 서비스에서 시작한 hello 사용자에 대 한 hello 위치 컨텍스트는입니다. Application Insights는 hello 클라이언트 IP에서 hello 지리적 위치 정보를 추출 하를 잘라 다음 합니다. 따라서 클라이언트 IP 자체는 최종 사용자가 식별할 수 있는 정보로 사용될 수 없습니다. 

최대 길이: 46


##<a name="device-type"></a>장치 유형

이 필드는 사용 된 원래 사용 하는 hello 응용 프로그램의 hello 장치 hello 최종 사용자의 tooindicate hello 유형입니다. 오늘날 주로 toodistinguish JavaScript 원격 분석 형식과 함께 사용 hello 장치 '브라우저'에서 서버 쪽 원격 분석 hello 장치 유형 'p C'으로 합니다.

최대 길이: 64


##<a name="operation-id"></a>작업 ID

Hello 루트 작업의 고유 식별자입니다. 이 식별자는 여러 구성 요소에서 toogroup 원격 분석을 허용 합니다. 자세한 내용은 [원격 분석 상관 관계](application-insights-correlation.md)를 참조하세요. hello 작업 id는 요청 또는 페이지 보기에서 만들어집니다. 다른 모든 원격 분석 요청이 나 페이지 뷰를 포함 하는 hello에 대 한이 필드 toohello 값을 설정 합니다. 

최대 길이: 128


##<a name="parent-operation-id"></a>부모 작업 ID

안녕 hello 원격 분석 항목의 직계 부모의 고유 식별자입니다. 자세한 내용은 [원격 분석 상관 관계](application-insights-correlation.md)를 참조하세요.

최대 길이: 128


##<a name="operation-name"></a>작업 이름

hello 연산의 hello 이름 (그룹)입니다. 요청 또는 페이지 보기 하 여 hello 작업 이름이 생성 됩니다. 다른 모든 원격 분석 항목 요청 또는 페이지 뷰를 포함 하는 hello에 대 한이 필드 toohello 값을 설정 합니다. 작업 이름이 작업 (예를 들어 ' GET Home/Index ')의 그룹에 대 한 모든 hello 원격 분석 항목을 찾는 데 사용 됩니다. 이 컨텍스트 속성은 사용 되는 tooanswer 같은 질문을 "hello이이 페이지에서 throw 되는 일반적인 예외 무엇 인가요."

최대 길이: 1024


##<a name="synthetic-source-of-hello-operation"></a>Hello 작업의 합성 소스

가상 원본의 이름입니다. Hello 응용 프로그램에서 일부 원격 분석 가상 트래픽을 나타낼 수 있습니다. 웹 크롤러 인덱싱 hello 웹 사이트, 사이트 가용성 테스트 또는 자체 Application Insights SDK과 같은 진단 라이브러리에서 추적 수 있습니다.

최대 길이: 1024


##<a name="session-id"></a>세션 ID

세션 ID-hello 인스턴스의 hello 사용자의 상호 hello 앱입니다. Hello 세션 컨텍스트 필드의 정보는 항상 hello 최종 사용자에 대 한 합니다. 서비스에서 원격 분석을 보내면 hello 세션 컨텍스트가 hello 작업 hello 서비스에서 시작한 hello 사용자에 대 한입니다.

최대 길이: 64


##<a name="anonymous-user-id"></a>익명 사용자 ID

익명 사용자 ID입니다. Hello 응용 프로그램의 hello 최종 사용자를 나타냅니다. 서비스에서 원격 분석을 보내면 hello 사용자 컨텍스트가 hello 작업 hello 서비스에서 시작한 hello 사용자에 대 한입니다.

[샘플링](app-insights-sampling.md) hello 기술 toominimize hello 양의 원격 분석 수집된 중 하나입니다. 알고리즘 시도 tooeither 샘플링 샘플 또는 모든 hello 축소 상관 관계가 지정 된 원격 분석 합니다. 익명 사용자 ID는 샘플링 점수 생성에 사용됩니다. 따라서 익명 사용자 ID는 충분히 임의의 값이어야 합니다. 

익명 사용자 id toostore 사용자 이름을 사용 하는 hello 필드의 오용입니다. 인증된 사용자 ID를 사용하세요.

최대 길이: 128


##<a name="authenticated-user-id"></a>인증된 사용자 ID

인증 된 사용자 id입니다. 익명 사용자 id,이 필드의 반대 hello 라는 이름으로 hello 사용자를 나타냅니다. PII 정보이므로 기본적으로 대부분의 SDK에서 수집되지 않습니다.

최대 길이: 1024


##<a name="account-id"></a>계정 ID

다중 테 넌 트 응용 프로그램에서 hello 계정 ID 또는 hello 사용자와 작동 하는 이름입니다. 예를 들어 Azure Portal의 구독 ID 또는 플랫폼을 블로깅하는 블로그 이름일 수 있습니다.

최대 길이: 1024


##<a name="cloud-role"></a>클라우드 역할

일부인 hello 역할 hello 응용 프로그램의 이름입니다. Azure에서 역할 이름을 toohello를 직접 매핑합니다. 사용 되는 toodistinguish 단일 응용 프로그램의 구성 요소인 마이크로 서비스 일 수도 있습니다.

최대 길이: 256


##<a name="cloud-role-instance"></a>클라우드 역할 인스턴스

Hello 응용 프로그램이 실행 중인 hello 인스턴스의 이름입니다. 온-프레미스의 경우 컴퓨터 이름, Azure의 경우 인스턴스 이름입니다.

최대 길이: 256


##<a name="internal-sdk-version"></a>내부: SDK 버전

SDK 버전입니다. 자세한 내용은 https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification을 참조하세요.

최대 길이: 64


##<a name="internal-node-name"></a>내부: 노드 이름

이 필드는 요금 청구를 위해 사용 되는 hello 노드 이름을 나타냅니다. 노드 toooverride hello 표준 검색 방법을 사용 합니다.

최대 길이: 256


## <a name="next-steps"></a>다음 단계

- 너무 방법에 대해 알아봅니다[확장 하 고 원격 분석 필터링](app-insights-api-filtering-sampling.md)합니다.
- Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.
- 표준 컨텍스트 속성 컬렉션 [구성](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet)을 확인합니다.
