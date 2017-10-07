---
title: "aaaExamples 및 일반적인 시나리오-Azure 논리 앱 | Microsoft Docs"
description: "예제, 시나리오 및 자습서를 통해 논리 앱에 대해 자세히 알아보세요."
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/9/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 17caa8539ec6a57726b9c6c07a71fb74caa07ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a>Azure Logic Apps 예제 및 일반적인 시나리오

Azure 논리 앱의 기능 및 많은 패턴에 대 한 자세한 내용은 toohelp hello, 다음은 일반적인 예 및 시나리오입니다.

## <a name="key-scenarios-for-logic-apps"></a>논리 앱에 대한 주요 시나리요

Azure Logic Apps는 다양한 서비스에 대한 복원력 있는 오케스트레이션과 통합을 제공합니다. hello 논리 앱 서비스는 "서버", 크기 조정 또는 인스턴스에 대 한 tooworry 없는-모든 있는 toodo는 hello 워크플로 (트리거 및 작업)를 정의 합니다. 기본 플랫폼 hello 배율, 가용성 및 성능 처리합니다. 필요한 toocoordinate 여러 동작을 모든 시나리오는 여러 시스템에서 특히 Azure 논리 앱에 대 한 사용 사례는 좋은 합니다. 다음은 몇 가지 패턴과 예제입니다.

## <a name="respond-tootriggers-and-extend-actions"></a>Tootriggers 응답 하 고 작업 확장

모든 논리 앱은 트리거로 시작됩니다. 예를 들어 워크플로 같은 시작할 수 일정 이벤트, 수동으로 호출 또는 외부 시스템에서 이벤트와 트리거 "때 파일이 tooan FTP 서버 추가" hello 합니다. 현재 azure 논리 앱에서 온-프레미스 SAP tooMicrosoft Cognitive 서비스 사이의 100 개 이상의 즉시 사용 커넥터를 지원 합니다. 게시된 커넥터를 포함하지 않을 수 있는 시스템 및 서비스에 대해 논리 앱을 확장할 수도 있습니다.

* [사용자 지정 트리거 또는 작업 만들기](../logic-apps/logic-apps-create-api-app.md)
* [워크플로 실행에 대해 장기 실행 작업 설정](../logic-apps/logic-apps-create-api-app.md)
* [Tooexternal 이벤트 및 webhook 사용 하 여 동작에 응답](../logic-apps/logic-apps-create-api-app.md)
* [트리거를 호출 하거나 중첩 동기 응답 tooHTTP 요청 된 워크플로](../logic-apps/logic-apps-http-endpoint.md)
* [자습서: tooTwilio SMS webhook 응답 하 고 텍스트 응답을 보내기](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [자습서: Logic Apps 및 Power BI로 몇 분 안에 AI 기반 소셜 대시보드 빌드](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a>오류 처리, 로깅 및 제어 흐름 기능

논리 앱에는 조건, 스위치, 루프 및 범위와 같은 고급 제어 흐름에 대한 다양한 기능을 포함합니다. tooensure 복구 솔루션 오류 및 예외 처리 워크플로에서 구현할 수 있습니다. 워크플로 실행 상태에 대한 알림 및 진단 로그를 위해 Azure Logic Apps에서는 모니터링 및 경고도 제공합니다.

* [Switch 문으로 다양한 작업 수행](../logic-apps/logic-apps-switch-case.md)
* [논리 앱에서 루프 및 일괄 처리로 배열 및 컬렉션의 항목 처리](../logic-apps/logic-apps-loops-and-scopes.md)
* [워크플로에서 작성자 오류 및 예외 처리](../logic-apps/logic-apps-exception-handling.md)
* [기존 논리 앱에 대한 모니터링, 로깅 및 경고 켜기](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [논리 앱을 만들 때 모니터링 및 진단 로깅 켜기](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [사용 사례: 의료 회사에서 HL7 FHIR 워크플로에 대해 논리 앱 예외 처리를 사용하는 방법](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a>논리 앱 배포 및 관리

Visual Studio, Visual Studio Team Services 또는 기타 소스 제어 및 자동화된 빌드 도구를 사용하여 논리 앱을 완전하게 개발 및 배포할 수 있습니다. 워크플로 및 리소스 서식 파일의 종속 연결에 대 한 toosupport 배포, 논리 앱 배포 템플릿에 Azure 리소스를 사용합니다. Visual Studio tools 버전 관리를 위한 toosource 컨트롤에서 확인할 수 있습니다 이러한 서식 파일을 자동으로 생성 합니다.

* [자동화된 배포 템플릿 만들기](../logic-apps/logic-apps-create-deploy-template.md)
* [Visual Studio의 논리 앱 빌드 및 배포](../logic-apps/logic-apps-deploy-from-vs.md)
* [논리 앱의 hello 상태 모니터](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a>콘텐츠 형식, 변환 및 실행 내에서 변형

에 액세스 하 고 변환 하 고 hello Azure 논리 앱의에서 많은 함수 hello를 사용 하 여 여러 개의 콘텐츠 형식을 변환할 수 [워크플로 정의 언어](http://aka.ms/logicappsdocs)합니다. 예를 들어 서로 변환할 수 있습니다 문자열, JSON 및 XML hello로 `@json()` 및 `@xml()` 워크플로 식입니다. hello 논리 앱 엔진 서비스 간에 무손실 방식 콘텐츠 형식을 toosupport 콘텐츠 전송을 유지합니다.

* [비JSON 콘텐츠 형식 처리](../logic-apps/logic-apps-content-type.md)(`application/xml`, `application/octet-stream` 및 `multipart/formdata`)
* [논리 앱에서 워크플로 식이 작동하는 방식](../logic-apps/logic-apps-author-definitions.md)
* [참조: Azure Logic Apps 워크플로 정의 언어](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a>기타 통합 및 기능

논리 앱에서는 Azure Functions, Azure API Management, Azure App Services와 같은 다양한 서비스 및 사용자 지정 HTTP 끝점(REST 및 SOAP)과 통합도 제공합니다.

* [Azure 서버를 사용하지 않고 실시간 소셜 대시보드 만들기](../logic-apps/logic-apps-scenario-social-serverless.md)
* [논리 앱에서 Azure Functions 호출](../logic-apps/logic-apps-azure-functions.md)
* [시나리오: Azure Functions로 논리 앱 트리거](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [블로그: 논리 앱에서 SOAP 끝점 호출](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a>종단 간 시나리오

* [백서: Logic Apps와 같은 Azure 서비스를 사용한 엔터프라이즈 통합 종단 간 사례 관리](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="next-steps"></a>다음 단계

- [논리 앱에서 오류 및 예외 처리](../logic-apps/logic-apps-exception-handling.md)
- [Hello 워크플로 정의 언어 작성자 워크플로 정의](../logic-apps/logic-apps-author-definitions.md)
- [Azure Logic Apps를 개선할 수 있는 방법에 대한 의견, 질문, 피드백 또는 제안 사항 제출](https://feedback.azure.com/forums/287593-logic-apps)