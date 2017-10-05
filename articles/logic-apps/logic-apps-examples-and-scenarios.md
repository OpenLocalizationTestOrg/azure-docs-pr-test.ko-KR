---
title: "예제 및 일반적인 시나리오 - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 50df1e3db239a6aa34ac91bfbd582625c5b0041b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a><span data-ttu-id="1c680-103">Azure Logic Apps 예제 및 일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="1c680-103">Examples and common scenarios for Azure Logic Apps</span></span>

<span data-ttu-id="1c680-104">Azure Logic Apps에서 다양한 패턴 및 기능에 대해 자세히 알아볼 수 있는 일반적인 예제 및 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-104">To help you learn more about the many patterns and capabilities in Azure Logic Apps, here are common examples and scenarios.</span></span>

## <a name="key-scenarios-for-logic-apps"></a><span data-ttu-id="1c680-105">논리 앱에 대한 주요 시나리요</span><span class="sxs-lookup"><span data-stu-id="1c680-105">Key scenarios for logic apps</span></span>

<span data-ttu-id="1c680-106">Azure Logic Apps는 다양한 서비스에 대한 복원력 있는 오케스트레이션과 통합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-106">Azure Logic Apps provides resilient orchestration and integration for different services.</span></span> <span data-ttu-id="1c680-107">Logic Apps 서비스는 "서버를 사용하지 않으므로" 규모 또는 인스턴스에 대해 고민할 필요가 없으며 워크플로(트리거 및 작업)만 정의하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-107">The Logic Apps service is "serverless", so you don't have to worry about scale or instances - all you have to do is define the workflow (trigger and actions).</span></span> <span data-ttu-id="1c680-108">기본 플랫폼에서 규모, 가용성 및 성능을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-108">The underlying platform handles scale, availability, and performance.</span></span> <span data-ttu-id="1c680-109">여러 작업(특히 여러 시스템 간)을 조정해야 하는 모든 시나리오는 Azure Logic Apps에 대한 좋은 사용 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-109">Any scenario where you need to coordinate multiple actions, especially across multiple systems, is a great use case for Azure Logic Apps.</span></span> <span data-ttu-id="1c680-110">다음은 몇 가지 패턴과 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-110">Here are some patterns and examples.</span></span>

## <a name="respond-to-triggers-and-extend-actions"></a><span data-ttu-id="1c680-111">트리거에 응답 및 작업 확장</span><span class="sxs-lookup"><span data-stu-id="1c680-111">Respond to triggers and extend actions</span></span>

<span data-ttu-id="1c680-112">모든 논리 앱은 트리거로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-112">Every logic app begins with a trigger.</span></span> <span data-ttu-id="1c680-113">예를 들어 워크플로는 일정 이벤트, 수동 호출 또는 "파일이 FTP 서버에 추가된 경우" 트리거와 같은 외부 시스템의 이벤트로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-113">For example, your workflow can start with a schedule event, a manual invocation, or an event from an external system, such as the "when a file is added to an FTP server" trigger.</span></span> <span data-ttu-id="1c680-114">현재 Azure Logic Apps는 온-프레미스 SAP에서 Microsoft Cognitive Services에 이르는 100개 이상의 즉시 사용 가능한 커넥터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-114">Azure Logic Apps currently supports over 100 ready-to-use connectors, ranging from on-premises SAP to Microsoft Cognitive Services.</span></span> <span data-ttu-id="1c680-115">게시된 커넥터를 포함하지 않을 수 있는 시스템 및 서비스에 대해 논리 앱을 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-115">For systems and services that might not have published connectors, you can also extend logic apps.</span></span>

