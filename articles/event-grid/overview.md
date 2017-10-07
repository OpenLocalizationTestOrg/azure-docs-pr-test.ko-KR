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
# <a name="an-introduction-tooazure-event-grid"></a><span data-ttu-id="ca686-103">소개 tooAzure 이벤트 표 형태</span><span class="sxs-lookup"><span data-stu-id="ca686-103">An introduction tooAzure Event Grid</span></span>

<span data-ttu-id="ca686-104">Azure 이벤트 표 형태 이벤트 기반 아키텍처를 가진 응용 프로그램을 tooeasily 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-104">Azure Event Grid allows you tooeasily build applications with event-based architectures.</span></span> <span data-ttu-id="ca686-105">Hello, toosubscribe 선택한 hello 이벤트 처리기 또는 WebHook 끝점 toosend hello 이벤트를 제공 하는 Azure 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-105">You select hello Azure resource you would like toosubscribe to, and give hello event handler or WebHook endpoint toosend hello event to.</span></span> <span data-ttu-id="ca686-106">Event Grid는 기본적으로 저장소 Blob 및 리소스 그룹과 같은 Azure 서비스의 이벤트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="ca686-107">또한 Event Grid는 사용자 지정 토픽 및 사용자 지정 웹후크를 사용하여 응용 프로그램 및 타사 이벤트에 대한 사용자 지정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="ca686-108">필터 tooroute 특정 이벤트 toodifferent 끝점, 멀티 캐스트 toomultiple 끝점을 사용할 수 있으며 이벤트 안정적으로 배달 되 고 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ca686-108">You can use filters tooroute specific events toodifferent endpoints, multicast toomultiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="ca686-109">Event Grid에는 기본적으로 사용자 지정 및 타사 이벤트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="ca686-110">이벤트 표 형태 hello 미리 보기 릴리스에 대 한 지원 **westus2** 및 **westcentralus** 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-110">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="ca686-111">다른 지역이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-111">Other regions will be added.</span></span>

