# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a><span data-ttu-id="c72f6-101">Azure Stream Analytics 사용 시작 : 실시간 부정 행위 감지</span><span class="sxs-lookup"><span data-stu-id="c72f6-101">Get started using Azure Stream Analytics: Real-time fraud detection</span></span>

<span data-ttu-id="c72f6-102">이 자습서에서는 Azure Stream Analytics를 사용하는 방법에 대한 종단 간 일러스트레이션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-102">This tutorial provides an end-to-end illustration of how to use Azure Stream Analytics.</span></span> <span data-ttu-id="c72f6-103">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-103">You learn how to:</span></span> 

* <span data-ttu-id="c72f6-104">스트리밍 이벤트를 Azure Event Hubs의 인스턴스로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-104">Bring streaming events into an instance of Azure Event Hubs.</span></span> <span data-ttu-id="c72f6-105">이 자습서에서는 휴대폰 메타데이터 레코드 스트림을 시뮬레이션하도록 제공하는 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-105">In this tutorial, you'll use an app that we provide that simulates a stream of mobile-phone metadata records.</span></span>

* <span data-ttu-id="c72f6-106">SQL과 유사한 Stream Analytics 쿼리를 작성하여 데이터, 집계 정보를 변환하고 패턴을 찾아냅니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-106">Write SQL-like Stream Analytics queries to transform data, aggregating information or looking for patterns.</span></span> <span data-ttu-id="c72f6-107">쿼리를 사용하여 들어오는 스트림을 검사하고 사기성일 수 있는 호출을 찾아내는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-107">You will see how to use a query to examine the incoming stream and look for calls that might be fraudulent.</span></span>

* <span data-ttu-id="c72f6-108">추가 정보를 분석할 수 있는 출력 싱크(저장소)로 결과를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-108">Send the results to an output sink (storage) that you can analyze for additional insights.</span></span> <span data-ttu-id="c72f6-109">이 경우 의심스러운 호출 데이터를 Azure Blob Storage로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-109">In this case, you'll send the suspicious call data to Azure Blob storage.</span></span>

<span data-ttu-id="c72f6-110">이 자습서에서는 전화 통화 데이터를 기반으로 하는 실시간 부정 행위 감지의 예를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-110">In  this tutorial, we use the example of real-time fraud detection based on phone-call data.</span></span> <span data-ttu-id="c72f6-111">하지만 여기서 설명하는 기법은 신용카드 사기 또는 ID 도용 같은 다른 유형의 부정 행위 감지에도 적용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-111">But the technique we illustrate is also suited for other types of fraud detection, such as credit card fraud or identity theft.</span></span> 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a><span data-ttu-id="c72f6-112">시나리오: 실시간으로 통신 및 SIM 사기 감지</span><span class="sxs-lookup"><span data-stu-id="c72f6-112">Scenario: Telecommunications and SIM fraud detection in real time</span></span>

<span data-ttu-id="c72f6-113">통신 회사에는 많은 양의 들어오는 호출 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-113">A telecommunications company has a large volume of data for incoming calls.</span></span> <span data-ttu-id="c72f6-114">회사에서는 고객에게 사기성 호출을 알리거나 고객이 특정 번호에 대한 서비스를 종료할 수 있도록 실시간으로 사기성 호출을 감지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-114">The company wants to detect fraudulent calls in real time so that they can notify customers or shut down service for a specific number.</span></span> <span data-ttu-id="c72f6-115">SIM 사기의 한 유형으로, 지리적으로 다른 위치에서 동일한 ID로 동시에 여러 호출을 이루어지는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-115">One type of SIM fraud involves multiple calls from the same identity around the same time but in geographically different locations.</span></span> <span data-ttu-id="c72f6-116">이러한 유형의 사기 행위를 감지하기 위해 회사는 들어오는 전화 레코드를 검토하고 특정 패턴을 찾아냅니다. 이 경우 서로 다른 국가에서 동시에 호출이 발생하는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-116">To detect this type of fraud, the company needs to examine incoming phone records and look for specific patterns—in this case, for calls made around the same time in different countries.</span></span> <span data-ttu-id="c72f6-117">이 범주에 속하는 모든 전화 레코드는 후속 분석을 위해 저장소에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-117">Any phone records that fall into this category are written to storage for subsequent analysis.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c72f6-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c72f6-118">Prerequisites</span></span>

<span data-ttu-id="c72f6-119">이 자습서에서는 샘플 전화 통화 메타데이터를 생성하는 클라이언트 앱을 사용하여 전화 통화 데이터를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-119">In this tutorial, you'll simulate phone-call data by using a client app that generates sample phone call metadata.</span></span> <span data-ttu-id="c72f6-120">앱에서 생성하는 일부 레코드는 사기성 호출과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-120">Some of the records that the app produces look like fraudulent calls.</span></span> 

<span data-ttu-id="c72f6-121">시작하기 전에 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-121">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="c72f6-122">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="c72f6-122">An Azure account.</span></span>
* <span data-ttu-id="c72f6-123">호출 이벤트 생성기 앱.</span><span class="sxs-lookup"><span data-stu-id="c72f6-123">The call-event generator app.</span></span> <span data-ttu-id="c72f6-124">Microsoft 다운로드 센터에서 [TelcoGenerator.zip 파일](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip)을 다운로드하여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-124">You can get this by downloading the [TelcoGenerator.zip file](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) from the Microsoft Download Center.</span></span> <span data-ttu-id="c72f6-125">컴퓨터의 폴더에 이 패키지의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-125">Unzip this package into a folder on your computer.</span></span> <span data-ttu-id="c72f6-126">소스 코드를 확인하고 디버거에서 앱을 실행하려면 [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator)에서 앱 소스 코드를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-126">If you want to see the source code and run the app in a debugger, you can get the app source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="c72f6-127">Windows에서 다운로드한 .zip 파일을 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-127">Windows might block the downloaded .zip file.</span></span> <span data-ttu-id="c72f6-128">압축을 풀 수 없는 경우 해당 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-128">If you can't unzip it, right-click the file and select **Properties**.</span></span> <span data-ttu-id="c72f6-129">“이 파일은 다른 컴퓨터로부터 왔으며 사용자의 컴퓨터를 보호하기 위해 차단되었을 수도 있습니다.”라는 메시지가 표시되면 **차단 해제** 옵션을 선택하여 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-129">If you see the "This file came from another computer and might be blocked to help protect this computer" message, select the **Unblock** option and then click **Apply**.</span></span>