* [<span data-ttu-id="1c680-116">사용자 지정 트리거 또는 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="1c680-116">Create custom triggers or actions</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="1c680-117">워크플로 실행에 대해 장기 실행 작업 설정</span><span class="sxs-lookup"><span data-stu-id="1c680-117">Set up long-running actions for workflow runs</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="1c680-118">웹후크로 외부 이벤트 및 작업에 응답</span><span class="sxs-lookup"><span data-stu-id="1c680-118">Respond to external events and actions with webhooks</span></span>](../logic-apps/logic-apps-create-api-app.md)
* [<span data-ttu-id="1c680-119">HTTP 요청에 대한 동기 응답을 포함하는 호출, 트리거 또는 중첩 워크플로</span><span class="sxs-lookup"><span data-stu-id="1c680-119">Call, trigger, or nest workflows with synchronous responses to HTTP requests</span></span>](../logic-apps/logic-apps-http-endpoint.md)
* [<span data-ttu-id="1c680-120">자습서: Twilio SMS 웹후크에 응답 및 텍스트 응답 보내기</span><span class="sxs-lookup"><span data-stu-id="1c680-120">Tutorial: Respond to Twilio SMS webhooks and send a text response</span></span>](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [<span data-ttu-id="1c680-121">자습서: Logic Apps 및 Power BI로 몇 분 안에 AI 기반 소셜 대시보드 빌드</span><span class="sxs-lookup"><span data-stu-id="1c680-121">Tutorial: Build an AI-powered social dashboard in minutes with Logic Apps and Power BI</span></span>](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a><span data-ttu-id="1c680-122">오류 처리, 로깅 및 제어 흐름 기능</span><span class="sxs-lookup"><span data-stu-id="1c680-122">Error handling, logging, and control flow capabilities</span></span>

<span data-ttu-id="1c680-123">논리 앱에는 조건, 스위치, 루프 및 범위와 같은 고급 제어 흐름에 대한 다양한 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-123">Logic apps include rich capabilities for advanced control flow, like conditions, switches, loops, and scopes.</span></span> <span data-ttu-id="1c680-124">복원력 있는 솔루션을 보장하기 위해 워크플로에서 오류 및 예외 처리를 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-124">To ensure resilient solutions, you can also implement error and exception handling in your workflows.</span></span> <span data-ttu-id="1c680-125">워크플로 실행 상태에 대한 알림 및 진단 로그를 위해 Azure Logic Apps에서는 모니터링 및 경고도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-125">For notification and diagnostic logs for workflow run status, Azure Logic Apps also provides monitoring and alerts.</span></span>

* [<span data-ttu-id="1c680-126">Switch 문으로 다양한 작업 수행</span><span class="sxs-lookup"><span data-stu-id="1c680-126">Perform different actions with switch statements</span></span>](../logic-apps/logic-apps-switch-case.md)
* [<span data-ttu-id="1c680-127">논리 앱에서 루프 및 일괄 처리로 배열 및 컬렉션의 항목 처리</span><span class="sxs-lookup"><span data-stu-id="1c680-127">Process items in arrays and collections with loops and batches in logic apps</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="1c680-128">워크플로에서 작성자 오류 및 예외 처리</span><span class="sxs-lookup"><span data-stu-id="1c680-128">Author error and exception handling in a workflow</span></span>](../logic-apps/logic-apps-exception-handling.md)
* [<span data-ttu-id="1c680-129">기존 논리 앱에 대한 모니터링, 로깅 및 경고 켜기</span><span class="sxs-lookup"><span data-stu-id="1c680-129">Turn on monitoring, logging, and alerts for existing logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="1c680-130">논리 앱을 만들 때 모니터링 및 진단 로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="1c680-130">Turn on monitoring and diagnostics logging when creating logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [<span data-ttu-id="1c680-131">사용 사례: 의료 회사에서 HL7 FHIR 워크플로에 대해 논리 앱 예외 처리를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="1c680-131">Use case: How a healthcare company uses logic app exception handling for HL7 FHIR workflows</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a><span data-ttu-id="1c680-132">논리 앱 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="1c680-132">Deploy and manage logic apps</span></span>

<span data-ttu-id="1c680-133">Visual Studio, Visual Studio Team Services 또는 기타 소스 제어 및 자동화된 빌드 도구를 사용하여 논리 앱을 완전하게 개발 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-133">You can fully develop and deploy logic apps with Visual Studio, Visual Studio Team Services, or any other source control and automated build tools.</span></span> <span data-ttu-id="1c680-134">리소스 템플릿에서 워크플로 및 종속 연결에 대한 배포를 지원하기 위해 논리 앱은 Azure 리소스 배포 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-134">To support deployment for workflows and dependent connections in a resource template, logic apps use Azure resource deployment templates.</span></span> <span data-ttu-id="1c680-135">Visual Studio 도구는 이러한 템플릿을 자동으로 생성하므로 버전 관리를 위해 소스 제어에 체크인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-135">Visual Studio tools automatically generate these templates, which you can check in to source control for versioning.</span></span>

* [<span data-ttu-id="1c680-136">자동화된 배포 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="1c680-136">Create an automated deployment template</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="1c680-137">Visual Studio의 논리 앱 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="1c680-137">Build and deploy logic apps from Visual Studio</span></span>](../logic-apps/logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="1c680-138">논리 앱 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="1c680-138">Monitor the health of your logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a><span data-ttu-id="1c680-139">콘텐츠 형식, 변환 및 실행 내에서 변형</span><span class="sxs-lookup"><span data-stu-id="1c680-139">Content types, conversions, and transformations within a run</span></span>

<span data-ttu-id="1c680-140">Azure Logic Apps [워크플로 정의 언어](http://aka.ms/logicappsdocs)의 다양한 함수를 사용하여 여러 콘텐츠 유형을 액세스, 변환 및 변형시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-140">You can access, convert, and transform multiple content types by using the many functions in the Azure Logic Apps [workflow definition language](http://aka.ms/logicappsdocs).</span></span> <span data-ttu-id="1c680-141">예를 들어, `@json()` 및 `@xml()` 워크플로 식을 사용하여 문자열, JSON 및 XML 간에 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-141">For example, you can convert between a string, JSON, and XML with the `@json()` and `@xml()` workflow expressions.</span></span> <span data-ttu-id="1c680-142">Logic Apps 엔진은 서비스 간에 무손실 방식으로 콘텐츠 전송을 지원하는 콘텐츠 형식을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-142">The Logic Apps engine preserves content types to support content transfer in a lossless manner between services.</span></span>

* <span data-ttu-id="1c680-143">[비JSON 콘텐츠 형식 처리](../logic-apps/logic-apps-content-type.md)(`application/xml`, `application/octet-stream` 및 `multipart/formdata`)</span><span class="sxs-lookup"><span data-stu-id="1c680-143">[Handle non-JSON content types](../logic-apps/logic-apps-content-type.md), like `application/xml`, `application/octet-stream`, and `multipart/formdata`</span></span>
* [<span data-ttu-id="1c680-144">논리 앱에서 워크플로 식이 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="1c680-144">How workflow expressions work in logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="1c680-145">참조: Azure Logic Apps 워크플로 정의 언어</span><span class="sxs-lookup"><span data-stu-id="1c680-145">Reference: Azure Logic Apps workflow definition language</span></span>](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a><span data-ttu-id="1c680-146">기타 통합 및 기능</span><span class="sxs-lookup"><span data-stu-id="1c680-146">Other integrations and capabilities</span></span>

<span data-ttu-id="1c680-147">논리 앱에서는 Azure Functions, Azure API Management, Azure App Services와 같은 다양한 서비스 및 사용자 지정 HTTP 끝점(REST 및 SOAP)과 통합도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c680-147">Logic apps also offer integration with many services, like Azure Functions, Azure API Management, Azure App Services, and custom HTTP endpoints, for example, REST and SOAP.</span></span>

* [<span data-ttu-id="1c680-148">Azure 서버를 사용하지 않고 실시간 소셜 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="1c680-148">Create a real-time social dashboard with Azure Serverless</span></span>](../logic-apps/logic-apps-scenario-social-serverless.md)
* [<span data-ttu-id="1c680-149">논리 앱에서 Azure Functions 호출</span><span class="sxs-lookup"><span data-stu-id="1c680-149">Call Azure Functions from logic apps</span></span>](../logic-apps/logic-apps-azure-functions.md)
* [<span data-ttu-id="1c680-150">시나리오: Azure Functions로 논리 앱 트리거</span><span class="sxs-lookup"><span data-stu-id="1c680-150">Scenario: Trigger logic apps with Azure Functions</span></span>](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [<span data-ttu-id="1c680-151">블로그: 논리 앱에서 SOAP 끝점 호출</span><span class="sxs-lookup"><span data-stu-id="1c680-151">Blog: Call SOAP endpoints from logic apps</span></span>](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a><span data-ttu-id="1c680-152">종단 간 시나리오</span><span class="sxs-lookup"><span data-stu-id="1c680-152">End-to-end scenarios</span></span>

* [<span data-ttu-id="1c680-153">백서: Logic Apps와 같은 Azure 서비스를 사용한 엔터프라이즈 통합 종단 간 사례 관리</span><span class="sxs-lookup"><span data-stu-id="1c680-153">Whitepaper: Enterprise integration end-to-end case management with Azure services, like Logic Apps</span></span>](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="next-steps"></a><span data-ttu-id="1c680-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c680-154">Next steps</span></span>

- [<span data-ttu-id="1c680-155">논리 앱에서 오류 및 예외 처리</span><span class="sxs-lookup"><span data-stu-id="1c680-155">Handle errors and exceptions in logic apps</span></span>](../logic-apps/logic-apps-exception-handling.md)
- [<span data-ttu-id="1c680-156">워크플로 정의 언어로 워크플로 정의 작성</span><span class="sxs-lookup"><span data-stu-id="1c680-156">Author workflow definitions with the workflow definition language</span></span>](../logic-apps/logic-apps-author-definitions.md)
- [<span data-ttu-id="1c680-157">Azure Logic Apps를 개선할 수 있는 방법에 대한 의견, 질문, 피드백 또는 제안 사항 제출</span><span class="sxs-lookup"><span data-stu-id="1c680-157">Submit your comments, questions, feedback, or suggestions for how can we improve Azure Logic Apps</span></span>](https://feedback.azure.com/forums/287593-logic-apps)