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
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a><span data-ttu-id="7470f-103">Azure Logic Apps 예제 및 일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="7470f-103">Examples and common scenarios for Azure Logic Apps</span></span>

<span data-ttu-id="7470f-104">Azure 논리 앱의 기능 및 많은 패턴에 대 한 자세한 내용은 toohelp hello, 다음은 일반적인 예 및 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-104">toohelp you learn more about hello many patterns and capabilities in Azure Logic Apps, here are common examples and scenarios.</span></span>

## <a name="key-scenarios-for-logic-apps"></a><span data-ttu-id="7470f-105">논리 앱에 대한 주요 시나리요</span><span class="sxs-lookup"><span data-stu-id="7470f-105">Key scenarios for logic apps</span></span>

<span data-ttu-id="7470f-106">Azure Logic Apps는 다양한 서비스에 대한 복원력 있는 오케스트레이션과 통합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-106">Azure Logic Apps provides resilient orchestration and integration for different services.</span></span> <span data-ttu-id="7470f-107">hello 논리 앱 서비스는 "서버", 크기 조정 또는 인스턴스에 대 한 tooworry 없는-모든 있는 toodo는 hello 워크플로 (트리거 및 작업)를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-107">hello Logic Apps service is "serverless", so you don't have tooworry about scale or instances - all you have toodo is define hello workflow (trigger and actions).</span></span> <span data-ttu-id="7470f-108">기본 플랫폼 hello 배율, 가용성 및 성능 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-108">hello underlying platform handles scale, availability, and performance.</span></span> <span data-ttu-id="7470f-109">필요한 toocoordinate 여러 동작을 모든 시나리오는 여러 시스템에서 특히 Azure 논리 앱에 대 한 사용 사례는 좋은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-109">Any scenario where you need toocoordinate multiple actions, especially across multiple systems, is a great use case for Azure Logic Apps.</span></span> <span data-ttu-id="7470f-110">다음은 몇 가지 패턴과 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-110">Here are some patterns and examples.</span></span>

## <a name="respond-tootriggers-and-extend-actions"></a><span data-ttu-id="7470f-111">Tootriggers 응답 하 고 작업 확장</span><span class="sxs-lookup"><span data-stu-id="7470f-111">Respond tootriggers and extend actions</span></span>

<span data-ttu-id="7470f-112">모든 논리 앱은 트리거로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-112">Every logic app begins with a trigger.</span></span> <span data-ttu-id="7470f-113">예를 들어 워크플로 같은 시작할 수 일정 이벤트, 수동으로 호출 또는 외부 시스템에서 이벤트와 트리거 "때 파일이 tooan FTP 서버 추가" hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-113">For example, your workflow can start with a schedule event, a manual invocation, or an event from an external system, such as hello "when a file is added tooan FTP server" trigger.</span></span> <span data-ttu-id="7470f-114">현재 azure 논리 앱에서 온-프레미스 SAP tooMicrosoft Cognitive 서비스 사이의 100 개 이상의 즉시 사용 커넥터를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-114">Azure Logic Apps currently supports over 100 ready-to-use connectors, ranging from on-premises SAP tooMicrosoft Cognitive Services.</span></span> <span data-ttu-id="7470f-115">게시된 커넥터를 포함하지 않을 수 있는 시스템 및 서비스에 대해 논리 앱을 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-115">For systems and services that might not have published connectors, you can also extend logic apps.</span></span>

