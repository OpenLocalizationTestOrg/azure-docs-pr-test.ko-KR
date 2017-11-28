---
title: "Azure Functions에 대한 Stream Analytics 실시간 처리 | Microsoft Docs"
description: "Service Bus Queue에 연결된 Azure 함수를 사용하여 Stream Analytic 작업의 출력으로 Azure Redis Cache를 채우는 방법을 알아봅니다."
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
ms.openlocfilehash: ad14cc858ff513573e2718a26a9ab5c524e1adc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-store-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="c4111-104">Azure Functions를 사용하여 Azure Redis Cache에 Azure Stream Analytic의 데이터를 저장하는 방법</span><span class="sxs-lookup"><span data-stu-id="c4111-104">How to store data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="c4111-105">Azure Stream Analytic을 통해 장치, 센서, 인프라, 응용 프로그램 또는 데이터 스트림에서 실시간 정보를 얻는 저비용 분석 솔루션을 빠르게 개발하고 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions to gain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="c4111-106">그뿐 아니라 실시간 관리 및 모니터링, 명령 및 컨트롤, 부정행위 감지, 연결된 자동차 등의 다양한 사용 사례를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="c4111-107">이러한 많은 시나리오에서 Azure Stream Analytic에 의해 출력된 데이터를 Azure Redis Cache와 같은 분산된 데이터 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-107">In many such scenarios, you may want to store data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="c4111-108">통신 회사에 근무하고 있다고 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="c4111-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="c4111-109">다중 호출이 동일한 ID에서 시작되지만, 동시에 지리적으로 다른 위치에서도 발생하는 SIM 부정 상황을 감지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-109">You are trying to detect SIM fraud where multiple calls coming from the same identity, at the same time, but in different geographically locations.</span></span> <span data-ttu-id="c4111-110">잠재적인 모든 사기성 전화 통화를 Azure Redis Cache에 저장하는 업무를 맡게되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-110">You are tasked with storing all the potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="c4111-111">이 블로그에 이러한 작업을 쉽게 완료하는 방법에 대한 지침이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c4111-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c4111-112">Prerequisites</span></span>
<span data-ttu-id="c4111-113">ASA에 대한 [실시간 사기 감지][fraud-detection] 연습 완료</span><span class="sxs-lookup"><span data-stu-id="c4111-113">Complete the [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="c4111-114">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="c4111-114">Architecture Overview</span></span>
![아키텍처 스크린샷](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="c4111-116">위 그림에 나와 있는 것처럼 Stream Analytic을 사용하여 스트리밍 입력 데이터를 쿼리하고 출력으로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-116">As shown in the preceding figure, Stream Analytics allows streaming input data to be queried and sent to an output.</span></span> <span data-ttu-id="c4111-117">출력에 따라, Azure Functions에서 일부 형식의 이벤트를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-117">Based on the output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="c4111-118">이 블로그에서는 이 파이프라인의 Azure Functions 부분을 좀 더 중점적으로 살펴보고 사기성 데이터를 캐시에 저장하는 이벤트 트리거에 대해서도 구체적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-118">In this blog, we focus on the Azure Functions part of this pipeline, or more specifically the triggering of an event that stores fraudulent data into the cache.</span></span>
<span data-ttu-id="c4111-119">[실시간 사기 감지][fraud-detection] 자습서를 완료하면 입력(이벤트 허브), 쿼리 및 출력(Blob Storage)이 구성되어 실행되고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-119">After completing the [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="c4111-120">이 블로그에서는 대신 Service Bus Queue를 사용하여 출력을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-120">In this blog, we change the output to use a Service Bus Queue instead.</span></span> <span data-ttu-id="c4111-121">그런 다음 이 큐에 Azure Function을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-121">After that, we connect an Azure Function to this queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="c4111-122">Service Bus Queue 출력 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="c4111-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="c4111-123">Service Bus 큐를 만들려면 [Service Bus 큐 시작][servicebus-getstarted]의 .NET 섹션 1~2단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-123">To create a Service Bus Queue, follow steps 1 and 2 of the .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="c4111-124">이제 이전 사기 감지 연습에서 만든 Stream Analytic 작업에 큐를 연결해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-124">Now let's connect the queue to the Stream Analytics job that was created in the earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="c4111-125">Azure Portal에서 작업의 **출력** 블레이드로 이동한 후 페이지 맨 위의 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-125">In the Azure portal, go to the **Outputs** blade of your job and select **Add** at the top of the page.</span></span>
   
    ![출력 추가](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="c4111-127">**Service Bus Queue**로 **싱크**를 선택하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-127">Choose **Service Bus Queue** as the **Sink** and follow the instructions on the screen.</span></span> <span data-ttu-id="c4111-128">[Service Bus 큐 시작][servicebus-getstarted]에서 만든 Service Bus 큐의 네임스페이스를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-128">Be sure to choose the namespace of the Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="c4111-129">작업이 완료되었으면 “오른쪽” 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-129">Click the "right" button when you are finished.</span></span>
3. <span data-ttu-id="c4111-130">다음 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-130">Specify the following values:</span></span>
   
   * <span data-ttu-id="c4111-131">**이벤트 직렬 변환기 형식**: JSON</span><span class="sxs-lookup"><span data-stu-id="c4111-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="c4111-132">**인코딩**: UTF8</span><span class="sxs-lookup"><span data-stu-id="c4111-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="c4111-133">**형식**: 줄로 구분</span><span class="sxs-lookup"><span data-stu-id="c4111-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="c4111-134">**만들기** 단추를 클릭하여 이 소스를 추가하고 Stream Analytic이 저장소 계정에 성공적으로 연결될 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-134">Click the **Create** button to add this source and to verify that Stream Analytics can successfully connect to the storage account.</span></span>
5. <span data-ttu-id="c4111-135">**쿼리** 탭에서 현재 쿼리를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-135">In the **Query** tab, replace the current query with the following.</span></span> <span data-ttu-id="c4111-136">*[YOUR SERVICE BUS NAME] *을 3단계에서 만든 출력 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-136">Replace *[YOUR SERVICE BUS NAME] * with the output name you created in step 3.</span></span> 
   
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

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="c4111-137">Azure Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="c4111-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="c4111-138">***캐시 클라이언트 구성***이라는 섹션까지 [Azure Redis Cache를 사용하는 방법][use-rediscache]의 .NET 섹션을 따라 Azure Redis Cache를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-138">Create an Azure Redis cache by following the .NET section in [How to Use Azure Redis Cache][use-rediscache] until the section called ***Configure the cache clients***.</span></span>
<span data-ttu-id="c4111-139">완료되면 새 Redis Cache가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="c4111-140">**모든 설정** 아래에서 **액세스 키**를 선택하고 ***기본 연결 문자열***을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-140">Under **All settings**, select **Access keys** and note down the ***Primary connection string***.</span></span>

![아키텍처 스크린샷](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="c4111-142">Azure Function 만들기</span><span class="sxs-lookup"><span data-stu-id="c4111-142">Create an Azure Function</span></span>
<span data-ttu-id="c4111-143">[첫 번째 Azure 함수 만들기][functions-getstarted] 자습서에 따라 Azure Functions를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-143">Follow [Create your first Azure Function][functions-getstarted] tutorial to get started with Azure Functions.</span></span> <span data-ttu-id="c4111-144">사용하려는 Azure 함수가 이미 있는 경우 [Redis Cache에 쓰기](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="c4111-144">If you already have an Azure function you would like to use, then skip ahead to [Writing to Redis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="c4111-145">포털의 왼쪽 탐색 모음에서 App Service를 선택하고 Azure 함수 앱 이름을 클릭하여 함수의 앱 웹 사이트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-145">In the portal, select App Services from the left-hand navigation, then click your Azure function app name to get to the Function's app website.</span></span>
    <span data-ttu-id="c4111-146">![앱 서비스 함수 목록 스크린샷](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="c4111-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="c4111-147">**새 함수 > ServiceBusQueueTrigger – C#**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="c4111-148">다음 필드에 대해 다음 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-148">For the following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="c4111-149">**큐 이름**: [Service Bus 큐 시작][servicebus-getstarted]에서 큐를 만들 때 입력한 이름과 같습니다(Service Bus 이름은 아님).</span><span class="sxs-lookup"><span data-stu-id="c4111-149">**Queue name**: The same name as the name you entered when you created the queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not the name of the service bus).</span></span> <span data-ttu-id="c4111-150">Stream Analytic 출력에 연결된 큐를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-150">Make sure you use the queue that is connected to the Stream Analytics output.</span></span>
   * <span data-ttu-id="c4111-151">**Service Bus 연결**: **연결 문자열 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="c4111-152">연결 문자열을 찾으려면 클래식 포털로 이동한 후 화면 아래쪽에 있는 **Service Bus**, 만든 서비스 버스 및 **연결 정보**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-152">To find the connection string, go to the classic portal, select **Service Bus**, the service bus you created, and **CONNECTION INFORMATION** at the bottom of the screen.</span></span> <span data-ttu-id="c4111-153">이 페이지의 주 화면에 계속 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-153">Make sure you are on the main screen on this page.</span></span> <span data-ttu-id="c4111-154">연결 문자열을 복사한 후 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-154">Copy and paste the connection string.</span></span> <span data-ttu-id="c4111-155">연결 이름은 원하는 대로 입력해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-155">Feel free to enter any connection name.</span></span>
     
       ![서비스 버스 연결 스크린샷](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="c4111-157">**AccessRights**: **관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="c4111-158">**만들기**</span><span class="sxs-lookup"><span data-stu-id="c4111-158">Click **Create**</span></span>

## <a name="writing-to-redis-cache"></a><span data-ttu-id="c4111-159">Redis Cache에 쓰기</span><span class="sxs-lookup"><span data-stu-id="c4111-159">Writing to Redis Cache</span></span>
<span data-ttu-id="c4111-160">이제 Service Bus Queue에서 읽는 Azure Function가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="c4111-161">이제 이 함수를 사용하여 이 데이터를 Redis Cache에 쓰면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-161">All that is left to do is use our Function to write this data to the Redis Cache.</span></span> 

1. <span data-ttu-id="c4111-162">새로 만든 **ServiceBusQueueTrigger**를 선택하고 오른쪽 위 구석에서 **함수 앱 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on the top right corner.</span></span> <span data-ttu-id="c4111-163">**App Service 설정으로 이동 > 설정 > 응용 프로그램 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-163">Select **Go to App Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="c4111-164">연결 문자열 섹션의 **이름** 섹션에 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-164">In the Connection strings section, create a name in the **Name** section.</span></span> <span data-ttu-id="c4111-165">**Redis Cache 만들기** 단계에서 찾은 기본 연결 문자열을 **값** 섹션에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-165">Paste the primary connection string you found in the **Create a Redis Cache** step into the **Value** section.</span></span> <span data-ttu-id="c4111-166">**SQL Database**라고 표시되는 **사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="c4111-167">위쪽에서 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-167">Click **Save** at the top.</span></span>
   
    ![서비스 버스 연결 스크린샷](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="c4111-169">이제 App Service 설정으로 다시 이동한 후 **도구 > App Service 편집기(미리 보기) > 켜기 > 이동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-169">Now go back to the App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![서비스 버스 연결 스크린샷](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="c4111-171">선택한 편집기에서 다음을 사용하여 **project.json** 이라는 JSON 파일을 만든 후 로컬 디스크에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-171">In an editor of your choice, create a JSON file named **project.json** with the following and save it to your local disk.</span></span>
   
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
6. <span data-ttu-id="c4111-172">함수의 루트 디렉터리(WWWROOT 아님)에 이 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-172">Upload this file into the root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="c4111-173">**project.lock.json** 이라는 파일이 자동으로 표시되면 "StackExchange.Redis" 및 "Newtonsoft.Json" Nuget 패키지를 가져왔는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-173">You should see a file named **project.lock.json** automatically appear, confirming that the Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="c4111-174">**run.csx** 파일에서 미리 생성된 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-174">In the **run.csx** file, replace the pre-generated code with the following code.</span></span> <span data-ttu-id="c4111-175">LazyConnection 함수에서 "CONN NAME"을 **Redis Cache에 데이터 저장**의 2단계에서 만든 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-175">In the lazyConnection function, replace “CONN NAME” with the name you created in step 2 of **Store data into the Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers to a property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract the time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using the cache object...
        // Simple put of integral data types into the cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from the cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect to the Service Bus
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

## <a name="start-the-stream-analytics-job"></a><span data-ttu-id="c4111-176">Stream Analytic 작업 시작</span><span class="sxs-lookup"><span data-stu-id="c4111-176">Start the Stream Analytics job</span></span>
1. <span data-ttu-id="c4111-177">telcodatagen.exe 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-177">Start the telcodatagen.exe application.</span></span> <span data-ttu-id="c4111-178">사용법은 다음과 같습니다. ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="c4111-178">The usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="c4111-179">포털의 Stream Analytic 작업 블레이드에서 페이지 위쪽의 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-179">From the Stream Analytics Job blade in the portal, click **Start** at the top of the page.</span></span>
   
    ![작업 시작 스크린샷](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="c4111-181">나타나는 **작업 시작** 블레이드에서 **지금**을 클릭하고 화면 아래쪽에서 **시작** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-181">In the **Start job** blade that appears, select **Now** and then click the **Start** button at the bottom of the screen.</span></span> <span data-ttu-id="c4111-182">작업 상태가 시작 중으로 변경되고, 잠시 후에는 실행 중으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-182">The job status changes to Starting and after some time changes to Running.</span></span>
   
    ![작업 시작 시간 선택 스크린샷](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="c4111-184">솔루션 실행 및 결과 확인</span><span class="sxs-lookup"><span data-stu-id="c4111-184">Run solution and check results</span></span>
<span data-ttu-id="c4111-185">**ServiceBusQueueTrigger** 페이지로 돌아가면 로그 설명이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-185">Going back to your **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="c4111-186">이러한 로그는 Service Bus Queue에서 일부 항목을 가져와 데이터베이스에 추가한 후 시간을 키로 사용해서 항목을 가져왔음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-186">These logs show that you got something from the Service Bus Queue, put it into the database, and fetched it out using the time as the key!</span></span>

<span data-ttu-id="c4111-187">Redis cache에 해당 데이터가 있는지 확인하려면 새 포털의 Redis Cache 페이지로 이동한 후(앞의 [Azure Redis Cache 만들기](#Create-an-Azure-Redis-Cache) 단계 참조) 콘솔을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-187">To verify that your data is in your Redis cache, go to your Redis cache page in the new portal (as shown in the preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="c4111-188">이제 해당 데이터가 실제로 캐시에 있는지를 확인하는 Redis 명령을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-188">Now you can write Redis commands to confirm that data is in fact in the cache.</span></span>

![Redis 콘솔 스크린샷](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="c4111-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4111-190">Next steps</span></span>
<span data-ttu-id="c4111-191">Azure Functions 및 Stream Analytic으로 수행할 수 있는 새로운 작업이 많이 있으며 이를 통해 새로운 가능성이 열릴 수 있기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-191">We’re excited about the new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="c4111-192">앞으로 원하는 기능에 대한 의견이 있는 경우 [Azure UserVoice 사이트](https://feedback.azure.com/forums/270577-stream-analytics)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="c4111-192">If you have any feedback on what you want next, feel free to use the [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="c4111-193">Microsoft Azure를 처음 사용하는 경우 [무료 Azure 평가판 계정](https://azure.microsoft.com/pricing/free-trial/)을 등록하여 사용해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-193">If you are new Microsoft Azure, we invite you to try it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="c4111-194">Stream Analytic을 처음 사용하는 경우 [첫 번째 Stream Analytic 작업을 만들어](stream-analytics-create-a-job.md)볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-194">If you are new to Stream Analytics, then we invite you to [create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="c4111-195">도움말이 필요하거나 질문이 있는 경우 [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) 또는 [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) 포럼에 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="c4111-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="c4111-196">다음 리소스를 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4111-196">You can also see the following resources:</span></span>

* [<span data-ttu-id="c4111-197">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="c4111-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="c4111-198">Azure Functions C# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="c4111-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="c4111-199">Azure Functions F# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="c4111-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="c4111-200">Azure Functions NodeJS 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="c4111-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="c4111-201">Azure Functions 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="c4111-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="c4111-202">Azure Redis Cache를 모니터링하는 방법</span><span class="sxs-lookup"><span data-stu-id="c4111-202">How to monitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="c4111-203">최신 소식과 기능에 대한 최신 동향을 파악하려면 Twitter의 [@AzureStreaming](https://twitter.com/AzureStreaming)을 팔로우하세요.</span><span class="sxs-lookup"><span data-stu-id="c4111-203">To stay up-to-date on all the latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