<span data-ttu-id="ca686-112">이 문서는 Azure Event Grid의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="ca686-113">이벤트 표 형태 시작 tooget 참조 [Azure 이벤트 표 형태를 사용자 지정 이벤트 만들기 및 경로](custom-event-quickstart.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-113">If you want tooget started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Event Grid 기능 모델](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="ca686-115">현재, Blob Storage는 게시자로 공개적으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="ca686-116">개념</span><span class="sxs-lookup"><span data-stu-id="ca686-116">Concepts</span></span>

<span data-ttu-id="ca686-117">이제부터 살펴볼 Azure Event Grid의 5가지 개념은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="ca686-118">**이벤트** - 발생한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-118">**Events** - What happened.</span></span>
* <span data-ttu-id="ca686-119">**이벤트 원본/게시자** -hello 이벤트 발생 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="ca686-119">**Event sources/publishers** - Where hello event took place.</span></span>
* <span data-ttu-id="ca686-120">**항목** -hello 게시자가 이벤트를 보낼 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-120">**Topics** - hello endpoint where publishers send events.</span></span>
* <span data-ttu-id="ca686-121">**이벤트 가입** -hello 끝점 또는 기본 제공 메커니즘 tooroute 이벤트, 경우에 따라 toomultiple 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-121">**Event subscriptions** - hello endpoint or built-in mechanism tooroute events, sometimes toomultiple handlers.</span></span> <span data-ttu-id="ca686-122">구독도 처리기 toointelligently 필터 들어오는 이벤트에 의해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-122">Subscriptions are also used by handlers toointelligently filter incoming events.</span></span>
* <span data-ttu-id="ca686-123">**이벤트 처리기** -앱 hello 또는 응답할 toohello 이벤트를 서비스 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-123">**Event handlers** - hello app or service reacting toohello event.</span></span>

<span data-ttu-id="ca686-124">이러한 개념에 대한 자세한 내용은 [Azure Event Grid의 개념](concepts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca686-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="ca686-125">기능</span><span class="sxs-lookup"><span data-stu-id="ca686-125">Capabilities</span></span>

<span data-ttu-id="ca686-126">다음은 이벤트 표 형태 Azure의 hello 주요 기능 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-126">Here are some of hello key features of Azure Event Grid:</span></span>

* <span data-ttu-id="ca686-127">**단순성** -Azure 리소스 tooany 이벤트 처리기 또는 끝점에서 tooaim 이벤트 가리키고 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-127">**Simplicity** - Point and click tooaim events from your Azure resource tooany event handler or endpoint.</span></span>
* <span data-ttu-id="ca686-128">**고급 필터링** -이벤트에 대 한 필터 유형 또는 이벤트 게시 경로 tooensure 이벤트 처리기만 관련 이벤트를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-128">**Advanced filtering** - Filter on event type or event publish path tooensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="ca686-129">**팬 아웃** -여러 끝점 toohello 구독 동일한 이벤트 toosend 복사 hello 이벤트 tooas의 여러 위치 필요에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-129">**Fan-out** - Subscribe multiple endpoints toohello same event toosend copies of hello event tooas many places as needed.</span></span>
* <span data-ttu-id="ca686-130">**안정성** -이벤트가 전달 되는 지 수 백오프 tooensure로 재시도 24 시간제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-130">**Reliability** - Utilize 24-hour retry with exponential backoff tooensure events are delivered.</span></span>
* <span data-ttu-id="ca686-131">**사용량 기준 과금 이벤트별** -지불 하는 hello 금액에 대 한 이벤트 표 형태를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-131">**Pay-per-event** - Pay only for hello amount you use Event Grid.</span></span>
* <span data-ttu-id="ca686-132">**높은 처리량** - 초당 수백만 개 이벤트 지원을 통해 Event Grid에서 대량 워크로드를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="ca686-133">**기본 제공 이벤트** - 리소스 정의 기본 제공 이벤트를 사용하여 신속하게 준비하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="ca686-134">**사용자 지정 이벤트** - Event Grid를 사용하여 사용자 앱의 사용자 지정 이벤트를 라우팅하고, 필터링하며, 안정적으로 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="ca686-135">기본 제공 게시자 및 처리기 통합</span><span class="sxs-lookup"><span data-stu-id="ca686-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="ca686-136">Azure는 게시자 및 처리기를 모두 포함한 다양한 서비스를 사용하는 기본 제공 이벤트 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="ca686-137">게시자</span><span class="sxs-lookup"><span data-stu-id="ca686-137">Publishers</span></span>

<span data-ttu-id="ca686-138">현재 hello 다음 Azure 서비스가 있는 이벤트 표 형태에 대 한 기본 제공 된 게시자 지원:</span><span class="sxs-lookup"><span data-stu-id="ca686-138">Currently, hello following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="ca686-139">리소스 그룹(관리 작업)</span><span class="sxs-lookup"><span data-stu-id="ca686-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="ca686-140">Azure 구독(관리 작업)</span><span class="sxs-lookup"><span data-stu-id="ca686-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="ca686-141">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ca686-141">Event Hubs</span></span>
* <span data-ttu-id="ca686-142">사용자 지정 토픽</span><span class="sxs-lookup"><span data-stu-id="ca686-142">Custom Topics</span></span>

<span data-ttu-id="ca686-143">올해 다른 Azure 서비스가 추가될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="ca686-144">처리기</span><span class="sxs-lookup"><span data-stu-id="ca686-144">Handlers</span></span>

<span data-ttu-id="ca686-145">현재 hello 다음 Azure 서비스가 있는 이벤트 표 형태에 대 한 기본 제공 처리기 지원:</span><span class="sxs-lookup"><span data-stu-id="ca686-145">Currently, hello following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="ca686-146">Azure 기능</span><span class="sxs-lookup"><span data-stu-id="ca686-146">Azure Functions</span></span>
* <span data-ttu-id="ca686-147">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ca686-147">Logic Apps</span></span>
* <span data-ttu-id="ca686-148">Azure Automation</span><span class="sxs-lookup"><span data-stu-id="ca686-148">Azure Automation</span></span>
* <span data-ttu-id="ca686-149">웹후크</span><span class="sxs-lookup"><span data-stu-id="ca686-149">WebHooks</span></span>

<span data-ttu-id="ca686-150">올해 다른 Azure 서비스가 추가될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="ca686-151">Event Grid로 할 수 있는 작업은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="ca686-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="ca686-152">Azure Event Grid는 서버를 사용하지 않는 작업 자동화 및 통합 작업을 크게 개선하는 여러 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="ca686-153">서버를 사용하지 않는 응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="ca686-153">Serverless application architectures</span></span>

![서버를 사용하지 않는 응용 프로그램](./media/overview/serverless_web_app.png)

<span data-ttu-id="ca686-155">Event Grid는 데이터 원본과 이벤트 처리기를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="ca686-156">예를 들어 새 사진을 때마다 tooa blob 저장소 컨테이너를 추가 하는 서버가 없는 함수 toorun 이미지 분석 이벤트 표 형태 tooinstantly 트리거를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-156">For example, use Event Grid tooinstantly trigger a serverless function toorun image analysis each time a new photo is added tooa blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="ca686-157">작업 자동화</span><span class="sxs-lookup"><span data-stu-id="ca686-157">Ops Automation</span></span>

![작업 자동화](./media/overview/Ops_automation.png)

<span data-ttu-id="ca686-159">이벤트 표 형태 toospeed 자동화를 지원 하 고 정책 적용을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-159">Event Grid allows you toospeed automation and simplify policy enforcement.</span></span> <span data-ttu-id="ca686-160">예를 들어 Event Grid는 가상 컴퓨터가 만들어지거나 SQL Database가 실행되면 Azure Automation에 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="ca686-161">이러한 이벤트를 사용할 수 있습니다 tooautomatically에 있는지 확인 서비스 구성, 운영 도구, 태그 가상 컴퓨터 또는 작업 항목 파일에 메타 데이터를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-161">These events can be used tooautomatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="ca686-162">응용 프로그램 통합</span><span class="sxs-lookup"><span data-stu-id="ca686-162">Application integration</span></span>

![응용 프로그램 통합](./media/overview/app_integration.png)

<span data-ttu-id="ca686-164">Event Grid는 앱을 다른 서비스와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="ca686-165">예를 들어 사용자 지정 항목 toosend 응용 프로그램의 이벤트 데이터 tooEvent 눈금 및 라우팅, 고급, 신뢰할 수 있는 배달 활용 하기 위해 만들고 Azure와 직접 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-165">For example, create a custom topic toosend your app's event data tooEvent Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="ca686-166">또는 코드를 작성 하지 않고도 어디에서 든 지 논리 앱 tooprocess 데이터와 이벤트 표 형태를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-166">Alternatively, you can use Event Grid with Logic Apps tooprocess data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="ca686-167">Event Grid는 다른 Azure 통합 서비스와 어떻게 다릅니까?</span><span class="sxs-lookup"><span data-stu-id="ca686-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="ca686-168">Event Grid는 이벤트 구동, 반응성 프로그래밍을 사용할 수 있는 이벤트 백플레인입니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="ca686-169">Azure 서비스와 긴밀히 통합하고 타사 서비스와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="ca686-170">hello 이벤트 메시지 tooreact toochanges 서비스 및 응용 프로그램에 필요한 hello 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-170">hello event message contains hello information you need tooreact toochanges in services and applications.</span></span> <span data-ttu-id="ca686-171">이벤트 표 형태 데이터 파이프라인 아니며 hello 실제 업데이트 된 개체에 배달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-171">Event Grid is not a data pipeline, and does not deliver hello actual object that was updated.</span></span>

<span data-ttu-id="ca686-172">Service Bus는 트랜잭션, 순서 지정, 중복 검색 및 즉시 일관성을 필요로 하는 일반적인 엔터프라이즈 응용 프로그램에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="ca686-173">Event Grid는 반응성 모델의 속도, 비율 크기 조정, 너비 및 저렴한 비용을 위해 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="ca686-174">것은 적합된 tooserverless 아키텍처입니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-174">It is well suited tooserverless architecture.</span></span>

<span data-ttu-id="ca686-175">Event Grid는 Logic Apps 및 Event Hubs와 같은 다른 Azure 서비스를 보완합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="ca686-176">이벤트 표 트리거 논리 앱 toobegin 워크플로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-176">Event Grid triggers hello logic app toobegin its workflow.</span></span> <span data-ttu-id="ca686-177">이벤트 허브 이벤트 표 형태 tooreact tooevents 이벤트 허브 캡처 및 데이터 유입과 변환 파이프라인 빌드를 사용 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-177">Event Hubs works with Event Grid by enabling you tooreact tooevents from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="ca686-178">Event Grid의 비용은 얼마입니까?</span><span class="sxs-lookup"><span data-stu-id="ca686-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="ca686-179">Azure Event Grid는 이벤트별 요금 가격 책정 모델을 사용하므로 사용한 것에 대해서만 지불하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="ca686-180">이벤트 표 형태 비용이 백만 작업 ($0.30 미리 보기 중) 당 $0.60 하며 hello 매달 처음 100, 000 작업 자유롭게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and hello first 100,000 operation per month are free.</span></span> <span data-ttu-id="ca686-181">작업은 이벤트 수신, 고급 일치, 배달 시도 및 관리 호출로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="ca686-182">자세한 내용은 hello에서 확인할 수 있습니다 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/event-grid/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-182">More details can be found on hello [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca686-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ca686-183">Next steps</span></span>

* <span data-ttu-id="ca686-184">[작성 하 고 toocustom 이벤트 가입](custom-event-quickstart.md) 고 hello Azure 이벤트 표 형태 퀵 스타트를 사용 하 여 사용자 고유의 사용자 지정 이벤트 tooany 끝점을 보내기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-184">[Create and subscribe toocustom events](custom-event-quickstart.md) Jump right in and start sending your own custom events tooany endpoint using hello Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="ca686-185">[논리 앱을 사용 하 여 이벤트 처리기로](monitor-virtual-machine-changes-event-grid-logic-app.md) 이벤트 표 형태 사용 하 여 논리 앱 tooreact tooevents를 사용 하 여 응용 프로그램 빌드에 대 한 자습서 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps tooreact tooevents pushed by Event Grid.</span></span>
* [<span data-ttu-id="ca686-186">Event Grid REST API 참조</span><span class="sxs-lookup"><span data-stu-id="ca686-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="ca686-187">이벤트 구독을 관리 하기 위한 hello Azure 이벤트 표 형태에 대 한 자세한 기술 내용은 대 한 참조를 제공 라우팅 및 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca686-187">Provides more technical information about hello Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>