<span data-ttu-id="c72f6-130">Streaming Analytics 작업 결과를 확인하려면 Azure Blob Storage 컨테이너의 내용을 보기 위한 도구도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-130">If you want to examine the results of the Streaming Analytics job, you also need a tool for viewing the contents of a Azure Blob Storage container.</span></span> <span data-ttu-id="c72f6-131">Visual Studio를 사용하는 경우 [Visual Studio용 Azure 도구](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) 또는 [Visual Studio 클라우드 탐색기](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-131">If you use Visual Studio, you can use [Azure Tools for Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) or [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer).</span></span> <span data-ttu-id="c72f6-132">또는 [Azure Storage 탐색기](http://storageexplorer.com/) 또는 [Azure 탐색기](http://www.cerebrata.com/products/azure-explorer/introduction)와 같은 독립 실행형 도구를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-132">Alternatively, you can install standalone tools like [Azure Storage Explorer](http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction).</span></span> 

## <a name="create-an-azure-event-hubs-to-ingest-events"></a><span data-ttu-id="c72f6-133">이벤트를 수집할 Azure Event Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="c72f6-133">Create an Azure event hubs to ingest events</span></span>

<span data-ttu-id="c72f6-134">데이터 스트림을 분석하기 위해 Azure로 *수집*합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-134">To analyze a data stream, you *ingest* it into Azure.</span></span> <span data-ttu-id="c72f6-135">데이터를 수집하는 일반적인 방법은 [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)를 사용하는 것이며, 이를 통해 초당 수백만 이벤트를 수집한 다음 이벤트 정보를 처리 및 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-135">A typical way to ingest data is to use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md), which lets you ingest millions of events per second and then process and store the event information.</span></span> <span data-ttu-id="c72f6-136">이 자습서에서는 이벤트 허브를 만든 후 호출 이벤트 생성기 앱에서 호출 데이터를 이벤트 허브로 보내도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-136">For this tutorial, you create an event hub and then have the call-event generator app send call data to that event hub.</span></span> <span data-ttu-id="c72f6-137">이벤트 허브에 대한 자세한 내용은 [Azure Service Bus 설명서](https://docs.microsoft.com/en-us/azure/service-bus/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72f6-137">For more about event hubs, see the [Azure Service Bus documentation](https://docs.microsoft.com/en-us/azure/service-bus/).</span></span>

>[!NOTE]
><span data-ttu-id="c72f6-138">이 절차의 보다 자세한 버전은 [Azure Portal을 사용하여 Event Hubs 네임스페이스 및 이벤트 허브 만들기](../event-hubs/event-hubs-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72f6-138">For a more detailed version of this procedure, see [Create an Event Hubs namespace and an event hub using the Azure portal](../event-hubs/event-hubs-create.md).</span></span> 

### <a name="create-a-namespace-and-event-hub"></a><span data-ttu-id="c72f6-139">네임스페이스 및 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="c72f6-139">Create a namespace and event hub</span></span>
<span data-ttu-id="c72f6-140">이 절차에서는 이벤트 허브 네임스페이스를 먼저 만든 후 이벤트 허브를 해당 네임스페이스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-140">In this procedure, you first create an event hub namespace, and then you add an event hub to that namepsace.</span></span> <span data-ttu-id="c72f6-141">이벤트 허브 네임스페이스는 관련된 이벤트 버스 인스턴스를 논리적으로 그룹화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-141">Event hub namespaces are used to logically group related event bus instances.</span></span> 

1. <span data-ttu-id="c72f6-142">Azure Portal에 로그인하고 **새로 만들기** > **사물 인터넷** > **이벤트 허브**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-142">Log  into the Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="c72f6-143">**네임스페이스 만들기** 블레이드에서 네임스페이스 이름을 입력합니다(예: `<yourname>-eh-ns-demo`).</span><span class="sxs-lookup"><span data-stu-id="c72f6-143">In the **Create namespace** blade, enter a namespace name such as `<yourname>-eh-ns-demo`.</span></span> <span data-ttu-id="c72f6-144">네임스페이스에 어떤 이름이든 사용할 수 있지만 이름은 URL에 대해 유효해야 하며 Azure 전체에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-144">You can use any name for the namespace, but the name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="c72f6-145">구독을 선택하고 리소스 그룹을 만들거나 선택한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-145">Select a subscription and create or choose a resource group , then click **Create**.</span></span> 

    ![이벤트 허브 네임스페이스 만들기](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. <span data-ttu-id="c72f6-147">네임스페이스에서 배포를 완료했으면 Azure 리소스 목록에서 이벤트 허브 네임스페이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-147">When the namespace has finished deploying, find the event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="c72f6-148">새 네임스페이스를 클릭하고 네임스페이스 블레이드에서 **+&nbsp;이벤트 허브**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-148">Click the new namespace, and in the namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="c72f6-149">새 이벤트 허브를 만들기 위한 이벤트 허브 추가 단추</span><span class="sxs-lookup"><span data-stu-id="c72f6-149">The Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. <span data-ttu-id="c72f6-150">새 이벤트 허브 이름을 `sa-eh-frauddetection-demo`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-150">Name the new event hub `sa-eh-frauddetection-demo`.</span></span> <span data-ttu-id="c72f6-151">다른 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-151">You can use a different name.</span></span> <span data-ttu-id="c72f6-152">이 경우 나중에 이름이 필요하기 때문에 메모해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-152">If you do, make a note of it, because you need the name later.</span></span> <span data-ttu-id="c72f6-153">지금 당장은 이벤트 허브에 다른 옵션을 설정하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-153">You don't need to set any other options for the event hub right now.</span></span>

    ![새 이벤트 허브를 만들기 위한 블레이드](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. <span data-ttu-id="c72f6-155">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-155">Click **Create**.</span></span>
### <a name="grant-access-to-the-event-hub-and-get-a-connection-string"></a><span data-ttu-id="c72f6-156">이벤트 허브에 대한 액세스 부여 및 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="c72f6-156">Grant access to the event hub and get a connection string</span></span>

<span data-ttu-id="c72f6-157">프로세스에서 이벤트 허브로 데이터를 보낼 수 있으려면 이벤트 허브에 적절한 액세스 권한을 허용하는 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-157">Before a process can send data to an event hub, the event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="c72f6-158">액세스 정책은 권한 부여 정보를 포함하는 연결 문자열을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-158">The access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="c72f6-159">이벤트 네임스페이스 블레이드에서 **이벤트 허브**를 클릭하고 새 이벤트 허브의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-159">In the event namespace blade, click **Event Hubs** and then click the name of your new event hub.</span></span>

2.  <span data-ttu-id="c72f6-160">이벤트 허브 블레이드에서 **공유 액세스 정책**을 클릭한 후 **+&nbsp;추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-160">In the event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="c72f6-161">이벤트 허브 네임스페이스가 아니라 이벤트 허브로 작업하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-161">Make sure you're working with the event hub, not the event hub namespace.</span></span>

3.  <span data-ttu-id="c72f6-162">**클레임**에 대해 `sa-policy-manage-demo`라는 이름의 정책을 추가하고 **관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-162">Add a policy named `sa-policy-manage-demo` and for **Claim**, select **Manage**.</span></span>

    ![새 이벤트 허브 액세스 정책을 만들기 위한 블레이드](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  <span data-ttu-id="c72f6-164">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-164">Click **Create**.</span></span>

5.  <span data-ttu-id="c72f6-165">정책이 배포되었으면 공유 액세스 정책 목록에서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-165">After the policy has been deployed, click it in the list of shared access policies.</span></span>

6.  <span data-ttu-id="c72f6-166">**CONNECTION STRING-PRIMARY KEY**로 레이블이 지정된 상자를 찾고 연결 문자열 옆의 복사 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-166">Find the box labeled **CONNECTION STRING-PRIMARY KEY** and click the copy button next to the connection string.</span></span> 
    
    ![액세스 정책에서 기본 연결 문자열 키 복사](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  <span data-ttu-id="c72f6-168">연결 문자열을 텍스트 편집기에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-168">Paste the connection string into a text editor.</span></span> <span data-ttu-id="c72f6-169">다음 섹션에서 몇 가지 편집을 수행한 후 이 연결 문자열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-169">You need this connection string for the next section, after you make some small edits to it.</span></span>

    <span data-ttu-id="c72f6-170">연결 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-170">The connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    <span data-ttu-id="c72f6-171">연결 문자열에는 세미콜론으로 구분된 여러 키-값 쌍이 포함되어 있습니다(`Endpoint`, `SharedAccessKeyName`, `SharedAccessKey` 및 `EntityPath`).</span><span class="sxs-lookup"><span data-stu-id="c72f6-171">Notice that the connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

## <a name="configure-and-start-the-event-generator-application"></a><span data-ttu-id="c72f6-172">이벤트 생성기 응용 프로그램 구성 및 시작</span><span class="sxs-lookup"><span data-stu-id="c72f6-172">Configure and start the event generator application</span></span>

<span data-ttu-id="c72f6-173">TelcoGenerator 앱을 시작하기 전에 호출 레코드를 방금 만든 이벤트 허브에 전송할 수 있도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-173">Before you start the TelcoGenerator app, you configure it so that it will send call records to the event hub you just created.</span></span>

### <a name="configure-the-telcogeneratorapp"></a><span data-ttu-id="c72f6-174">TelcoGeneratorapp 구성</span><span class="sxs-lookup"><span data-stu-id="c72f6-174">Configure the TelcoGeneratorapp</span></span>

1.  <span data-ttu-id="c72f6-175">연결 문자열을 복사한 편집기에서 `EntityPath` 값을 기록해둔 후 `EntityPath` 쌍을 제거합니다(앞에 있는 세미콜론을 반드시 제거).</span><span class="sxs-lookup"><span data-stu-id="c72f6-175">In the editor where you copied the connection string, make a note of the `EntityPath` value, and then remove the `EntityPath` pair (don't forget to remove the semicolon that precedes it).</span></span> 

2.  <span data-ttu-id="c72f6-176">TelcoGenerator.zip 파일의 압축을 푼 폴더에서 편집기로 telcodatagen.exe.config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-176">In the folder where you unzipped the TelcoGenerator.zip file, open the telcodatagen.exe.config file in an editor.</span></span> <span data-ttu-id="c72f6-177">(둘 이상의 .config 파일이 있으므로 해당 파일을 열어야 함)</span><span class="sxs-lookup"><span data-stu-id="c72f6-177">(There is more than one .config file, so be sure that you open the right one.)</span></span>

3.  <span data-ttu-id="c72f6-178">`<appSettings>` 요소에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-178">In the `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="c72f6-179">`EventHubName` 키 값을 이벤트 허브 이름으로 설정합니다(즉, 엔터티 경로 값).</span><span class="sxs-lookup"><span data-stu-id="c72f6-179">Set the value of the `EventHubName` key to the event hub name (that is, to the value of the entity path).</span></span>
    * <span data-ttu-id="c72f6-180">`Microsoft.ServiceBus.ConnectionString` 키 값을 연결 문자열로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-180">Set the value of the `Microsoft.ServiceBus.ConnectionString` key to the connection string.</span></span> 

    <span data-ttu-id="c72f6-181">`<appSettings>` 섹션은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-181">The `<appSettings>` section will look like the following example.</span></span> <span data-ttu-id="c72f6-182">(쉽게 이해할 수 있도록 줄을 래핑하고 권한 부여 토큰에서 일부 문자를 제거했음)</span><span class="sxs-lookup"><span data-stu-id="c72f6-182">(For clarity, we wrapped the lines and removed some characters from the authorization token.)</span></span>

    ![이벤트 허브 이름 및 연결 문자열을 보여 주는 TelcoGenerator 앱 구성 파일](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  <span data-ttu-id="c72f6-184">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-184">Save the file.</span></span> 

### <a name="start-the-app"></a><span data-ttu-id="c72f6-185">앱 시작</span><span class="sxs-lookup"><span data-stu-id="c72f6-185">Start the app</span></span>
1.  <span data-ttu-id="c72f6-186">명령 창을 열고 TelcoGenerator 앱이 압축 해제된 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-186">Open a command window and change to the folder where the TelcoGenerator app is unzipped.</span></span>
2.  <span data-ttu-id="c72f6-187">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-187">Enter the following command:</span></span>

        telcodatagen.exe 1000 .2 2

    <span data-ttu-id="c72f6-188">매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-188">The parameters are:</span></span> 

    * <span data-ttu-id="c72f6-189">시간당 CDR 수.</span><span class="sxs-lookup"><span data-stu-id="c72f6-189">Number of CDRs per hour.</span></span> 
    * <span data-ttu-id="c72f6-190">SIM 카드 사기 확률: 앱에서 사기성 호출을 시뮬레이션하게 되는 전체 호출 대비 백분율로의 빈도</span><span class="sxs-lookup"><span data-stu-id="c72f6-190">SIM Card Fraud Probability: How often, as a percentage of all calls, that the app should simulate a fraudulent call.</span></span> <span data-ttu-id="c72f6-191">값 .2는 호출 레코드의 약 20%가 사기성으로 나타남을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-191">The value .2 means that about 20% of the call records will look fraudulent.</span></span>
    * <span data-ttu-id="c72f6-192">기간(시간).</span><span class="sxs-lookup"><span data-stu-id="c72f6-192">Duration in hours.</span></span> <span data-ttu-id="c72f6-193">앱이 실행되는 시간.</span><span class="sxs-lookup"><span data-stu-id="c72f6-193">The number of hours that the app should run.</span></span> <span data-ttu-id="c72f6-194">명령줄에서 Ctrl + C를 눌러 언제든지 앱을 중지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-194">You can also stop the app any time by pressing Ctrl+C at the command line.</span></span>

    <span data-ttu-id="c72f6-195">몇 초 후 앱에서 이벤트 허브로 데이터를 전송함에 따라 화면에 전화 통화 레코드가 표시되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-195">After a few seconds, the app starts displaying phone call records on the screen as it sends them to the event hub.</span></span>

<span data-ttu-id="c72f6-196">이 실시간 사기 감지 응용 프로그램에서 사용할 수 있는 일부 키 필드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-196">Some of the key fields that you will be using in this real-time fraud detection application are the following:</span></span>

|<span data-ttu-id="c72f6-197">**레코드**</span><span class="sxs-lookup"><span data-stu-id="c72f6-197">**Record**</span></span>|<span data-ttu-id="c72f6-198">**정의**</span><span class="sxs-lookup"><span data-stu-id="c72f6-198">**Definition**</span></span>|
|----------|--------------|
|`CallrecTime`|<span data-ttu-id="c72f6-199">호출 시작 시간에 대한 타임스탬프</span><span class="sxs-lookup"><span data-stu-id="c72f6-199">The timestamp for the call start time.</span></span> |
|`SwitchNum`|<span data-ttu-id="c72f6-200">호출 연결에 사용되는 전화 스위치.</span><span class="sxs-lookup"><span data-stu-id="c72f6-200">The telephone switch used to connect the call.</span></span> <span data-ttu-id="c72f6-201">이 예에서는 스위치는 발신 국가(미국, 중국, 영국, 독일 또는 오스트레일리아)를 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-201">For this example, the switches are strings that represent the country of origin (US, China, UK, Germany, or Australia).</span></span> |
|`CallingNum`|<span data-ttu-id="c72f6-202">호출자의 전화번호.</span><span class="sxs-lookup"><span data-stu-id="c72f6-202">The phone number of the caller.</span></span> |
|`CallingIMSI`|<span data-ttu-id="c72f6-203">국제 모바일 구독자 ID(IMSI)</span><span class="sxs-lookup"><span data-stu-id="c72f6-203">The International Mobile Subscriber Identity (IMSI).</span></span> <span data-ttu-id="c72f6-204">호출자의 고유 식별자.</span><span class="sxs-lookup"><span data-stu-id="c72f6-204">This is the Unique identifier of the caller.</span></span> |
|`CalledNum`|<span data-ttu-id="c72f6-205">호출 수신자의 전화번호.</span><span class="sxs-lookup"><span data-stu-id="c72f6-205">The phone number of the call recipient.</span></span> |
|`CalledIMSI`|<span data-ttu-id="c72f6-206">국제 모바일 구독자 ID(IMSI)</span><span class="sxs-lookup"><span data-stu-id="c72f6-206">International Mobile Subscriber Identity (IMSI).</span></span> <span data-ttu-id="c72f6-207">호출 수신자의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-207">This is the unique identifier of the call recipient.</span></span> |


## <a name="create-a-stream-analytics-job-to-manage-streaming-data"></a><span data-ttu-id="c72f6-208">스트리밍 데이터를 관리하는 Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="c72f6-208">Create a Stream Analytics job to manage streaming data</span></span>

<span data-ttu-id="c72f6-209">이제 호출 이벤트 스트림이 있고 Stream Analytics 작업을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-209">Now that you have a stream of call events, you can set up a Stream Analytics job.</span></span> <span data-ttu-id="c72f6-210">이 작업은 설정한 이벤트 허브에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-210">The job will read data from the event hub that you set up.</span></span> 

### <a name="create-the-job"></a><span data-ttu-id="c72f6-211">작업 만들기</span><span class="sxs-lookup"><span data-stu-id="c72f6-211">Create the job</span></span> 

1. <span data-ttu-id="c72f6-212">Azure Portal에서 **새로 만들기** > **사물 인터넷** > **Stream Analytics 작업**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-212">In the Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="c72f6-213">작업 이름을 `sa_frauddetection_job_demo`로 지정하고 구독, 리소스 그룹 및 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-213">Name the job `sa_frauddetection_job_demo`, specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="c72f6-214">최상의 성능을 위해 동일한 지역에 작업 및 이벤트 허브를 배치하는 것이 좋으며 지역 간에 데이터를 전송하는 데 비용을 지불하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-214">It's a good idea to place the job and the event hub in the same region for best performance and so that you don't pay to transfer data between regions.</span></span>

    ![새 Stream Analytics 작업 만들기](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. <span data-ttu-id="c72f6-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-216">Click **Create**.</span></span>

    <span data-ttu-id="c72f6-217">작업이 만들어지고 포털에 작업 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-217">The job is created and the portal displays job details.</span></span> <span data-ttu-id="c72f6-218">아직 아무 것도 실행되지 않지만 시작하려면 작업을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-218">Nothing is running yet, though—you have to configure the job before it can be started.</span></span>

### <a name="configure-job-input"></a><span data-ttu-id="c72f6-219">작업 입력 구성</span><span class="sxs-lookup"><span data-stu-id="c72f6-219">Configure job input</span></span>

1. <span data-ttu-id="c72f6-220">대시보드 또는 **모든 리소스** 블레이드에서 `sa_frauddetection_job_demo` Stream Analytics 작업을 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-220">In the dashboard or the **All resources** blade, find and select the `sa_frauddetection_job_demo` Stream Analytics job.</span></span> 
2. <span data-ttu-id="c72f6-221">Stream Analytics 작업 블레이드의 **작업 토폴로지** 섹션에서 **입력** 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-221">In the **Job Topology** section of the Stream Analytics job blade, click the **Input** box.</span></span>

    ![Streaming Analytics 작업 블레이드에서 토폴로지 아래 입력 상자](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. <span data-ttu-id="c72f6-223">**+&nbsp;추가**를 클릭한 후 블레이드를 다음 값으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-223">Click **+&nbsp;Add** and then fill out the blade with these values:</span></span>

    * <span data-ttu-id="c72f6-224">**입력 별칭**: 이름으로 `CallStream`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-224">**Input alias**: Use the name `CallStream`.</span></span> <span data-ttu-id="c72f6-225">다른 이름을 사용하는 경우 나중에 필요하므로 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-225">If you use a different name, make a note of it because you'll need it later.</span></span>
    * <span data-ttu-id="c72f6-226">**원본 형식**: **데이터 스트림**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-226">**Source type**: Select **Data stream**.</span></span> <span data-ttu-id="c72f6-227">(**참조 데이터**는 이 자습서에서 사용하지 않는 정적 조회 데이터를 나타냄)</span><span class="sxs-lookup"><span data-stu-id="c72f6-227">(**Reference data** refers to static lookup data, which you won't use in this tutorial.)</span></span>
    * <span data-ttu-id="c72f6-228">**원본**: **이벤트 허브**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-228">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="c72f6-229">**가져오기 옵션**: **현재 구독의 이벤트 허브 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-229">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="c72f6-230">**서비스 버스 네임스페이스**: 이전에 만든 이벤트 허브 네임스페이스를 선택합니다(`<yourname>-eh-ns-demo`).</span><span class="sxs-lookup"><span data-stu-id="c72f6-230">**Service bus namespace**: Select the event hub namespace that you created earlier (`<yourname>-eh-ns-demo`).</span></span>
    * <span data-ttu-id="c72f6-231">**이벤트 허브**: 이전에 만든 이벤트 허브를 선택합니다(`sa-eh-frauddetection-demo`).</span><span class="sxs-lookup"><span data-stu-id="c72f6-231">**Event hub**: Select the event hub that you created earlier (`sa-eh-frauddetection-demo`).</span></span>
    * <span data-ttu-id="c72f6-232">**이벤트 허브 정책 이름**: 앞부분에서 만든 액세스 정책을 선택합니다(`sa-policy-manage-demo`).</span><span class="sxs-lookup"><span data-stu-id="c72f6-232">**Event hub policy name**: Select the access policy that you created earlier (`sa-policy-manage-demo`).</span></span>

    ![Streaming Analytics 작업에 대한 새 입력 만들기](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="c72f6-234">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-234">Click **Create**.</span></span>

## <a name="create-queries-to-transform-real-time-data"></a><span data-ttu-id="c72f6-235">실시간 데이터를 변환하는 쿼리 만들기</span><span class="sxs-lookup"><span data-stu-id="c72f6-235">Create queries to transform real-time data</span></span>

<span data-ttu-id="c72f6-236">이 시점에는 들어오는 데이터 스트림을 읽도록 설정된 Stream Analytics 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-236">At this point, you have a Stream Analytics job set up to read an incoming data stream.</span></span> <span data-ttu-id="c72f6-237">다음 단계는 실시간으로 데이터를 분석하는 변환을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-237">The next step is to create a transformation that analyzes the data in real time.</span></span> <span data-ttu-id="c72f6-238">쿼리를 만들어 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-238">You do this by creating a query.</span></span> <span data-ttu-id="c72f6-239">Stream Analytics는 실시간 처리에 대해 변환을 설명하는 간단하고 선언적인 쿼리 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-239">Stream Analytics supports a simple, declarative query model that describes transformations for real-time processing.</span></span> <span data-ttu-id="c72f6-240">쿼리는 스트림 분석과 관련된 일부 확장 기능을 포함한 SQL과 유사한 언어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-240">The queries use a SQL-like language that has some extensions specific to stream analytics.</span></span> 

<span data-ttu-id="c72f6-241">매우 간단한 쿼리로 들어오는 모든 데이터를 단순히 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-241">A very simple query might simply read all the incoming data.</span></span> <span data-ttu-id="c72f6-242">그러나 보통은 데이터에서 특정 데이터 또는 관계를 찾는 쿼리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-242">However, you often create queries that look for specific data or for relationships in the data.</span></span> <span data-ttu-id="c72f6-243">자습서의 이 섹션에서는 분석을 위해 입력 스트림을 변환할 수 있는 몇 가지 방법에 대해 알아보기 위해 여러 쿼리를 작성 및 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-243">In this section of the tutorial, you will create and test several queries to learn a few ways in which you can transform an input stream for analysis.</span></span> 

<span data-ttu-id="c72f6-244">여기서 작성한 쿼리는 화면에 변환된 데이터를 표시하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-244">The queries you create here will just display the transformed data to the screen.</span></span> <span data-ttu-id="c72f6-245">이후 섹션에서는 출력 싱크 및 변환된 데이터를 해당 싱크에 기록하는 쿼리를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-245">In a later section, you'll configure an output sink and a query that writes the transformed data to that sink.</span></span>

<span data-ttu-id="c72f6-246">이 언어에 대한 자세한 내용은 [Azure Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/dn834998.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72f6-246">To learn more about the language, see the [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/dn834998.aspx).</span></span>

### <a name="get-sample-data-for-testing-queries"></a><span data-ttu-id="c72f6-247">쿼리를 테스트하기 위한 샘플 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="c72f6-247">Get sample data for testing queries</span></span>

<span data-ttu-id="c72f6-248">TelcoGenerator 앱은 호출 레코드를 이벤트 허브로 보내고 Stream Analytics 작업은 이벤트 허브에서 읽어오도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-248">The TelcoGenerator app is sending call records to the event hub, and your Stream Analytics job is configured to read from the event hub.</span></span> <span data-ttu-id="c72f6-249">쿼리로 작업을 테스트하여 올바르게 읽고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-249">You can use a query to test the job to make sure that it's reading correctly.</span></span> <span data-ttu-id="c72f6-250">Azure 콘솔에서 쿼리를 테스트하려면 샘플 데이터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-250">To  test a query in the Azure console, you need sample data.</span></span> <span data-ttu-id="c72f6-251">이 연습에서는 이벤트 허브로 들어오는 스트림에서 샘플 데이터를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-251">For this walkthrough, you'll extract sample data from the stream that's coming into the event hub.</span></span>

1. <span data-ttu-id="c72f6-252">TelcoGenerator 앱이 실행 중이고 호출 레코드를 생성하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-252">Make sure that the TelcoGenerator app is running and producing call records.</span></span>
2. <span data-ttu-id="c72f6-253">포털에서 Streaming Analytics 작업 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-253">In the portal, return to the Streaming Analytics job blade.</span></span> <span data-ttu-id="c72f6-254">(블레이드를 닫은 경우 **모든 리소스** 블레이드에서 `sa_frauddetection_job_demo`를 검색)</span><span class="sxs-lookup"><span data-stu-id="c72f6-254">(If you closed the blade, search for `sa_frauddetection_job_demo` in the **All resources** blade.)</span></span>
3. <span data-ttu-id="c72f6-255">**쿼리** 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-255">Click the **Query** box.</span></span> <span data-ttu-id="c72f6-256">Azure에서는 작업에 대해 구성된 입력 및 출력을 나열하고 데이터가 출력으로 전송됨에 따라 사용자가 입력 스트림을 변환하는 쿼리를 작성할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-256">Azure lists the inputs and outputs that are configured for the job, and lets you create a query that lets you transform the input stream as it is sent to the output.</span></span>
4. <span data-ttu-id="c72f6-257">**쿼리** 블레이드에서 `CallStream` 입력 옆에 있는 점을 클릭한 후 **입력의 샘플 데이터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-257">In the **Query** blade, click the dots next to the `CallStream` input and then select **Sample data from input**.</span></span>

    ![Streaming Analytics 작업 항목에 대해 샘플 데이터를 사용하는 메뉴 옵션, “입력의 샘플 데이터” 선택됨](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="c72f6-259">그러면 입력 스트림을 읽는 시간에 따라 정의된, 가져올 샘플 데이터의 양을 지정할 수 있는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-259">This opens a blade that lets you specify how much sample data to get, defined in terms of how long to read the input stream.</span></span>

5. <span data-ttu-id="c72f6-260">**분**을 3으로 설정한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-260">Set **Minutes** to 3 and then click **OK**.</span></span> 
    
    ![입력 스트림을 샘플링하는 옵션, “3분” 선택됨](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="c72f6-262">Azure에서는 입력 스트림의 3분 분량의 데이터를 샘플링하고 샘플 데이터가 준비되면 이를 사용자에게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-262">Azure samples 3 minutes' worth of data from the input stream and notifies you when the sample data is ready.</span></span> <span data-ttu-id="c72f6-263">(짧은 시간이 소요됩니다.)</span><span class="sxs-lookup"><span data-stu-id="c72f6-263">(This takes a short while.)</span></span> 

<span data-ttu-id="c72f6-264">샘플 데이터는 임시로 저장되었다가 쿼리 창이 열려 있는 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-264">The sample data is stored temporarily and is available while you have the query window open.</span></span> <span data-ttu-id="c72f6-265">쿼리 창을 닫으면 샘플 데이터가 무시되고 새로운 샘플 데이터 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-265">If you close the query window, the sample data is discarded, and you'll have to create a new set of sample data.</span></span> 

<span data-ttu-id="c72f6-266">대안으로, 안에 샘플 데이터가 있는 .json 파일을 [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json)에서 가져온 후 `CallStream` 입력에 대한 샘플 데이터로 사용할 .json 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-266">As an alternative, you can get a .json file that has sample data in it [from GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json), and then upload that .json file to use as sample data for the `CallStream` input .</span></span> 

### <a name="test-using-a-pass-through-query"></a><span data-ttu-id="c72f6-267">통과 쿼리를 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="c72f6-267">Test using a pass-through query</span></span>

<span data-ttu-id="c72f6-268">모든 이벤트를 보관하려는 경우 통과 쿼리를 사용하여 이벤트의 페이로드에서 모든 필드를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-268">If you want to archive every event, you can use a pass-through query to read all the fields in the payload of the event.</span></span>

1. <span data-ttu-id="c72f6-269">쿼리 창에서 다음 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-269">In the query window, enter this query:</span></span>

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    ><span data-ttu-id="c72f6-270">SQL처럼 키워드는 대/소문자를 구분하지 않고 공백은 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-270">As with SQL, keywords are not case sensitive, and whitespace is not significant.</span></span>

    <span data-ttu-id="c72f6-271">쿼리에서 `CallStream`은 입력을 만들 때 지정한 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-271">In this query, `CallStream` is the alias that you specified when you created the input.</span></span> <span data-ttu-id="c72f6-272">다른 별칭을 사용하는 경우 대신 해당 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-272">If you used a different alias, use that name instead.</span></span>

2. <span data-ttu-id="c72f6-273">**테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-273">Click **Test**.</span></span>

    <span data-ttu-id="c72f6-274">Stream Analytics 작업이 샘플 데이터에 대해 쿼리를 실행하고 창 맨 아래 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-274">The Stream Analytics job runs the query against the sample data and displays the output at the bottom of the window.</span></span> <span data-ttu-id="c72f6-275">그러면 이벤트 허브 및 Stream Analytics 작업이 올바르게 구성된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-275">This tells you that the event hub and the Streaming Analytics job are configured correctly.</span></span> <span data-ttu-id="c72f6-276">(설명했듯이, 나중에 쿼리에서 데이터를 쓸 수 있는 출력 싱크를 만듭니다.)</span><span class="sxs-lookup"><span data-stu-id="c72f6-276">(As noted, later you'll create an output sink that the query can write data to.)</span></span>

    ![Stream Analytics 작업 출력, 73개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    <span data-ttu-id="c72f6-278">표시되는 레코드의 정확한 수는 3분 샘플에 캡처된 레코드 수에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-278">The exact number of records you see will depend on how many records were captured in your 3-minute sample.</span></span>
 
### <a name="reduce-the-number-of-fields-using-a-column-projection"></a><span data-ttu-id="c72f6-279">열 프로젝션을 사용하여 필드 수 줄이기</span><span class="sxs-lookup"><span data-stu-id="c72f6-279">Reduce the number of fields using a column projection</span></span>

<span data-ttu-id="c72f6-280">대부분의 경우 분석 시에 입력 스트림의 모든 열이 필요하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-280">In many cases, your analysis doesn't need all the columns from the input stream.</span></span> <span data-ttu-id="c72f6-281">쿼리를 사용하여 통과 쿼리에서보다 더 작은 집합의 반환된 필드를 프로젝션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-281">You can use a query to project a smaller set of returned fields than in the pass-through query.</span></span>

1. <span data-ttu-id="c72f6-282">코드 편집기에서 쿼리를 다음으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-282">Change the query in the code editor to the following:</span></span>

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. <span data-ttu-id="c72f6-283">**테스트**를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-283">Click **Test** again.</span></span> 

    ![프로젝션에 대한 Stream Analytics 작업 출력, 25개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a><span data-ttu-id="c72f6-285">지역별로 들어오는 호출 수: 집계를 포함하는 연속 창</span><span class="sxs-lookup"><span data-stu-id="c72f6-285">Count incoming calls by region: Tumbling window with aggregation</span></span>

<span data-ttu-id="c72f6-286">지역당 들어오는 호출의 수를 계산한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-286">Suppose you want to count the number of incoming calls per region.</span></span> <span data-ttu-id="c72f6-287">스트리밍 데이터에서 개수와 같은 집계 함수를 수행하려는 경우 데이터 스트림 자체가 사실상 무한하므로 스트림을 temporal 단위로 분할해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-287">In streaming data, when you want to perform aggregate functions like counting, you need to segment the stream into temporal units (since the data stream itself is effectively endless).</span></span> <span data-ttu-id="c72f6-288">Streaming Analytics [window 함수](stream-analytics-window-functions.md)를 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-288">You do this using a Streaming Analytics [window function](stream-analytics-window-functions.md).</span></span> <span data-ttu-id="c72f6-289">그런 다음 해당 창 내에서 데이터를 단위로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-289">You can then work with the data inside that window as a unit.</span></span>

<span data-ttu-id="c72f6-290">이 변환의 경우 겹치지 않는 temporal 창 시퀀스를 원하며 각 창에는 그룹화 및 집계할 수 있는 불연속 데이터 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-290">For this transformation, you want a sequence of temporal windows that don't overlap—each window will have a discrete set of data that you can group and aggregate.</span></span> <span data-ttu-id="c72f6-291">이러한 형식의 창을 *연속 창*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-291">This type of window is referred to as a *Tumbling window* .</span></span> <span data-ttu-id="c72f6-292">연속 창 내에서 호출이 시작된 국가를 나타내는 `SwitchNum`으로 그룹화된 들어오는 호출 수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-292">Within the Tumbling window, you can get a count of the incoming calls grouped by `SwitchNum`, which represents the country where the call originated.</span></span> 

1. <span data-ttu-id="c72f6-293">코드 편집기에서 쿼리를 다음으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-293">Change the query in the code editor to the following:</span></span>

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    <span data-ttu-id="c72f6-294">이 쿼리에서는 `FROM` 절에 `Timestamp By` 키워드를 사용하여 연속 창을 정의하는 데 사용할 입력 스트림의 타임스탬프 필드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-294">This query uses the `Timestamp By` keyword in the `FROM` clause to specify which timestamp field in the input stream to use to define the Tumbling window.</span></span> <span data-ttu-id="c72f6-295">이 경우 창은 각 레코드의 `CallRecTime` 필드에 따라 데이터를 세그먼트로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-295">In this case, the window divides the data into segments by the `CallRecTime` field in each record.</span></span> <span data-ttu-id="c72f6-296">(이 필드를 지정하지 않으면 창 작업에서 각 이벤트가 이벤트 허브에 도착한 시간을 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="c72f6-296">(If no field is specified, the windowing operation uses the time that each event arrives at the event hub.</span></span> <span data-ttu-id="c72f6-297">[Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)에서 “도착 시간과 응용 프로그램 시간”을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72f6-297">See "Arrival Time Vs Application Time" in [Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span> 

    <span data-ttu-id="c72f6-298">프로젝션에는 각 창의 끝에 대한 타임스탬프를 반환하는 `System.Timestamp`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-298">The projection includes `System.Timestamp`, which returns a timestamp for the end of each window.</span></span> 

    <span data-ttu-id="c72f6-299">연속 창을 사용할 것인지를 지정하려면 `GROUP BY `절에 [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-299">To specify that you want to use a Tumbling window, you use the [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) function in the `GROUP BY `clause.</span></span> <span data-ttu-id="c72f6-300">함수에서 시간 단위(마이크로초에서 하루까지) 및 창 크기(단위 수)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-300">In the function, you specify a time unit (anywhere from a microsecond to a day) and a window size (how many units).</span></span> <span data-ttu-id="c72f6-301">이 예제에서 연속 창은 5초 간격으로 구성되므로 5초 분량의 호출에 대한 국가별 개수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-301">In this example, the Tumbling window consists of 5-second intervals, so you will get a count by country for every 5 seconds' worth of calls.</span></span>

2. <span data-ttu-id="c72f6-302">**테스트**를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-302">Click **Test** again.</span></span> <span data-ttu-id="c72f6-303">결과에서 **WindowEnd** 아래 타임스탬프가 5초 단위로 증가하는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-303">In the results, notice that the timestamps under **WindowEnd** are in 5-second increments.</span></span>

    ![집계에 대한 Stream Analytics 작업 출력, 13개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a><span data-ttu-id="c72f6-305">셀프 조인을 사용하여 SIM 사기 감지</span><span class="sxs-lookup"><span data-stu-id="c72f6-305">Detect SIM fraud using a self-join</span></span>

<span data-ttu-id="c72f6-306">이 예제에서는 5초 이내에 서로 다른 위치에서 동일한 사용자로부터 발생한 호출을 사기성 있는 사용으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-306">For this example, we can consider fraudulent usage to be calls that originate from the same user but in different locations within 5 seconds of one another.</span></span> <span data-ttu-id="c72f6-307">예를 들어 동일한 사용자가 미국 및 오스트레일리아에서 동시에 합법적으로 전화를 걸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-307">For example, the same user can't legitimately make a call from the US and Australia at the same time.</span></span> 

<span data-ttu-id="c72f6-308">이러한 경우를 확인하려면 스트리밍 데이터의 셀프 조인을 사용하여 `CallRecTime` 값에 따라 스트림을 셀프 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-308">To check for these cases, you can use a self-join of the streaming data to join the stream to itself based on the `CallRecTime` value.</span></span> <span data-ttu-id="c72f6-309">그런 다음 `CallingIMSI` 값(발신 번호)이 동일하지만 `SwitchNum` 값(발신 국가)은 다른 호출 레코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-309">You can then look for call records where the `CallingIMSI` value (the originating number) is the same, but the `SwitchNum` value (country of origin) is not the same.</span></span>

<span data-ttu-id="c72f6-310">스트리밍 데이터에 조인을 사용할 경우 조인은 일치하는 행이 시간상으로 얼마나 분리할 수 있는지 정도에 대한 몇 가지 한도를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-310">When you use a join with streaming data, the join must provide some limits on how far the matching rows can be separated in time.</span></span> <span data-ttu-id="c72f6-311">(앞에서 설명한 대로 스트리밍 데이터는 사실상 무한함) 관계에 대한 시간 범위는 조인의 `ON` 절 내부에 `DATEDIFF` 함수를 사용하여 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-311">(As noted earlier, the streaming data is effectively endless.) The time bounds for the relationship are specified inside the `ON` clause of the join, using the `DATEDIFF` function .</span></span> <span data-ttu-id="c72f6-312">이 경우 조인은 호출 데이터의 5초 간격을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-312">In this case, the join is based on a 5-second interval of call data .</span></span>

1. <span data-ttu-id="c72f6-313">코드 편집기에서 쿼리를 다음으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-313">Change the query in the code editor to the following:</span></span> 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    <span data-ttu-id="c72f6-314">이 쿼리는 조인에서 `DATEDIFF` 함수를 제외하고 SQL 조인과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-314">This query is like any SQL join except for the `DATEDIFF` function in the join.</span></span> <span data-ttu-id="c72f6-315">Streaming Analytics에 한정된 `DATEDIFF` 버전이며 `ON...BETWEEN` 절에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-315">This is a version of `DATEDIFF` that's specific to Streaming Analytics, and it must appear in the `ON...BETWEEN` clause.</span></span> <span data-ttu-id="c72f6-316">매개 변수는 시간 단위(이 예제에서는 초)와 조인의 두 원본에 대한 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-316">The parameters are a time unit (seconds in this example) and the aliases of the two sources for the join.</span></span> <span data-ttu-id="c72f6-317">(표준 SQL `DATEDIFF` 함수와는 다름)</span><span class="sxs-lookup"><span data-stu-id="c72f6-317">(This is different from the standard SQL `DATEDIFF` function.)</span></span> 

    <span data-ttu-id="c72f6-318">`WHERE` 절에는 사기성 호출에 플래그를 지정하는 조건이 포함되며 발신 스위치는 동일하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-318">The `WHERE` clause includes the condition that flags the fraudulent call: the originating switches are not the same.</span></span> 

2. <span data-ttu-id="c72f6-319">**테스트**를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-319">Click **Test** again.</span></span> 

    ![셀프 조인에 대한 Stream Analytics 작업 출력, 6개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. <span data-ttu-id="c72f6-321">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-321">Click **Save**.</span></span> <span data-ttu-id="c72f6-322">Streaming Analytics 작업의 일부로 셀프 조인 쿼리를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-322">This saves the self-join query as part of the Streaming Analytics job.</span></span> <span data-ttu-id="c72f6-323">(샘플 데이터를 저장하지 않음)</span><span class="sxs-lookup"><span data-stu-id="c72f6-323">(It doesn't save the sample data.)</span></span>

    ![Stream Analytics 작업 저장](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-to-store-transformed-data"></a><span data-ttu-id="c72f6-325">변환된 데이터를 저장할 출력 싱크 만들기</span><span class="sxs-lookup"><span data-stu-id="c72f6-325">Create an output sink to store transformed data</span></span>

<span data-ttu-id="c72f6-326">이벤트 스트림, 이벤트를 수집할 이벤트 허브 입력 및 스트림 변환을 수행할 쿼리를 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-326">You've defined an event stream, an event hub input to ingest events, and a query to perform a transformation over the stream.</span></span> <span data-ttu-id="c72f6-327">마지막 단계는 작업의 출력 싱크(즉, 변환된 스트림을 기록할 위치)를 정의하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-327">The last step is to define an output sink for the job—that is, a place to write the transformed stream to.</span></span> 

<span data-ttu-id="c72f6-328">SQL Server Database, Table Storage, Data Lake Storage, Power BI 및 다른 이벤트 허브 등 많은 리소스를 출력 싱크로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-328">You can use many resources as output sinks—a SQL Server database, table storage, Data Lake storage, Power BI, and even another event hub.</span></span> <span data-ttu-id="c72f6-329">이 자습서에서는 구조화되지 않은 데이터를 수용하므로 추가 분석을 위한 이벤트 정보를 수집하는 데 일반적으로 사용되는 Azure Blob Storage에 스트림을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-329">For this tutorial, you'll write the stream to Azure Blob Storage, which is a typical choice for collecting event information for later analysis, since it accommodates unstructured data .</span></span>

<span data-ttu-id="c72f6-330">기존 Blob Storage 계정이 있는 경우 기존 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-330">If you have an existing blob storage account, you can use that.</span></span> <span data-ttu-id="c72f6-331">이 자습서에서는 이 자습서에 필요한 새 저장소 계정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-331">For this tutorial, we'll show you how to create a new storage account just for this tutorial.</span></span>

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="c72f6-332">Azure Blob Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="c72f6-332">Create an Azure Blob Storage account</span></span>

1. <span data-ttu-id="c72f6-333">Azure Portal에서 Streaming Analytics 작업 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-333">In the Azure portal, return to the Streaming Analytics job blade.</span></span> <span data-ttu-id="c72f6-334">(블레이드를 닫은 경우 **모든 리소스** 블레이드에서 `sa_frauddetection_job_demo`를 검색)</span><span class="sxs-lookup"><span data-stu-id="c72f6-334">(If you closed the blade, search for `sa_frauddetection_job_demo` in the **All resources** blade.)</span></span>
2. <span data-ttu-id="c72f6-335">**작업 토폴로지** 섹션에서 **출력** 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-335">In the **Job Topology** section, click the **Output** box.</span></span> 
3. <span data-ttu-id="c72f6-336">**출력** 블레이드에서 **+&nbsp;추가**를 클릭한 후 블레이드를 다음 값으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-336">In the **Outputs** blade, click **+&nbsp;Add** and then fill out the blade with these values:</span></span>

    * <span data-ttu-id="c72f6-337">**출력 별칭**: 이름으로 `CallStream-FraudulentCalls`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-337">**Output alias**: Use the name `CallStream-FraudulentCalls`.</span></span> 
    * <span data-ttu-id="c72f6-338">**싱크**: **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-338">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="c72f6-339">**가져오기 옵션**: **현재 구독의 Blob Storage 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-339">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="c72f6-340">**저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="c72f6-340">**Storage account**.</span></span> <span data-ttu-id="c72f6-341">**새 저장소 계정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-341">Select **Create new storage account.**</span></span>
    * <span data-ttu-id="c72f6-342">**저장소 계정**(두 번째 상자).</span><span class="sxs-lookup"><span data-stu-id="c72f6-342">**Storage account** (second box).</span></span> <span data-ttu-id="c72f6-343">`YOURNAMEsademo`를 입력합니다. 여기서 `YOURNAME`은 사용자 이름 또는 다른 고유 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-343">Enter `YOURNAMEsademo`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="c72f6-344">이름으로 소문자 및 숫자만 사용할 수 있으며 Azure 전체에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-344">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="c72f6-345">**컨테이너**.</span><span class="sxs-lookup"><span data-stu-id="c72f6-345">**Container**.</span></span> <span data-ttu-id="c72f6-346">`sa-fraudulentcalls-demo`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-346">Enter `sa-fraudulentcalls-demo`.</span></span>
    <span data-ttu-id="c72f6-347">저장소 계정 이름 및 컨테이너 이름을 다음과 같이 함께 사용하여 Blob Storage에 대한 URI를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-347">The storage account name and container name are used together to provide a URI for the blob storage, like this:</span></span> 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![Stream Analytics 작업에 대한 “새 출력” 블레이드](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. <span data-ttu-id="c72f6-349">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-349">Click **Create**.</span></span> 

    <span data-ttu-id="c72f6-350">Azure에서 저장소 계정을 만들고 키를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-350">Azure creates the storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="c72f6-351">**출력** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-351">Close the **Outputs** blade.</span></span> 

## <a name="start-the-streaming-analytics-job"></a><span data-ttu-id="c72f6-352">Streaming Analytics 작업 시작</span><span class="sxs-lookup"><span data-stu-id="c72f6-352">Start the Streaming Analytics job</span></span>

<span data-ttu-id="c72f6-353">이제 작업이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-353">The job is now configured.</span></span> <span data-ttu-id="c72f6-354">입력(이벤트 허브), 변환(사기성 호출을 찾는 쿼리), 출력(Blob Storage)을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-354">You've specified an input (the event hub), a transformation (the query to look for fraudulent calls), and an output (blob storage).</span></span> <span data-ttu-id="c72f6-355">이제 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-355">You can now start the job.</span></span> 

1. <span data-ttu-id="c72f6-356">TelcoGenerator 앱이 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-356">Make sure the TelcoGenerator app is running.</span></span>

2. <span data-ttu-id="c72f6-357">작업 블레이드에서 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-357">In the job blade, click **Start**.</span></span>

    ![Stream Analytic 작업 시작](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="c72f6-359">**작업 시작** 블레이드에서 작업 출력 시작 시간으로 **지금**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-359">In the **Start job** blade, for Job output start time, select **Now**.</span></span> 

4. <span data-ttu-id="c72f6-360">**시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-360">Click **Start**.</span></span> 

    ![Stream Analytics 작업에 대한 “작업 시작” 블레이드](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="c72f6-362">Azure에서 사용자에게 작업이 시작된 때를 알려주고 작업 블레이드에 상태가 **실행 중**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-362">Azure notifies you when the job has started, and in the job blade, the status is displayed as **Running**.</span></span>

    ![Stream Analytics 작업 상태, “실행 중” 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-the-transformed-data"></a><span data-ttu-id="c72f6-364">변환된 데이터 검사</span><span class="sxs-lookup"><span data-stu-id="c72f6-364">Examine the transformed data</span></span>

<span data-ttu-id="c72f6-365">이제 Streaming Analytics 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-365">You now have a complete Streaming Analytics job.</span></span> <span data-ttu-id="c72f6-366">작업에서 전화 통화 메타데이터 스트림을 검사하여 실시간으로 사기성 전화 통화를 찾고 이러한 사기성 통화에 대한 정보를 저장소에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-366">The job is examining a stream of phone call metadata, looking for fraudulent phone calls in real time, and writing information about those fraudulent calls to storage.</span></span> 

<span data-ttu-id="c72f6-367">이 자습서를 완료하기 위해 Streaming Analytics 작업으로 캡처된 데이터를 살펴보려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-367">To complete this tutorial, you might want to look at the data being captured by the Streaming Analytics job.</span></span> <span data-ttu-id="c72f6-368">데이터는 청크(파일)로 Azure Blob Storage에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-368">The data is being written to Azure Blog Storage in chunks (files).</span></span> <span data-ttu-id="c72f6-369">Azure Blob Storage를 읽는 데 아무 도구나 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-369">You can use any tool that reads Azure Blob Storage.</span></span> <span data-ttu-id="c72f6-370">필수 조건 섹션에서 설명한 대로, Visual Studio에서 Azure 확장을 사용하거나 [Azure Storage 탐색기](http://storageexplorer.com/) 또는 [Azure 탐색기](http://www.cerebrata.com/products/azure-explorer/introduction)와 같은 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-370">As noted in the Prerequisites section, you can use Azure extensions in Visual Studio, or you can use a tool like [Azure Storage Explorer](http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction).</span></span> 

<span data-ttu-id="c72f6-371">Blob Storage에서 파일 내용을 검사할 때 다음과 같은 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-371">When you examine the contents of a file in blob storage, you see something like the following :</span></span>

![Streaming Analytics 출력이 있는 Azure Blob Storage](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a><span data-ttu-id="c72f6-373">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="c72f6-373">Clean up resources</span></span>

<span data-ttu-id="c72f6-374">사기 감지 시나리오를 진행하고 이 자습서에서 만든 리소스를 사용하는 추가 문서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-374">We have additional articles that continue with the fraud-detection scenario and that use the resources that you've created in this tutorial.</span></span> <span data-ttu-id="c72f6-375">계속하려면 뒷부분에 **다음 단계** 아래의 제안 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72f6-375">If you want to continue, see the suggestions under **Next steps** later.</span></span>

<span data-ttu-id="c72f6-376">그러나 작업을 수행했고 만든 리소스가 필요하지 않는 경우 불필요한 Azure 비용이 발생하지 않도록 해당 항목을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-376">However, if you're done and you don't need the resources you've created, you can delete them so that you don't incur unnecessary Azure charges.</span></span> <span data-ttu-id="c72f6-377">이 경우 다음을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-377">In that case, we suggest that you do the following:</span></span>

1. <span data-ttu-id="c72f6-378">Streaming Analytics 작업을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-378">Stop the Streaming Analytics job.</span></span> <span data-ttu-id="c72f6-379">**작업** 블레이드의 맨 위에서 **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-379">In the **Jobs** blade, click **Stop** at the top.</span></span>
2. <span data-ttu-id="c72f6-380">Telco Generator 앱을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-380">Stop the Telco Generator app.</span></span> <span data-ttu-id="c72f6-381">앱을 시작한 명령 창에서 Ctrl + C를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-381">In the command window where you started the app, press Ctrl+C.</span></span>
3. <span data-ttu-id="c72f6-382">이 자습서에 대해 새 Blob Storage 계정을 만든 경우 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-382">If you created a new blob storage account just for this tutorial, delete it.</span></span> 
4. <span data-ttu-id="c72f6-383">Streaming Analytics 작업을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-383">Delete the Streaming Analytics job.</span></span>
5. <span data-ttu-id="c72f6-384">이벤트 허브를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-384">Delete the event hub.</span></span>
6. <span data-ttu-id="c72f6-385">이벤트 허브 네임스페이스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-385">Delete the event hub namespace.</span></span>

## <a name="get-support"></a><span data-ttu-id="c72f6-386">지원 받기</span><span class="sxs-lookup"><span data-stu-id="c72f6-386">Get support</span></span>

<span data-ttu-id="c72f6-387">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72f6-387">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c72f6-388">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c72f6-388">Next steps</span></span>

<span data-ttu-id="c72f6-389">다음 문서를 통해 이 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-389">You can continue this tutorial with the following articles:</span></span>

* <span data-ttu-id="c72f6-390">[Stream Analytics 및 Power BI: 스트리밍 데이터에 대한 실시간 분석 대시보드](stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="c72f6-390">[Stream Analytics and Power BI: A real-time analytics dashboard for streaming data](stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="c72f6-391">이 문서에서는 실시간 시각화 및 분석을 위해 Stream Analytics 작업의 TelCo 출력을 Power BI로 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-391">This article shows you how to send the TelCo output of the Stream Analytics job to Power BI for real-time visualization and analysis.</span></span>
* <span data-ttu-id="c72f6-392">[Azure Functions를 사용하여 Azure Redis Cache에 Azure Stream Analytics의 데이터를 저장하는 방법](stream-analytics-functions-redis.md).</span><span class="sxs-lookup"><span data-stu-id="c72f6-392">[How to store data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions](stream-analytics-functions-redis.md).</span></span> <span data-ttu-id="c72f6-393">이 문서에서는 Azure Functions를 사용하여 Service Bus 큐를 통해 사기성 호출을 Azure Redis Cache에 기록하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72f6-393">This article shows how to use Azure Functions to write fraudulent calls to an Azure Redis cache via a Service Bus queue.</span></span>

<span data-ttu-id="c72f6-394">일반적인 Stream Analytics에 대한 자세한 내용은 다음 문서를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="c72f6-394">For more information about Stream Analytics in general, try these articles:</span></span>

* [<span data-ttu-id="c72f6-395">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="c72f6-395">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c72f6-396">Azure Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="c72f6-396">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c72f6-397">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="c72f6-397">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c72f6-398">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="c72f6-398">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
