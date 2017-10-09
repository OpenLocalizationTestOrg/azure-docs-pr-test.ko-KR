---
title: "Azure 기능에 대 한 분석 실시간 처리 aaaStream | Microsoft Docs"
description: "Azure 함수 toouse toopopulate 스트림 분석 작업의 hello 출력에서 Azure Redis 캐시 서비스 버스 큐를 연결 하는 방법을 알아봅니다."
keywords: "데이터 스트림, Redis Cache, Service Bus Queue"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="9e9c0-104">어떻게 Azure 함수를 사용 하는 Azure Redis Cache에서 Azure 스트림 분석에서 toostore 데이터</span><span class="sxs-lookup"><span data-stu-id="9e9c0-104">How toostore data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="9e9c0-105">Azure 스트림 분석을 사용 하 여 신속 하 게 개발 하 고 장치, 센서, 인프라 및 응용 프로그램, 또는 모든 데이터 스트림의에서 toogain 실시간 정보 저렴 한 비용 솔루션을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions toogain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="9e9c0-106">그뿐 아니라 실시간 관리 및 모니터링, 명령 및 컨트롤, 부정행위 감지, 연결된 자동차 등의 다양한 사용 사례를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="9e9c0-107">이러한 대부분의 시나리오에서 Azure Redis 캐시 같은 분산된 된 데이터 저장소에 Azure 스트림 분석에 의해 출력 된 toostore 데이터 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-107">In many such scenarios, you may want toostore data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="9e9c0-108">통신 회사에 근무하고 있다고 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="9e9c0-109">여기서 여러 호출에서 들어오는 hello 동일한 id toodetect SIM 사기 고치려는, 동일한 hello에 항상 사용 하지만 서로 다른 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-109">You are trying toodetect SIM fraud where multiple calls coming from hello same identity, at hello same time, but in different geographically locations.</span></span> <span data-ttu-id="9e9c0-110">업무를 맡았다고 모든 hello는 사기성 전화 통화를 잠재적인 Azure Redis 캐시에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-110">You are tasked with storing all hello potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="9e9c0-111">이 블로그에 이러한 작업을 쉽게 완료하는 방법에 대한 지침이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9e9c0-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9e9c0-112">Prerequisites</span></span>
<span data-ttu-id="9e9c0-113">전체 hello [실시간 사기 감지] [ fraud-detection] ASA에 대 한 연습</span><span class="sxs-lookup"><span data-stu-id="9e9c0-113">Complete hello [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="9e9c0-114">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="9e9c0-114">Architecture Overview</span></span>
![아키텍처 스크린샷](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="9e9c0-116">Hello 앞 그림에에서 나와 있는 것 처럼 스트림 분석 쿼리할 toobe 입력된 데이터를 스트리밍 및 tooan 출력을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-116">As shown in hello preceding figure, Stream Analytics allows streaming input data toobe queried and sent tooan output.</span></span> <span data-ttu-id="9e9c0-117">Hello 출력에 따라, Azure 함수 일부 형식의 이벤트를 트리거한 다음 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-117">Based on hello output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="9e9c0-118">이 블로그의이 파이프라인의 hello Azure 기능 요소에 집중 했습니다 또는 좀 더 구체적으로 hello 캐시로 사기성 일 수 있는 데이터를 저장 하는 이벤트의 트리거를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-118">In this blog, we focus on hello Azure Functions part of this pipeline, or more specifically hello triggering of an event that stores fraudulent data into hello cache.</span></span>
<span data-ttu-id="9e9c0-119">Hello를 완료 한 후 [실시간 사기 감지] [ fraud-detection] 자습서에서는 해야 입력 (이벤트 허브), 쿼리 및 출력 (blob storage) 이미 구성 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-119">After completing hello [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="9e9c0-120">이 블로그의 변경 hello 출력 toouse 서비스 버스 큐 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-120">In this blog, we change hello output toouse a Service Bus Queue instead.</span></span> <span data-ttu-id="9e9c0-121">그런 다음 Azure 함수 toothis 큐를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-121">After that, we connect an Azure Function toothis queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="9e9c0-122">Service Bus Queue 출력 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="9e9c0-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="9e9c0-123">1과 2에서 hello.NET 섹션의 단계를 수행 하는 서비스 버스 큐 toocreate [서비스 버스 큐 시작][servicebus-getstarted]합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-123">toocreate a Service Bus Queue, follow steps 1 and 2 of hello .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="9e9c0-124">이제 hello에서 만든 hello 큐 toohello 스트림 분석 작업에 연결 하겠습니다 이전 사기 감지 연습 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-124">Now let's connect hello queue toohello Stream Analytics job that was created in hello earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="9e9c0-125">Hello Azure 포털에서에서 toohello 이동 **출력** 작업과 선택의 블레이드에서 **추가** hello hello 페이지 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-125">In hello Azure portal, go toohello **Outputs** blade of your job and select **Add** at hello top of hello page.</span></span>
   
    ![출력 추가](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="9e9c0-127">선택 **서비스 버스 큐** hello로 **싱크** hello 화면에 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-127">Choose **Service Bus Queue** as hello **Sink** and follow hello instructions on hello screen.</span></span> <span data-ttu-id="9e9c0-128">만든 있는지 toochoose hello 네임 스페이스의 서비스 버스 큐 hello [서비스 버스 큐 시작][servicebus-getstarted]합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-128">Be sure toochoose hello namespace of hello Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="9e9c0-129">작업이 완료 되 면 hello "오른쪽" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-129">Click hello "right" button when you are finished.</span></span>
3. <span data-ttu-id="9e9c0-130">Hello 다음 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-130">Specify hello following values:</span></span>
   
   * <span data-ttu-id="9e9c0-131">**이벤트 직렬 변환기 형식**: JSON</span><span class="sxs-lookup"><span data-stu-id="9e9c0-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="9e9c0-132">**인코딩**: UTF8</span><span class="sxs-lookup"><span data-stu-id="9e9c0-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="9e9c0-133">**형식**: 줄로 구분</span><span class="sxs-lookup"><span data-stu-id="9e9c0-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="9e9c0-134">Hello 클릭 **만들기** 이 소스와 스트림 분석 toohello 저장소 계정에 연결할 수 있는지 tooverify tooadd 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-134">Click hello **Create** button tooadd this source and tooverify that Stream Analytics can successfully connect toohello storage account.</span></span>
5. <span data-ttu-id="9e9c0-135">Hello에 **쿼리** 탭에서 현재 쿼리 hello hello 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-135">In hello **Query** tab, replace hello current query with hello following.</span></span> <span data-ttu-id="9e9c0-136">대체 * [YOUR 서비스 버스 이름] * 3 단계에서 만든 hello 출력 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-136">Replace *[YOUR SERVICE BUS NAME] * with hello output name you created in step 3.</span></span> 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="9e9c0-137">Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="9e9c0-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="9e9c0-138">Azure Redis 캐시에 hello.NET 섹션에 따라 만들 [어떻게 tooUse Azure Redis Cache] [ use-rediscache] hello 섹션 호출 될 때까지 ***hello 캐시 클라이언트 구성***합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-138">Create an Azure Redis cache by following hello .NET section in [How tooUse Azure Redis Cache][use-rediscache] until hello section called ***Configure hello cache clients***.</span></span>
<span data-ttu-id="9e9c0-139">완료되면 새 Redis Cache가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="9e9c0-140">아래 **모든 설정을**선택, **액세스 키** hello 메모 ***기본 연결 문자열***합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-140">Under **All settings**, select **Access keys** and note down hello ***Primary connection string***.</span></span>

![아키텍처 스크린샷](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="9e9c0-142">Azure Function 만들기</span><span class="sxs-lookup"><span data-stu-id="9e9c0-142">Create an Azure Function</span></span>
<span data-ttu-id="9e9c0-143">에 따라 [사용자 첫 번째 Azure 함수를 만들어] [ functions-getstarted] 자습서 tooget Azure 기능을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-143">Follow [Create your first Azure Function][functions-getstarted] tutorial tooget started with Azure Functions.</span></span> <span data-ttu-id="9e9c0-144">Azure 함수 toouse, 같은 다음 너무 건너 뛸는 이미 있는 경우[tooRedis 캐시를 작성 합니다.](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="9e9c0-144">If you already have an Azure function you would like toouse, then skip ahead too[Writing tooRedis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="9e9c0-145">Hello 포털에서 hello 왼쪽 탐색 영역 응용 프로그램 서비스를 선택한 다음 Azure 함수 응용 프로그램 이름 tooget toohello 함수의 응용 프로그램 웹 사이트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-145">In hello portal, select App Services from hello left-hand navigation, then click your Azure function app name tooget toohello Function's app website.</span></span>
    <span data-ttu-id="9e9c0-146">![앱 서비스 함수 목록 스크린샷](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="9e9c0-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="9e9c0-147">**새 함수 > ServiceBusQueueTrigger – C#**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="9e9c0-148">Hello에 대 한 다음 필드는 다음이 지침을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-148">For hello following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="9e9c0-149">**큐 이름은**: hello 이름에 hello 큐를 만들 때 입력 한 이름이 hello [서비스 버스 큐 시작] [ servicebus-getstarted] hello 이름이 아닌 hello 서비스 버스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-149">**Queue name**: hello same name as hello name you entered when you created hello queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not hello name of hello service bus).</span></span> <span data-ttu-id="9e9c0-150">연결 된 toohello 스트림 분석에서 출력 된 hello 큐를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-150">Make sure you use hello queue that is connected toohello Stream Analytics output.</span></span>
   * <span data-ttu-id="9e9c0-151">**Service Bus 연결**: **연결 문자열 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="9e9c0-152">toofind hello 연결 문자열을 이동 toohello 클래식 포털에서 선택 **서비스 버스**, 서비스 버스를 만든 hello 및 **연결 정보** hello hello 화면 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-152">toofind hello connection string, go toohello classic portal, select **Service Bus**, hello service bus you created, and **CONNECTION INFORMATION** at hello bottom of hello screen.</span></span> <span data-ttu-id="9e9c0-153">이 페이지에서 기본 화면 hello 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-153">Make sure you are on hello main screen on this page.</span></span> <span data-ttu-id="9e9c0-154">복사한 hello 연결 문자열을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-154">Copy and paste hello connection string.</span></span> <span data-ttu-id="9e9c0-155">무료 tooenter 모든 연결 이름을 느낍니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-155">Feel free tooenter any connection name.</span></span>
     
       ![서비스 버스 연결 스크린샷](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="9e9c0-157">**AccessRights**: **관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="9e9c0-158">**만들기**</span><span class="sxs-lookup"><span data-stu-id="9e9c0-158">Click **Create**</span></span>

## <a name="writing-tooredis-cache"></a><span data-ttu-id="9e9c0-159">쓰기 tooRedis 캐시</span><span class="sxs-lookup"><span data-stu-id="9e9c0-159">Writing tooRedis Cache</span></span>
<span data-ttu-id="9e9c0-160">이제 Service Bus Queue에서 읽는 Azure Function가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="9e9c0-161">Toodo 남았습니다는 우리의 함수 toowrite이 데이터 toohello Redis Cache를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-161">All that is left toodo is use our Function toowrite this data toohello Redis Cache.</span></span> 

1. <span data-ttu-id="9e9c0-162">새로 만든 선택 **ServiceBusQueueTrigger**를 클릭 하 고 **앱 설정 함수** hello 상단 오른쪽 모서리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on hello top right corner.</span></span> <span data-ttu-id="9e9c0-163">선택 **tooApp 서비스 설정 이동 > 설정 > 응용 프로그램 설정**</span><span class="sxs-lookup"><span data-stu-id="9e9c0-163">Select **Go tooApp Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="9e9c0-164">연결 문자열 섹션 hello에서 hello에 이름을 만듭니다. **이름** 섹션.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-164">In hello Connection strings section, create a name in hello **Name** section.</span></span> <span data-ttu-id="9e9c0-165">Hello에서 찾은 hello 기본 연결 문자열을 붙여 **Redis 캐시를 만들** hello 한 단계씩 **값** 섹션.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-165">Paste hello primary connection string you found in hello **Create a Redis Cache** step into hello **Value** section.</span></span> <span data-ttu-id="9e9c0-166">**SQL Database**라고 표시되는 **사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="9e9c0-167">클릭 **저장** hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-167">Click **Save** at hello top.</span></span>
   
    ![서비스 버스 연결 스크린샷](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="9e9c0-169">이제 toohello 응용 프로그램 서비스 설정 다시 이동 하 고 선택 **도구 > 앱 서비스 편집기 (미리 보기) >에서 > 이동**합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-169">Now go back toohello App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![서비스 버스 연결 스크린샷](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="9e9c0-171">원하는 편집기에는 JSON 파일을 만듭니다 **project.json** 와 다음 hello 및 tooyour 로컬 디스크를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-171">In an editor of your choice, create a JSON file named **project.json** with hello following and save it tooyour local disk.</span></span>
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. <span data-ttu-id="9e9c0-172">함수 (WWWROOT)의 hello 루트 디렉터리에이 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-172">Upload this file into hello root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="9e9c0-173">라는 파일이 **project.lock.json** 확인 해당 hello Nuget 패키지 "StackExchange.Redis" 및 "Newtonsoft.Json" 가져온, 자동으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-173">You should see a file named **project.lock.json** automatically appear, confirming that hello Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="9e9c0-174">Hello에 **run.csx** 파일, 코드 다음 hello hello 미리 생성 된 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-174">In hello **run.csx** file, replace hello pre-generated code with hello following code.</span></span> <span data-ttu-id="9e9c0-175">Hello lazyConnection 함수에서 "CONN 이름"의 2 단계에서 만든 hello 이름으로 대체 **hello Redis 캐시에 데이터를 저장할**합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-175">In hello lazyConnection function, replace “CONN NAME” with hello name you created in step 2 of **Store data into hello Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a><span data-ttu-id="9e9c0-176">Hello 스트림 분석 작업 시작</span><span class="sxs-lookup"><span data-stu-id="9e9c0-176">Start hello Stream Analytics job</span></span>
1. <span data-ttu-id="9e9c0-177">Hello telcodatagen.exe 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-177">Start hello telcodatagen.exe application.</span></span> <span data-ttu-id="9e9c0-178">hello 사용법은 다음과 같습니다.````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="9e9c0-178">hello usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="9e9c0-179">스트림 분석 작업 블레이드에서 hello hello 포털에서에서 클릭 **시작** hello hello 페이지 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-179">From hello Stream Analytics Job blade in hello portal, click **Start** at hello top of hello page.</span></span>
   
    ![작업 시작 스크린샷](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="9e9c0-181">Hello에 **시작 작업** 선택 표시 되 면 블레이드 **이제** hello를 클릭 한 다음 **시작** hello hello 화면 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-181">In hello **Start job** blade that appears, select **Now** and then click hello **Start** button at hello bottom of hello screen.</span></span> <span data-ttu-id="9e9c0-182">hello 작업 상태 변경 tooStarting 변경 tooRunning 일정 시간 후 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-182">hello job status changes tooStarting and after some time changes tooRunning.</span></span>
   
    ![작업 시작 시간 선택 스크린샷](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="9e9c0-184">솔루션 실행 및 결과 확인</span><span class="sxs-lookup"><span data-stu-id="9e9c0-184">Run solution and check results</span></span>
<span data-ttu-id="9e9c0-185">Tooyour를 다시 살펴보자면 **ServiceBusQueueTrigger** 이제 페이지 문을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-185">Going back tooyour **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="9e9c0-186">이러한 로그 항목 hello 데이터베이스에 저장 하는 hello 서비스 버스 큐에서에서 받은 hello 시간 hello 키로 사용 하 여 인출 하 표시!</span><span class="sxs-lookup"><span data-stu-id="9e9c0-186">These logs show that you got something from hello Service Bus Queue, put it into hello database, and fetched it out using hello time as hello key!</span></span>

<span data-ttu-id="9e9c0-187">Redis 캐시에 있는 데이터 tooverify hello 새로운 포털에서 Redis 캐시 페이지 tooyour 이동 (hello 앞에 표시 된 대로 [Azure Redis 캐시를 만들](#Create-an-Azure-Redis-Cache) 단계) 콘솔을 선택 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-187">tooverify that your data is in your Redis cache, go tooyour Redis cache page in hello new portal (as shown in hello preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="9e9c0-188">이제 데이터가 실제로 hello 캐시 Redis 명령 tooconfirm 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-188">Now you can write Redis commands tooconfirm that data is in fact in hello cache.</span></span>

![Redis 콘솔 스크린샷](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="9e9c0-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9e9c0-190">Next steps</span></span>
<span data-ttu-id="9e9c0-191">Hello 새로운 것 Azure 함수에 대 한 기능 및 스트림 분석을 수행할 수 있습니다에 대 한 새로운 가능성의 잠금을 해제이 하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-191">We’re excited about hello new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="9e9c0-192">수행한 다음에 대 한 의견 있다면 느껴집니다 무료 toouse hello [Azure UserVoice 사이트](https://feedback.azure.com/forums/270577-stream-analytics)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-192">If you have any feedback on what you want next, feel free toouse hello [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="9e9c0-193">새 Microsoft Azure 인 경우 초대 tootry에 등록 하 여 로그 아웃 한 [무료 Azure 평가판 계정](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-193">If you are new Microsoft Azure, we invite you tootry it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="9e9c0-194">새 tooStream 분석 중인 경우 너무 초대[첫 번째 스트림 분석 작업 만들기](stream-analytics-create-a-job.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-194">If you are new tooStream Analytics, then we invite you too[create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="9e9c0-195">도움말이 필요하거나 질문이 있는 경우 [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) 또는 [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) 포럼에 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="9e9c0-196">Hello 다음 리소스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-196">You can also see hello following resources:</span></span>

* [<span data-ttu-id="9e9c0-197">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="9e9c0-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="9e9c0-198">Azure Functions C# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="9e9c0-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="9e9c0-199">Azure Functions F# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="9e9c0-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="9e9c0-200">Azure Functions NodeJS 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="9e9c0-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="9e9c0-201">Azure Functions 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="9e9c0-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="9e9c0-202">Azure Redis 캐시 하는 toomonitor 방법</span><span class="sxs-lookup"><span data-stu-id="9e9c0-202">How toomonitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="9e9c0-203">toostay 모든 hello 최신 뉴스 및 기능에서 최신 상태에 따라 [ @AzureStreaming ](https://twitter.com/AzureStreaming) Twitter에서.</span><span class="sxs-lookup"><span data-stu-id="9e9c0-203">toostay up-to-date on all hello latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