* [<span data-ttu-id="7470f-116">사용자 지정 트리거 또는 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="7470f-116">Create custom triggers or actions</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="7470f-117">워크플로 실행에 대해 장기 실행 작업 설정</span><span class="sxs-lookup"><span data-stu-id="7470f-117">Set up long-running actions for workflow runs</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="7470f-118">Tooexternal 이벤트 및 webhook 사용 하 여 동작에 응답</span><span class="sxs-lookup"><span data-stu-id="7470f-118">Respond tooexternal events and actions with webhooks</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="7470f-119">트리거를 호출 하거나 중첩 동기 응답 tooHTTP 요청 된 워크플로</span><span class="sxs-lookup"><span data-stu-id="7470f-119">Call, trigger, or nest workflows with synchronous responses tooHTTP requests</span></span>](../logic-apps/logic-apps-http-endpoint.md)
* [<span data-ttu-id="7470f-120">자습서: tooTwilio SMS webhook 응답 하 고 텍스트 응답을 보내기</span><span class="sxs-lookup"><span data-stu-id="7470f-120">Tutorial: Respond tooTwilio SMS webhooks and send a text response</span></span>](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [<span data-ttu-id="7470f-121">자습서: Logic Apps 및 Power BI로 몇 분 안에 AI 기반 소셜 대시보드 빌드</span><span class="sxs-lookup"><span data-stu-id="7470f-121">Tutorial: Build an AI-powered social dashboard in minutes with Logic Apps and Power BI</span></span>](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a><span data-ttu-id="7470f-122">오류 처리, 로깅 및 제어 흐름 기능</span><span class="sxs-lookup"><span data-stu-id="7470f-122">Error handling, logging, and control flow capabilities</span></span>

<span data-ttu-id="7470f-123">논리 앱에는 조건, 스위치, 루프 및 범위와 같은 고급 제어 흐름에 대한 다양한 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-123">Logic apps include rich capabilities for advanced control flow, like conditions, switches, loops, and scopes.</span></span> <span data-ttu-id="7470f-124">tooensure 복구 솔루션 오류 및 예외 처리 워크플로에서 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-124">tooensure resilient solutions, you can also implement error and exception handling in your workflows.</span></span> <span data-ttu-id="7470f-125">워크플로 실행 상태에 대한 알림 및 진단 로그를 위해 Azure Logic Apps에서는 모니터링 및 경고도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-125">For notification and diagnostic logs for workflow run status, Azure Logic Apps also provides monitoring and alerts.</span></span>

* [<span data-ttu-id="7470f-126">Switch 문으로 다양한 작업 수행</span><span class="sxs-lookup"><span data-stu-id="7470f-126">Perform different actions with switch statements</span></span>](../logic-apps/logic-apps-switch-case.md)
* [<span data-ttu-id="7470f-127">논리 앱에서 루프 및 일괄 처리로 배열 및 컬렉션의 항목 처리</span><span class="sxs-lookup"><span data-stu-id="7470f-127">Process items in arrays and collections with loops and batches in logic apps</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="7470f-128">워크플로에서 작성자 오류 및 예외 처리</span><span class="sxs-lookup"><span data-stu-id="7470f-128">Author error and exception handling in a workflow</span></span>](../logic-apps/logic-apps-exception-handling.md)
* [<span data-ttu-id="7470f-129">기존 논리 앱에 대한 모니터링, 로깅 및 경고 켜기</span><span class="sxs-lookup"><span data-stu-id="7470f-129">Turn on monitoring, logging, and alerts for existing logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="7470f-130">논리 앱을 만들 때 모니터링 및 진단 로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="7470f-130">Turn on monitoring and diagnostics logging when creating logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [<span data-ttu-id="7470f-131">사용 사례: 의료 회사에서 HL7 FHIR 워크플로에 대해 논리 앱 예외 처리를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="7470f-131">Use case: How a healthcare company uses logic app exception handling for HL7 FHIR workflows</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a><span data-ttu-id="7470f-132">논리 앱 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="7470f-132">Deploy and manage logic apps</span></span>

<span data-ttu-id="7470f-133">Visual Studio, Visual Studio Team Services 또는 기타 소스 제어 및 자동화된 빌드 도구를 사용하여 논리 앱을 완전하게 개발 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-133">You can fully develop and deploy logic apps with Visual Studio, Visual Studio Team Services, or any other source control and automated build tools.</span></span> <span data-ttu-id="7470f-134">워크플로 및 리소스 서식 파일의 종속 연결에 대 한 toosupport 배포, 논리 앱 배포 템플릿에 Azure 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-134">toosupport deployment for workflows and dependent connections in a resource template, logic apps use Azure resource deployment templates.</span></span> <span data-ttu-id="7470f-135">Visual Studio tools 버전 관리를 위한 toosource 컨트롤에서 확인할 수 있습니다 이러한 서식 파일을 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-135">Visual Studio tools automatically generate these templates, which you can check in toosource control for versioning.</span></span>

* [<span data-ttu-id="7470f-136">자동화된 배포 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="7470f-136">Create an automated deployment template</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="7470f-137">Visual Studio의 논리 앱 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="7470f-137">Build and deploy logic apps from Visual Studio</span></span>](../logic-apps/logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="7470f-138">논리 앱의 hello 상태 모니터</span><span class="sxs-lookup"><span data-stu-id="7470f-138">Monitor hello health of your logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a><span data-ttu-id="7470f-139">콘텐츠 형식, 변환 및 실행 내에서 변형</span><span class="sxs-lookup"><span data-stu-id="7470f-139">Content types, conversions, and transformations within a run</span></span>

<span data-ttu-id="7470f-140">에 액세스 하 고 변환 하 고 hello Azure 논리 앱의에서 많은 함수 hello를 사용 하 여 여러 개의 콘텐츠 형식을 변환할 수 [워크플로 정의 언어](http://aka.ms/logicappsdocs)합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-140">You can access, convert, and transform multiple content types by using hello many functions in hello Azure Logic Apps [workflow definition language](http://aka.ms/logicappsdocs).</span></span> <span data-ttu-id="7470f-141">예를 들어 서로 변환할 수 있습니다 문자열, JSON 및 XML hello로 `@json()` 및 `@xml()` 워크플로 식입니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-141">For example, you can convert between a string, JSON, and XML with hello `@json()` and `@xml()` workflow expressions.</span></span> <span data-ttu-id="7470f-142">hello 논리 앱 엔진 서비스 간에 무손실 방식 콘텐츠 형식을 toosupport 콘텐츠 전송을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-142">hello Logic Apps engine preserves content types toosupport content transfer in a lossless manner between services.</span></span>

* <span data-ttu-id="7470f-143">[비JSON 콘텐츠 형식 처리](../logic-apps/logic-apps-content-type.md)(`application/xml`, `application/octet-stream` 및 `multipart/formdata`)</span><span class="sxs-lookup"><span data-stu-id="7470f-143">[Handle non-JSON content types](../logic-apps/logic-apps-content-type.md), like `application/xml`, `application/octet-stream`, and `multipart/formdata`</span></span>
* [<span data-ttu-id="7470f-144">논리 앱에서 워크플로 식이 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="7470f-144">How workflow expressions work in logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="7470f-145">참조: Azure Logic Apps 워크플로 정의 언어</span><span class="sxs-lookup"><span data-stu-id="7470f-145">Reference: Azure Logic Apps workflow definition language</span></span>](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a><span data-ttu-id="7470f-146">기타 통합 및 기능</span><span class="sxs-lookup"><span data-stu-id="7470f-146">Other integrations and capabilities</span></span>

<span data-ttu-id="7470f-147">논리 앱에서는 Azure Functions, Azure API Management, Azure App Services와 같은 다양한 서비스 및 사용자 지정 HTTP 끝점(REST 및 SOAP)과 통합도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7470f-147">Logic apps also offer integration with many services, like Azure Functions, Azure API Management, Azure App Services, and custom HTTP endpoints, for example, REST and SOAP.</span></span>

* [<span data-ttu-id="7470f-148">Azure 서버를 사용하지 않고 실시간 소셜 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="7470f-148">Create a real-time social dashboard with Azure Serverless</span></span>](../logic-apps/logic-apps-scenario-social-serverless.md)
* [<span data-ttu-id="7470f-149">논리 앱에서 Azure Functions 호출</span><span class="sxs-lookup"><span data-stu-id="7470f-149">Call Azure Functions from logic apps</span></span>](../logic-apps/logic-apps-azure-functions.md)
* [<span data-ttu-id="7470f-150">시나리오: Azure Functions로 논리 앱 트리거</span><span class="sxs-lookup"><span data-stu-id="7470f-150">Scenario: Trigger logic apps with Azure Functions</span></span>](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [<span data-ttu-id="7470f-151">블로그: 논리 앱에서 SOAP 끝점 호출</span><span class="sxs-lookup"><span data-stu-id="7470f-151">Blog: Call SOAP endpoints from logic apps</span></span>](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a><span data-ttu-id="7470f-152">종단 간 시나리오</span><span class="sxs-lookup"><span data-stu-id="7470f-152">End-to-end scenarios</span></span>

* [<span data-ttu-id="7470f-153">백서: Logic Apps와 같은 Azure 서비스를 사용한 엔터프라이즈 통합 종단 간 사례 관리</span><span class="sxs-lookup"><span data-stu-id="7470f-153">Whitepaper: Enterprise integration end-to-end case management with Azure services, like Logic Apps</span></span>](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="next-steps"></a><span data-ttu-id="7470f-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7470f-154">Next steps</span></span>

- [<span data-ttu-id="7470f-155">논리 앱에서 오류 및 예외 처리</span><span class="sxs-lookup"><span data-stu-id="7470f-155">Handle errors and exceptions in logic apps</span></span>](../logic-apps/logic-apps-exception-handling.md)
- [<span data-ttu-id="7470f-156">Hello 워크플로 정의 언어 작성자 워크플로 정의</span><span class="sxs-lookup"><span data-stu-id="7470f-156">Author workflow definitions with hello workflow definition language</span></span>](../logic-apps/logic-apps-author-definitions.md)
- [<span data-ttu-id="7470f-157">Azure Logic Apps를 개선할 수 있는 방법에 대한 의견, 질문, 피드백 또는 제안 사항 제출</span><span class="sxs-lookup"><span data-stu-id="7470f-157">Submit your comments, questions, feedback, or suggestions for how can we improve Azure Logic Apps</span></span>](https://feedback.azure.com/forums/287593-logic-apps)