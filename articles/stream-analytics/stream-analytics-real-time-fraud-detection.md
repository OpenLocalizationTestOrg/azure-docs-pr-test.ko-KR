# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a><span data-ttu-id="674d1-101">Azure Stream Analytics 사용 시작 : 실시간 부정 행위 감지</span><span class="sxs-lookup"><span data-stu-id="674d1-101">Get started using Azure Stream Analytics: Real-time fraud detection</span></span>

<span data-ttu-id="674d1-102">이 자습서는 방법의 종단 간 그림을 제공 toouse Azure 스트림 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-102">This tutorial provides an end-to-end illustration of how toouse Azure Stream Analytics.</span></span> <span data-ttu-id="674d1-103">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-103">You learn how to:</span></span> 

* <span data-ttu-id="674d1-104">스트리밍 이벤트를 Azure Event Hubs의 인스턴스로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-104">Bring streaming events into an instance of Azure Event Hubs.</span></span> <span data-ttu-id="674d1-105">이 자습서에서는 휴대폰 메타데이터 레코드 스트림을 시뮬레이션하도록 제공하는 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-105">In this tutorial, you'll use an app that we provide that simulates a stream of mobile-phone metadata records.</span></span>

* <span data-ttu-id="674d1-106">정보 집계 또는 패턴을 찾고 있습니다. SQL과 유사한 스트림 분석 쿼리 tootransform 데이터를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-106">Write SQL-like Stream Analytics queries tootransform data, aggregating information or looking for patterns.</span></span> <span data-ttu-id="674d1-107">어떻게 toouse 쿼리 tooexamine 들어오는 스트림을 hello를 찾아서 클릭 사기 될 수 있는 호출에 대 한 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-107">You will see how toouse a query tooexamine hello incoming stream and look for calls that might be fraudulent.</span></span>

* <span data-ttu-id="674d1-108">보낼 hello 결과 tooan 출력 싱크 (저장소)를 추가로 insights를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-108">Send hello results tooan output sink (storage) that you can analyze for additional insights.</span></span> <span data-ttu-id="674d1-109">이 경우 hello 의심 스러운 호출 데이터 tooAzure Blob 저장소를 보내 드립니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-109">In this case, you'll send hello suspicious call data tooAzure Blob storage.</span></span>

<span data-ttu-id="674d1-110">이 자습서에서는 전화 통화 데이터를 기반으로 하는 실시간 사기 감지의 hello 예제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-110">In  this tutorial, we use hello example of real-time fraud detection based on phone-call data.</span></span> <span data-ttu-id="674d1-111">하지만 hello 기술을 설명할 사기 감지 신용 카드 사기 또는 id 도용 같은 다른 형식에도 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-111">But hello technique we illustrate is also suited for other types of fraud detection, such as credit card fraud or identity theft.</span></span> 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a><span data-ttu-id="674d1-112">시나리오: 실시간으로 통신 및 SIM 사기 감지</span><span class="sxs-lookup"><span data-stu-id="674d1-112">Scenario: Telecommunications and SIM fraud detection in real time</span></span>

<span data-ttu-id="674d1-113">통신 회사에는 많은 양의 들어오는 호출 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-113">A telecommunications company has a large volume of data for incoming calls.</span></span> <span data-ttu-id="674d1-114">hello 사는 고객에 게 알림 하거나 특정 수에 대 한 서비스를 종료할 수 있도록 toodetect 사기성 실시간으로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-114">hello company wants toodetect fraudulent calls in real time so that they can notify customers or shut down service for a specific number.</span></span> <span data-ttu-id="674d1-115">한 가지 유형의 SIM 사기 포함 hello에서 여러 번 호출 됩니다. hello 주위 동일한 id 시간이 하지만 서로 다른 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-115">One type of SIM fraud involves multiple calls from hello same identity around hello same time but in geographically different locations.</span></span> <span data-ttu-id="674d1-116">toodetect이이 유형의 사기, 회사 요구 tooexamine 들어오는 전화 레코드 hello 찾은 특정 패턴에 대 한-이 경우에 대 한 호출 주위 hello 각각 다른 국가에서 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-116">toodetect this type of fraud, hello company needs tooexamine incoming phone records and look for specific patterns—in this case, for calls made around hello same time in different countries.</span></span> <span data-ttu-id="674d1-117">이 범주에 해당 하는 모든 전화 레코드 toostorage 이후 분석을 위해 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-117">Any phone records that fall into this category are written toostorage for subsequent analysis.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="674d1-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="674d1-118">Prerequisites</span></span>

<span data-ttu-id="674d1-119">이 자습서에서는 샘플 전화 통화 메타데이터를 생성하는 클라이언트 앱을 사용하여 전화 통화 데이터를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-119">In this tutorial, you'll simulate phone-call data by using a client app that generates sample phone call metadata.</span></span> <span data-ttu-id="674d1-120">일부 앱 hello hello 레코드 모양을 사기성 호출을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-120">Some of hello records that hello app produces look like fraudulent calls.</span></span> 

<span data-ttu-id="674d1-121">시작 하기 전에 hello 다음 항목이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-121">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="674d1-122">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="674d1-122">An Azure account.</span></span>
* <span data-ttu-id="674d1-123">hello 호출 이벤트 생성기는 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="674d1-123">hello call-event generator app.</span></span> <span data-ttu-id="674d1-124">Hello를 다운로드 하 여 가져올 수 있습니다 [TelcoGenerator.zip 파일](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) hello Microsoft 다운로드 센터에서에서.</span><span class="sxs-lookup"><span data-stu-id="674d1-124">You can get this by downloading hello [TelcoGenerator.zip file](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) from hello Microsoft Download Center.</span></span> <span data-ttu-id="674d1-125">컴퓨터의 폴더에 이 패키지의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-125">Unzip this package into a folder on your computer.</span></span> <span data-ttu-id="674d1-126">Toosee hello 소스 코드를 디버거에서 실행된 hello 앱을 원하는 hello 앱 소스 코드에서 얻을 수 있습니다 [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator)합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-126">If you want toosee hello source code and run hello app in a debugger, you can get hello app source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="674d1-127">Windows는 hello를 다운로드 한.zip 파일을 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-127">Windows might block hello downloaded .zip file.</span></span> <span data-ttu-id="674d1-128">풀고 수 없는 경우 hello 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-128">If you can't unzip it, right-click hello file and select **Properties**.</span></span> <span data-ttu-id="674d1-129">Hello 표시 되 면 "파일인 다른 컴퓨터에서이 및 보호할 수 있습니다 수 차단 된 toohelp이이 컴퓨터" 메시지, 선택 hello **차단 해제** 옵션 선택한 다음 클릭 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-129">If you see hello "This file came from another computer and might be blocked toohelp protect this computer" message, select hello **Unblock** option and then click **Apply**.</span></span>

<span data-ttu-id="674d1-130">Hello 스트리밍 분석 작업의 tooexamine hello 결과 찾으려는 경우 또한 Azure Blob 저장소 컨테이너의 hello 내용을 보기 위한 도구를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-130">If you want tooexamine hello results of hello Streaming Analytics job, you also need a tool for viewing hello contents of a Azure Blob Storage container.</span></span> <span data-ttu-id="674d1-131">Visual Studio를 사용하는 경우 [Visual Studio용 Azure 도구](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) 또는 [Visual Studio 클라우드 탐색기](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-131">If you use Visual Studio, you can use [Azure Tools for Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) or [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer).</span></span> <span data-ttu-id="674d1-132">또는 [Azure Storage 탐색기](http://storageexplorer.com/) 또는 [Azure 탐색기](http://www.cerebrata.com/products/azure-explorer/introduction)와 같은 독립 실행형 도구를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-132">Alternatively, you can install standalone tools like [Azure Storage Explorer](http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction).</span></span> 

## <a name="create-an-azure-event-hubs-tooingest-events"></a><span data-ttu-id="674d1-133">Azure 이벤트 허브 tooingest 이벤트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-133">Create an Azure event hubs tooingest events</span></span>

<span data-ttu-id="674d1-134">데이터 스트림, tooanalyze 있습니다 *수집* Azure로 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-134">tooanalyze a data stream, you *ingest* it into Azure.</span></span> <span data-ttu-id="674d1-135">일반적인 방법은 tooingest 데이터는 다음과 같은 toouse [Azure 이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md), 수백만 개의 초당 이벤트를 수집 하 고 다음 처리를 hello 이벤트 정보를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-135">A typical way tooingest data is toouse [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md), which lets you ingest millions of events per second and then process and store hello event information.</span></span> <span data-ttu-id="674d1-136">이 자습서에서는 이벤트 허브 만들고 hello 호출 이벤트 생성기 앱 송신 호출 데이터 toothat 이벤트 허브를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-136">For this tutorial, you create an event hub and then have hello call-event generator app send call data toothat event hub.</span></span> <span data-ttu-id="674d1-137">이벤트 허브에 대 한 자세한 참조 hello [Azure 서비스 버스 설명서](https://docs.microsoft.com/en-us/azure/service-bus/)합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-137">For more about event hubs, see hello [Azure Service Bus documentation](https://docs.microsoft.com/en-us/azure/service-bus/).</span></span>

>[!NOTE]
><span data-ttu-id="674d1-138">이 절차의 보다 자세한 버전용 참조 [는 이벤트 허브 네임 스페이스를 만들고 Azure 포털 hello 사용 하 여 이벤트 허브](../event-hubs/event-hubs-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-138">For a more detailed version of this procedure, see [Create an Event Hubs namespace and an event hub using hello Azure portal](../event-hubs/event-hubs-create.md).</span></span> 

### <a name="create-a-namespace-and-event-hub"></a><span data-ttu-id="674d1-139">네임스페이스 및 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="674d1-139">Create a namespace and event hub</span></span>
<span data-ttu-id="674d1-140">이 절차에서는 이벤트 허브 네임 스페이스를 먼저 만들어야 하 고 이벤트 허브 toothat namepsace를 추가 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-140">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namepsace.</span></span> <span data-ttu-id="674d1-141">이벤트 허브 네임 스페이스는 사용 toologically 그룹 관련 이벤트 버스 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="674d1-141">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="674d1-142">Hello Azure 포털에 로그인 하 고 클릭 **새로** > **사물 인터넷** > **이벤트 허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-142">Log  into hello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="674d1-143">Hello에 **네임 스페이스 만들기** 블레이드에서 같은 네임 스페이스 이름 입력 `<yourname>-eh-ns-demo`합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-143">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-eh-ns-demo`.</span></span> <span data-ttu-id="674d1-144">Hello 네임 스페이스에 대 한 모든 이름을 사용할 수 있습니다 하지만 hello 이름은 URL에 유효 해야 하 고 Azure 전체에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-144">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="674d1-145">구독을 선택하고 리소스 그룹을 만들거나 선택한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-145">Select a subscription and create or choose a resource group , then click **Create**.</span></span> 

    ![이벤트 허브 네임스페이스 만들기](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. <span data-ttu-id="674d1-147">Hello 네임 스페이스 배포 완료 되 면 Azure 리소스 목록에 hello 이벤트 허브 네임 스페이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-147">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="674d1-148">Hello 새 네임 스페이스를 클릭 하 고 hello 네임 스페이스 블레이드에서 클릭  **+ &nbsp;이벤트 허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-148">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="674d1-149">새 이벤트 허브를 만들기 위한 hello 이벤트 허브 추가 단추</span><span class="sxs-lookup"><span data-stu-id="674d1-149">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. <span data-ttu-id="674d1-150">이름 hello 새 이벤트 허브 `sa-eh-frauddetection-demo`합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-150">Name hello new event hub `sa-eh-frauddetection-demo`.</span></span> <span data-ttu-id="674d1-151">다른 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-151">You can use a different name.</span></span> <span data-ttu-id="674d1-152">이렇게 하면 hello 이름을 나중에 필요 하기 때문에, 메모를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-152">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="674d1-153">않아도 tooset 다른 옵션 hello 이벤트 허브에 대 한 현재 됩니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-153">You don't need tooset any other options for hello event hub right now.</span></span>

    ![새 이벤트 허브를 만들기 위한 블레이드](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. <span data-ttu-id="674d1-155">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-155">Click **Create**.</span></span>
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a><span data-ttu-id="674d1-156">액세스 toohello 이벤트 허브를 부여 하 고 연결 문자열을 가져올</span><span class="sxs-lookup"><span data-stu-id="674d1-156">Grant access toohello event hub and get a connection string</span></span>

<span data-ttu-id="674d1-157">프로세스 tooan 이벤트 허브 데이터를 보낼 수 있습니다, 전에 hello 이벤트 허브에 적절 한 액세스를 허용 하는 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-157">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="674d1-158">hello 액세스 정책 권한 부여 정보를 포함 하는 연결 문자열을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-158">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="674d1-159">Hello 이벤트 네임 스페이스 블레이드에서 클릭 **이벤트 허브** 새 이벤트 허브의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-159">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="674d1-160">이벤트 허브 블레이드에서 hello 클릭 **공유 액세스 정책을** 클릭 하 고  **+ &nbsp;추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-160">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="674d1-161">Hello 이벤트 허브 네임 스페이스가 아니라 hello 이벤트 허브를 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-161">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="674d1-162">**클레임**에 대해 `sa-policy-manage-demo`라는 이름의 정책을 추가하고 **관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-162">Add a policy named `sa-policy-manage-demo` and for **Claim**, select **Manage**.</span></span>

    ![새 이벤트 허브 액세스 정책을 만들기 위한 블레이드](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  <span data-ttu-id="674d1-164">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-164">Click **Create**.</span></span>

5.  <span data-ttu-id="674d1-165">정책이 배포 된 hello 후, 공유 액세스 정책의 hello 목록에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-165">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="674d1-166">찾기 hello 상자 **연결 문자열-기본 키** hello 복사 단추 다음 toohello 연결 문자열을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-166">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![Hello 액세스 정책에서 hello 기본 연결 문자열 키를 복사합니다.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  <span data-ttu-id="674d1-168">연결 문자열을 hello를 텍스트 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-168">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="674d1-169">몇 가지 약간의 편집 tooit를 변경한 후이 연결 문자열 hello 다음 섹션에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-169">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="674d1-170">hello 연결 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-170">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    <span data-ttu-id="674d1-171">Hello 연결 문자열을 세미콜론으로 구분 된 여러 키-값 쌍이 들어: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, 및 `EntityPath`합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-171">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

## <a name="configure-and-start-hello-event-generator-application"></a><span data-ttu-id="674d1-172">구성 되 고 hello 이벤트 생성기 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="674d1-172">Configure and start hello event generator application</span></span>

<span data-ttu-id="674d1-173">Hello TelcoGenerator 앱을 시작 하기 전에 수 있도록 구성 방금 만든 호출 레코드 toohello 이벤트 허브를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-173">Before you start hello TelcoGenerator app, you configure it so that it will send call records toohello event hub you just created.</span></span>

### <a name="configure-hello-telcogeneratorapp"></a><span data-ttu-id="674d1-174">Hello TelcoGeneratorapp 구성</span><span class="sxs-lookup"><span data-stu-id="674d1-174">Configure hello TelcoGeneratorapp</span></span>

1.  <span data-ttu-id="674d1-175">Hello 편집기 hello 연결 문자열을 복사한 위치에 hello 기록해 `EntityPath` 값을 복사한 후 제거 hello `EntityPath` 쌍 (tooremove hello 세미콜론 앞에 오는 반드시 함).</span><span class="sxs-lookup"><span data-stu-id="674d1-175">In hello editor where you copied hello connection string, make a note of hello `EntityPath` value, and then remove hello `EntityPath` pair (don't forget tooremove hello semicolon that precedes it).</span></span> 

2.  <span data-ttu-id="674d1-176">Hello TelcoGenerator.zip 파일의 압축을 푼 hello 폴더에서 hello telcodatagen.exe.config 편집기에서에서 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-176">In hello folder where you unzipped hello TelcoGenerator.zip file, open hello telcodatagen.exe.config file in an editor.</span></span> <span data-ttu-id="674d1-177">(둘 이상의.config 파일은, hello 오른쪽으로 한 열 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="674d1-177">(There is more than one .config file, so be sure that you open hello right one.)</span></span>

3.  <span data-ttu-id="674d1-178">Hello에 `<appSettings>` 요소를이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-178">In hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="674d1-179">Hello의 hello 값 설정 `EventHubName` 키 toohello 이벤트 허브 이름 (즉, hello 엔터티 경로 toohello 값).</span><span class="sxs-lookup"><span data-stu-id="674d1-179">Set hello value of hello `EventHubName` key toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="674d1-180">Hello의 hello 값 설정 `Microsoft.ServiceBus.ConnectionString` toohello 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-180">Set hello value of hello `Microsoft.ServiceBus.ConnectionString` key toohello connection string.</span></span> 

    <span data-ttu-id="674d1-181">hello `<appSettings>` 섹션은 다음 예제는 hello 같습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-181">hello `<appSettings>` section will look like hello following example.</span></span> <span data-ttu-id="674d1-182">(명확성을 위해 우리 줄 바꿈된 hello 줄 및 hello 인증 토큰에서 일부 문자를 제거 합니다.)</span><span class="sxs-lookup"><span data-stu-id="674d1-182">(For clarity, we wrapped hello lines and removed some characters from hello authorization token.)</span></span>

    ![Hello 이벤트 허브 이름 및 연결 문자열을 보여 주는 TelcoGenerator 응용 프로그램 구성 파일](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  <span data-ttu-id="674d1-184">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-184">Save hello file.</span></span> 

### <a name="start-hello-app"></a><span data-ttu-id="674d1-185">Hello 응용 프로그램을 시작</span><span class="sxs-lookup"><span data-stu-id="674d1-185">Start hello app</span></span>
1.  <span data-ttu-id="674d1-186">명령 창을 열고 hello TelcoGenerator 앱 압축 되지 않습니다 toohello 폴더를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-186">Open a command window and change toohello folder where hello TelcoGenerator app is unzipped.</span></span>
2.  <span data-ttu-id="674d1-187">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-187">Enter hello following command:</span></span>

        telcodatagen.exe 1000 .2 2

    <span data-ttu-id="674d1-188">hello 매개 변수는.</span><span class="sxs-lookup"><span data-stu-id="674d1-188">hello parameters are:</span></span> 

    * <span data-ttu-id="674d1-189">시간당 CDR 수.</span><span class="sxs-lookup"><span data-stu-id="674d1-189">Number of CDRs per hour.</span></span> 
    * <span data-ttu-id="674d1-190">SIM 카드 사기 확률: 모든 호출의 백분율로 서 얼마나 자주 hello 이러한 앱을 시뮬레이션 해야 사기성 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-190">SIM Card Fraud Probability: How often, as a percentage of all calls, that hello app should simulate a fraudulent call.</span></span> <span data-ttu-id="674d1-191">hello 값.2가 기록 하는 hello 호출의 약 20% 사기성 한지를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-191">hello value .2 means that about 20% of hello call records will look fraudulent.</span></span>
    * <span data-ttu-id="674d1-192">기간(시간).</span><span class="sxs-lookup"><span data-stu-id="674d1-192">Duration in hours.</span></span> <span data-ttu-id="674d1-193">hello 수 시간 hello 응용 프로그램을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-193">hello number of hours that hello app should run.</span></span> <span data-ttu-id="674d1-194">작업을 hello 명령줄에서 Ctrl + C를 눌러 언제 든 지 hello 앱으로 중지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-194">You can also stop hello app any time by pressing Ctrl+C at hello command line.</span></span>

    <span data-ttu-id="674d1-195">몇 초 후 hello 앱 toohello 이벤트 허브에 전송할 때 hello 화면에 전화 통화 레코드를 표시를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-195">After a few seconds, hello app starts displaying phone call records on hello screen as it sends them toohello event hub.</span></span>

<span data-ttu-id="674d1-196">이 실시간 사기 감지 응용 프로그램에서 사용 하 여 hello 키 필드는 hello 다음 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-196">Some of hello key fields that you will be using in this real-time fraud detection application are hello following:</span></span>

|<span data-ttu-id="674d1-197">**레코드**</span><span class="sxs-lookup"><span data-stu-id="674d1-197">**Record**</span></span>|<span data-ttu-id="674d1-198">**정의**</span><span class="sxs-lookup"><span data-stu-id="674d1-198">**Definition**</span></span>|
|----------|--------------|
|`CallrecTime`|<span data-ttu-id="674d1-199">hello timestamp 안녕 호출에 대 한 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-199">hello timestamp for hello call start time.</span></span> |
|`SwitchNum`|<span data-ttu-id="674d1-200">hello 전화 스위치 tooconnect hello 호출을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-200">hello telephone switch used tooconnect hello call.</span></span> <span data-ttu-id="674d1-201">예를 들어 hello 스위치는 hello 국가별 (미국, 중국, 영국, 독일에 또는 오스트레일리아의 경우)을 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-201">For this example, hello switches are strings that represent hello country of origin (US, China, UK, Germany, or Australia).</span></span> |
|`CallingNum`|<span data-ttu-id="674d1-202">hello 호출자의 hello 전화 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-202">hello phone number of hello caller.</span></span> |
|`CallingIMSI`|<span data-ttu-id="674d1-203">국제 모바일 IMSI (Subscriber Identity) 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-203">hello International Mobile Subscriber Identity (IMSI).</span></span> <span data-ttu-id="674d1-204">Hello hello 호출자의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-204">This is hello Unique identifier of hello caller.</span></span> |
|`CalledNum`|<span data-ttu-id="674d1-205">hello 호출 수신자의 hello 전화 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-205">hello phone number of hello call recipient.</span></span> |
|`CalledIMSI`|<span data-ttu-id="674d1-206">국제 모바일 구독자 ID(IMSI)</span><span class="sxs-lookup"><span data-stu-id="674d1-206">International Mobile Subscriber Identity (IMSI).</span></span> <span data-ttu-id="674d1-207">Hello hello 호출 수신자의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-207">This is hello unique identifier of hello call recipient.</span></span> |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a><span data-ttu-id="674d1-208">스트리밍 데이터 스트림 분석 작업 toomanage 만들기</span><span class="sxs-lookup"><span data-stu-id="674d1-208">Create a Stream Analytics job toomanage streaming data</span></span>

<span data-ttu-id="674d1-209">이제 호출 이벤트 스트림이 있고 Stream Analytics 작업을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-209">Now that you have a stream of call events, you can set up a Stream Analytics job.</span></span> <span data-ttu-id="674d1-210">hello 작업은 설정 하는 hello 이벤트 허브에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-210">hello job will read data from hello event hub that you set up.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="674d1-211">Hello 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="674d1-211">Create hello job</span></span> 

1. <span data-ttu-id="674d1-212">Hello Azure 포털에서에서 클릭 **새로** > **사물 인터넷** > **스트림 분석 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-212">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="674d1-213">이름 hello 작업 `sa_frauddetection_job_demo`, 구독, 리소스 그룹 및 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-213">Name hello job `sa_frauddetection_job_demo`, specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="674d1-214">것이 좋습니다 tooplace hello 작업과 hello 이벤트 허브를 hello에 동일한 지역에 대 한 최상의 성능 지역 간 데이터 tootransfer을 지불 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-214">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![새 Stream Analytics 작업 만들기](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. <span data-ttu-id="674d1-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-216">Click **Create**.</span></span>

    <span data-ttu-id="674d1-217">hello 작업은 생성 하 고 hello 포털 작업 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-217">hello job is created and hello portal displays job details.</span></span> <span data-ttu-id="674d1-218">아무 것도 실행 되 고 아직 하지만-시작 하기 전에 tooconfigure hello 작업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-218">Nothing is running yet, though—you have tooconfigure hello job before it can be started.</span></span>

### <a name="configure-job-input"></a><span data-ttu-id="674d1-219">작업 입력 구성</span><span class="sxs-lookup"><span data-stu-id="674d1-219">Configure job input</span></span>

1. <span data-ttu-id="674d1-220">Hello 대시보드 또는 hello **모든 리소스** 블레이드, 찾기 및 선택 hello `sa_frauddetection_job_demo` 스트림 분석 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-220">In hello dashboard or hello **All resources** blade, find and select hello `sa_frauddetection_job_demo` Stream Analytics job.</span></span> 
2. <span data-ttu-id="674d1-221">Hello에 **작업 토폴로지** hello 스트림 분석 작업 블레이드의 섹션에 있는 클릭 hello **입력** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-221">In hello **Job Topology** section of hello Stream Analytics job blade, click hello **Input** box.</span></span>

    ![Hello 스트리밍 분석 작업 블레이드에서 토폴로지에서 입력된 상자](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. <span data-ttu-id="674d1-223">클릭  **+ &nbsp;추가** hello 블 레이 이러한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-223">Click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="674d1-224">**입력된 별칭**: hello 이름 사용 `CallStream`합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-224">**Input alias**: Use hello name `CallStream`.</span></span> <span data-ttu-id="674d1-225">다른 이름을 사용하는 경우 나중에 필요하므로 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-225">If you use a different name, make a note of it because you'll need it later.</span></span>
    * <span data-ttu-id="674d1-226">**원본 형식**: **데이터 스트림**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-226">**Source type**: Select **Data stream**.</span></span> <span data-ttu-id="674d1-227">(**참조 데이터** 이 자습서에서 사용 하지 않으며 toostatic 조회 데이터를 참조 합니다.)</span><span class="sxs-lookup"><span data-stu-id="674d1-227">(**Reference data** refers toostatic lookup data, which you won't use in this tutorial.)</span></span>
    * <span data-ttu-id="674d1-228">**원본**: **이벤트 허브**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-228">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="674d1-229">**가져오기 옵션**: **현재 구독의 이벤트 허브 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-229">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="674d1-230">**서비스 버스 네임 스페이스**: 이전에 만든 hello 이벤트 허브 네임 스페이스를 선택 (`<yourname>-eh-ns-demo`).</span><span class="sxs-lookup"><span data-stu-id="674d1-230">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-eh-ns-demo`).</span></span>
    * <span data-ttu-id="674d1-231">**이벤트 허브**: 이전에 만든 선택 hello 이벤트 허브 (`sa-eh-frauddetection-demo`).</span><span class="sxs-lookup"><span data-stu-id="674d1-231">**Event hub**: Select hello event hub that you created earlier (`sa-eh-frauddetection-demo`).</span></span>
    * <span data-ttu-id="674d1-232">**이벤트 허브 정책 이름**: 이전에 만든 hello 액세스 정책 (`sa-policy-manage-demo`).</span><span class="sxs-lookup"><span data-stu-id="674d1-232">**Event hub policy name**: Select hello access policy that you created earlier (`sa-policy-manage-demo`).</span></span>

    ![Streaming Analytics 작업에 대한 새 입력 만들기](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="674d1-234">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-234">Click **Create**.</span></span>

## <a name="create-queries-tootransform-real-time-data"></a><span data-ttu-id="674d1-235">실시간 데이터 tootransform 쿼리 만들기</span><span class="sxs-lookup"><span data-stu-id="674d1-235">Create queries tootransform real-time data</span></span>

<span data-ttu-id="674d1-236">이 시점에서 스트림 분석 작업 tooread 들어오는 데이터 스트림을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-236">At this point, you have a Stream Analytics job set up tooread an incoming data stream.</span></span> <span data-ttu-id="674d1-237">hello 다음 단계는 toocreate hello 데이터를 실시간으로 분석 하는 변환입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-237">hello next step is toocreate a transformation that analyzes hello data in real time.</span></span> <span data-ttu-id="674d1-238">쿼리를 만들어 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-238">You do this by creating a query.</span></span> <span data-ttu-id="674d1-239">Stream Analytics는 실시간 처리에 대해 변환을 설명하는 간단하고 선언적인 쿼리 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-239">Stream Analytics supports a simple, declarative query model that describes transformations for real-time processing.</span></span> <span data-ttu-id="674d1-240">hello 쿼리 일부 확장 특정 toostream 분석 있는 SQL 유사 언어를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-240">hello queries use a SQL-like language that has some extensions specific toostream analytics.</span></span> 

<span data-ttu-id="674d1-241">매우 간단한 쿼리는 hello 들어오는 모든 데이터를 읽어 단순히 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-241">A very simple query might simply read all hello incoming data.</span></span> <span data-ttu-id="674d1-242">그러나 자주 표시 된 특정 데이터에 대 한 또는 hello 데이터의 관계에 대 한 쿼리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-242">However, you often create queries that look for specific data or for relationships in hello data.</span></span> <span data-ttu-id="674d1-243">Hello 자습서의이 섹션에서는 만들고 테스트 하면 몇 가지 쿼리 toolearn 몇 가지 방법으로 분석을 위한 입력된 스트림을 변형할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-243">In this section of hello tutorial, you will create and test several queries toolearn a few ways in which you can transform an input stream for analysis.</span></span> 

<span data-ttu-id="674d1-244">여기서 만드는 hello 쿼리 hello 변환 된 데이터 toohello 화면을 표시만 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-244">hello queries you create here will just display hello transformed data toohello screen.</span></span> <span data-ttu-id="674d1-245">이후 섹션에는 출력 싱크 및 hello 변환 된 데이터 toothat 싱크를 작성 하는 쿼리를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-245">In a later section, you'll configure an output sink and a query that writes hello transformed data toothat sink.</span></span>

<span data-ttu-id="674d1-246">hello 언어에 대해 자세히 toolearn 참조 hello [Azure 스트림 분석 쿼리 언어 참조](https://msdn.microsoft.com/library/dn834998.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-246">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/dn834998.aspx).</span></span>

### <a name="get-sample-data-for-testing-queries"></a><span data-ttu-id="674d1-247">쿼리를 테스트하기 위한 샘플 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="674d1-247">Get sample data for testing queries</span></span>

<span data-ttu-id="674d1-248">hello TelcoGenerator 앱에서 보내는 호출 레코드 toohello 이벤트 허브 및 스트림 분석 작업은 hello 이벤트 허브에서 구성 된 tooread 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-248">hello TelcoGenerator app is sending call records toohello event hub, and your Stream Analytics job is configured tooread from hello event hub.</span></span> <span data-ttu-id="674d1-249">쿼리 tootest hello 작업 toomake 올바르게 읽거나 있는지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-249">You can use a query tootest hello job toomake sure that it's reading correctly.</span></span> <span data-ttu-id="674d1-250">너무 hello Azure 콘솔에에서는 쿼리를 테스트 하 고 예제 데이터를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-250">too test a query in hello Azure console, you need sample data.</span></span> <span data-ttu-id="674d1-251">이 연습에서는 hello 이벤트 허브에 들어오는 hello 스트림에서 샘플 데이터를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-251">For this walkthrough, you'll extract sample data from hello stream that's coming into hello event hub.</span></span>

1. <span data-ttu-id="674d1-252">Hello TelcoGenerator 이러한 앱을 실행 하 고 기록 하는 호출을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-252">Make sure that hello TelcoGenerator app is running and producing call records.</span></span>
2. <span data-ttu-id="674d1-253">Hello 포털에서 toohello 스트리밍 분석 작업 블레이드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-253">In hello portal, return toohello Streaming Analytics job blade.</span></span> <span data-ttu-id="674d1-254">(Hello 블레이드를 닫은 경우 검색할 `sa_frauddetection_job_demo` hello에 **모든 리소스** 블레이드.)</span><span class="sxs-lookup"><span data-stu-id="674d1-254">(If you closed hello blade, search for `sa_frauddetection_job_demo` in hello **All resources** blade.)</span></span>
3. <span data-ttu-id="674d1-255">Hello 클릭 **쿼리** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-255">Click hello **Query** box.</span></span> <span data-ttu-id="674d1-256">Azure hello 입력 목록과 hello 작업에 대해 구성 되 고 수 있는 쿼리를 만들 수 있습니다는 출력을 toohello 출력 전송 될 때 hello 입력된 스트림 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-256">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>
4. <span data-ttu-id="674d1-257">Hello에 **쿼리** 블레이드에서 hello 점 다음 toohello 클릭 `CallStream` 입력 한 다음 선택 **데이터 입력에서 샘플**합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-257">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

    ![메뉴 옵션 toouse 샘플 hello 스트리밍 분석 작업 항목에 대 한 데이터와 데이터 "샘플 입력에서" 선택](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="674d1-259">Tooread hello 입력 스트림을 기간 측면에서 정의 된 샘플 데이터 tooget 양을 지정할 수 있는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-259">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

5. <span data-ttu-id="674d1-260">설정 **분** too3 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-260">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    !["3 분" 선택 된 입력된 스트림의 hello 샘플링에 대 한 옵션입니다.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="674d1-262">Azure는 3 분 분량의 hello 입력 스트림에서 데이터를 샘플링 하 고 hello 샘플 데이터를 준비 되 면 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-262">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="674d1-263">(짧은 시간이 소요됩니다.)</span><span class="sxs-lookup"><span data-stu-id="674d1-263">(This takes a short while.)</span></span> 

<span data-ttu-id="674d1-264">hello 예제 데이터는 임시로 저장 되었다가 hello 쿼리 창이 열려 있는 동안를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-264">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="674d1-265">Hello 쿼리 창을 닫으면 hello 샘플 데이터가 무시 되 고 해야 합니다. toocreate 새 샘플 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-265">If you close hello query window, hello sample data is discarded, and you'll have toocreate a new set of sample data.</span></span> 

<span data-ttu-id="674d1-266">대신에 샘플 데이터.json 파일을 가져올 수 있습니다 [GitHub에서](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json), 한 다음 해당.json 파일 toouse hello에 대 한 예제 데이터로 업로드 `CallStream` 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-266">As an alternative, you can get a .json file that has sample data in it [from GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json), and then upload that .json file toouse as sample data for hello `CallStream` input .</span></span> 

### <a name="test-using-a-pass-through-query"></a><span data-ttu-id="674d1-267">통과 쿼리를 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="674d1-267">Test using a pass-through query</span></span>

<span data-ttu-id="674d1-268">모든 이벤트 tooarchive 하려는 경우 모든 hello 필드 hello 이벤트의 페이로드를 hello에 통과 쿼리 tooread를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-268">If you want tooarchive every event, you can use a pass-through query tooread all hello fields in hello payload of hello event.</span></span>

1. <span data-ttu-id="674d1-269">Hello 쿼리 창에서이 쿼리를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-269">In hello query window, enter this query:</span></span>

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    ><span data-ttu-id="674d1-270">SQL처럼 키워드는 대/소문자를 구분하지 않고 공백은 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-270">As with SQL, keywords are not case sensitive, and whitespace is not significant.</span></span>

    <span data-ttu-id="674d1-271">이 쿼리에서 `CallStream` 는 hello 별칭 hello 입력을 만들 때 지정한 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-271">In this query, `CallStream` is hello alias that you specified when you created hello input.</span></span> <span data-ttu-id="674d1-272">다른 별칭을 사용하는 경우 대신 해당 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-272">If you used a different alias, use that name instead.</span></span>

2. <span data-ttu-id="674d1-273">**테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-273">Click **Test**.</span></span>

    <span data-ttu-id="674d1-274">hello 스트림 분석 작업 hello 샘플 데이터에 대해 hello 쿼리를 실행 하 고 hello hello 창 맨 아래에 hello 출력을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-274">hello Stream Analytics job runs hello query against hello sample data and displays hello output at hello bottom of hello window.</span></span> <span data-ttu-id="674d1-275">이 알 수 hello 이벤트 허브 및 hello 스트리밍 분석 작업을 올바르게 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-275">This tells you that hello event hub and hello Streaming Analytics job are configured correctly.</span></span> <span data-ttu-id="674d1-276">(앞에서 설명한 것 처럼 나중에 만들게 출력 싱크가 해당 hello 쿼리 데이터를 쓸 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="674d1-276">(As noted, later you'll create an output sink that hello query can write data to.)</span></span>

    ![Stream Analytics 작업 출력, 73개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    <span data-ttu-id="674d1-278">표시 되는 레코드의 수를 정확 하 게 hello 레코드 수를 3 분 샘플에서 캡처된에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-278">hello exact number of records you see will depend on how many records were captured in your 3-minute sample.</span></span>
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a><span data-ttu-id="674d1-279">열 투영을 사용 하 여 필드의 hello 수 줄이기</span><span class="sxs-lookup"><span data-stu-id="674d1-279">Reduce hello number of fields using a column projection</span></span>

<span data-ttu-id="674d1-280">대부분의 경우에서 분석 hello 입력 스트림에서 모든 hello 열이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-280">In many cases, your analysis doesn't need all hello columns from hello input stream.</span></span> <span data-ttu-id="674d1-281">보다 적은 집합의 필드 보다 hello 통과 쿼리에서 반환 된 쿼리 tooproject를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-281">You can use a query tooproject a smaller set of returned fields than in hello pass-through query.</span></span>

1. <span data-ttu-id="674d1-282">Hello 코드 편집기 toohello 다음과에서 hello 쿼리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-282">Change hello query in hello code editor toohello following:</span></span>

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. <span data-ttu-id="674d1-283">**테스트**를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-283">Click **Test** again.</span></span> 

    ![프로젝션에 대한 Stream Analytics 작업 출력, 25개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a><span data-ttu-id="674d1-285">지역별로 들어오는 호출 수: 집계를 포함하는 연속 창</span><span class="sxs-lookup"><span data-stu-id="674d1-285">Count incoming calls by region: Tumbling window with aggregation</span></span>

<span data-ttu-id="674d1-286">Toocount hello 개수의 들어오는 호출 / 지역당 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-286">Suppose you want toocount hello number of incoming calls per region.</span></span> <span data-ttu-id="674d1-287">데이터 스트리밍에서 tooperform, 횟수와 같은 집계 함수를 원하는 때 toosegment hello 스트림이 필요 임시 단위로 (효과적으로 무한 hello 데이터 스트림 자체 이므로).</span><span class="sxs-lookup"><span data-stu-id="674d1-287">In streaming data, when you want tooperform aggregate functions like counting, you need toosegment hello stream into temporal units (since hello data stream itself is effectively endless).</span></span> <span data-ttu-id="674d1-288">Streaming Analytics [window 함수](stream-analytics-window-functions.md)를 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-288">You do this using a Streaming Analytics [window function](stream-analytics-window-functions.md).</span></span> <span data-ttu-id="674d1-289">그런 다음 해당 창 내부의 hello 데이터와 하나의 단위로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-289">You can then work with hello data inside that window as a unit.</span></span>

<span data-ttu-id="674d1-290">이 변환의 경우 겹치지 않는 temporal 창 시퀀스를 원하며 각 창에는 그룹화 및 집계할 수 있는 불연속 데이터 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-290">For this transformation, you want a sequence of temporal windows that don't overlap—each window will have a discrete set of data that you can group and aggregate.</span></span> <span data-ttu-id="674d1-291">이 창 유형은 참조 tooas는 *연속 창* 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-291">This type of window is referred tooas a *Tumbling window* .</span></span> <span data-ttu-id="674d1-292">Hello 텀블 링 창 내에서 그룹화 된 걸려오는 전화를 hello의 개수를 가져올 수 있습니다 `SwitchNum`, hello 국가 hello 호출 발생을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-292">Within hello Tumbling window, you can get a count of hello incoming calls grouped by `SwitchNum`, which represents hello country where hello call originated.</span></span> 

1. <span data-ttu-id="674d1-293">Hello 코드 편집기 toohello 다음과에서 hello 쿼리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-293">Change hello query in hello code editor toohello following:</span></span>

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    <span data-ttu-id="674d1-294">이 쿼리에서 hello를 사용 하 여 `Timestamp By` hello 키워드 `FROM` 절 toospecify hello에는 타임 스탬프 필드 입력 스트림 toouse toodefine hello 연속 창.</span><span class="sxs-lookup"><span data-stu-id="674d1-294">This query uses hello `Timestamp By` keyword in hello `FROM` clause toospecify which timestamp field in hello input stream toouse toodefine hello Tumbling window.</span></span> <span data-ttu-id="674d1-295">이 경우 hello 창 나눕니다 hello 데이터 세그먼트로 hello `CallRecTime` 각 레코드의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-295">In this case, hello window divides hello data into segments by hello `CallRecTime` field in each record.</span></span> <span data-ttu-id="674d1-296">(필드가 없으면 지정 된 경우 hello 기간 이동 연산은 사용 하 여 hello 이벤트 허브에 각 이벤트 도착 하는 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-296">(If no field is specified, hello windowing operation uses hello time that each event arrives at hello event hub.</span></span> <span data-ttu-id="674d1-297">[Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)에서 “도착 시간과 응용 프로그램 시간”을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="674d1-297">See "Arrival Time Vs Application Time" in [Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span> 

    <span data-ttu-id="674d1-298">hello 프로젝션에 `System.Timestamp`, 각 창의 hello 끝에 대 한 타임 스탬프를 반환 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-298">hello projection includes `System.Timestamp`, which returns a timestamp for hello end of each window.</span></span> 

    <span data-ttu-id="674d1-299">hello를 사용 하면 원하는 toouse 연속 창 toospecify, [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) 함수 hello에 `GROUP BY `절.</span><span class="sxs-lookup"><span data-stu-id="674d1-299">toospecify that you want toouse a Tumbling window, you use hello [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) function in hello `GROUP BY `clause.</span></span> <span data-ttu-id="674d1-300">Hello 함수 (마이크로초 tooa 날)에서 든 시간 단위 및 창 크기 (단위)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-300">In hello function, you specify a time unit (anywhere from a microsecond tooa day) and a window size (how many units).</span></span> <span data-ttu-id="674d1-301">이 예제에서는 hello 연속 창 개의 5 초 간격으로 이루어지며 5 초 마다 동안의 호출에 대 한 국가별 개수를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-301">In this example, hello Tumbling window consists of 5-second intervals, so you will get a count by country for every 5 seconds' worth of calls.</span></span>

2. <span data-ttu-id="674d1-302">**테스트**를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-302">Click **Test** again.</span></span> <span data-ttu-id="674d1-303">Hello 결과 얻으려면 해당 hello 타임 스탬프에서 알 수 있듯이 **WindowEnd** 5 초 단위로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-303">In hello results, notice that hello timestamps under **WindowEnd** are in 5-second increments.</span></span>

    ![집계에 대한 Stream Analytics 작업 출력, 13개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a><span data-ttu-id="674d1-305">셀프 조인을 사용하여 SIM 사기 감지</span><span class="sxs-lookup"><span data-stu-id="674d1-305">Detect SIM fraud using a self-join</span></span>

<span data-ttu-id="674d1-306">이 예를 고려할 수도 있지만 사기성 사용 toobe 호출에서에서 생성 되는 hello 동일 사용자 서로 5 초 안에 서로 다른 위치에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-306">For this example, we can consider fraudulent usage toobe calls that originate from hello same user but in different locations within 5 seconds of one another.</span></span> <span data-ttu-id="674d1-307">예를 들어 hello 동일한 사용자 없습니다 합법적인 방식으로에서 전화를 걸거나 hello 미국 및 오스트레일리아 hello에서 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-307">For example, hello same user can't legitimately make a call from hello US and Australia at hello same time.</span></span> 

<span data-ttu-id="674d1-308">이러한 경우에 대 한 toocheck, 스트리밍 데이터 toojoin hello 스트림 tooitself hello에 따라 hello의 자체 조인을 사용할 수 있습니다 `CallRecTime` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-308">toocheck for these cases, you can use a self-join of hello streaming data toojoin hello stream tooitself based on hello `CallRecTime` value.</span></span> <span data-ttu-id="674d1-309">여기서 hello 호출 기록에 대 한 다음 확인할 수 있습니다 `CallingIMSI` 동일 값 (원래 수 hello) hello은 있지만 hello `SwitchNum` 값 (원점 국가)은 동일한 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-309">You can then look for call records where hello `CallingIMSI` value (hello originating number) is hello same, but hello `SwitchNum` value (country of origin) is not hello same.</span></span>

<span data-ttu-id="674d1-310">조인을 사용 하 여 스트리밍 데이터 행을 일치 시켜 얼마나 hello에 대 한 몇 가지 제한 시간으로 구분 되어 있을 수 hello 조인 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-310">When you use a join with streaming data, hello join must provide some limits on how far hello matching rows can be separated in time.</span></span> <span data-ttu-id="674d1-311">(앞에서 설명한 대로 hello 스트리밍 데이터를 효과적으로 무한.) hello 내 hello 관계에 대 한 hello 시간 범위에서 지정 된 `ON` hello를 사용 하 여 hello 조인의 절 `DATEDIFF` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-311">(As noted earlier, hello streaming data is effectively endless.) hello time bounds for hello relationship are specified inside hello `ON` clause of hello join, using hello `DATEDIFF` function .</span></span> <span data-ttu-id="674d1-312">이 경우 hello 조인의 호출 데이터는 5 초 간격 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-312">In this case, hello join is based on a 5-second interval of call data .</span></span>

1. <span data-ttu-id="674d1-313">Hello 코드 편집기 toohello 다음과에서 hello 쿼리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-313">Change hello query in hello code editor toohello following:</span></span> 

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

    <span data-ttu-id="674d1-314">이 쿼리는 hello 제외한 모든 SQL 조인 같습니다 `DATEDIFF` hello 조인에는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-314">This query is like any SQL join except for hello `DATEDIFF` function in hello join.</span></span> <span data-ttu-id="674d1-315">버전이이 `DATEDIFF` 특정 tooStreaming 분석, 이며 hello에 표시 되어야 `ON...BETWEEN` 절.</span><span class="sxs-lookup"><span data-stu-id="674d1-315">This is a version of `DATEDIFF` that's specific tooStreaming Analytics, and it must appear in hello `ON...BETWEEN` clause.</span></span> <span data-ttu-id="674d1-316">hello 매개 변수는 시간 단위 (이 예제에서는 초)와 hello 조인에 대 한 hello 두 소스의 hello 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-316">hello parameters are a time unit (seconds in this example) and hello aliases of hello two sources for hello join.</span></span> <span data-ttu-id="674d1-317">(이 다른 표준 SQL hello `DATEDIFF` 함수입니다.)</span><span class="sxs-lookup"><span data-stu-id="674d1-317">(This is different from hello standard SQL `DATEDIFF` function.)</span></span> 

    <span data-ttu-id="674d1-318">hello `WHERE` hello 사기성 호출 플래그를 지정 하는 hello 조건 절에 포함 되어: hello 원래 스위치는 동일한 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-318">hello `WHERE` clause includes hello condition that flags hello fraudulent call: hello originating switches are not hello same.</span></span> 

2. <span data-ttu-id="674d1-319">**테스트**를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-319">Click **Test** again.</span></span> 

    ![셀프 조인에 대한 Stream Analytics 작업 출력, 6개 레코드가 생성된 것으로 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. <span data-ttu-id="674d1-321">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-321">Click **Save**.</span></span> <span data-ttu-id="674d1-322">이 hello 스트리밍 분석 작업의 일부로 hello 자체 조인 쿼리를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-322">This saves hello self-join query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="674d1-323">(Hello 예제 데이터 저장 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="674d1-323">(It doesn't save hello sample data.)</span></span>

    ![Stream Analytics 작업 저장](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a><span data-ttu-id="674d1-325">출력 싱크 변환 toostore 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="674d1-325">Create an output sink toostore transformed data</span></span>

<span data-ttu-id="674d1-326">Hello 스트림을 통해 이벤트 스트림, 이벤트 허브 입력된 tooingest 이벤트 및 쿼리 tooperform 변환 정의 했습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-326">You've defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="674d1-327">hello 마지막 단계는 hello 작업에 대 한 출력 싱크가 toodefine-즉, 전체 toowrite hello 변환 스트림입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-327">hello last step is toodefine an output sink for hello job—that is, a place toowrite hello transformed stream to.</span></span> 

<span data-ttu-id="674d1-328">SQL Server Database, Table Storage, Data Lake Storage, Power BI 및 다른 이벤트 허브 등 많은 리소스를 출력 싱크로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-328">You can use many resources as output sinks—a SQL Server database, table storage, Data Lake storage, Power BI, and even another event hub.</span></span> <span data-ttu-id="674d1-329">이 자습서에서는 hello 스트림 tooAzure는 구조화 되지 않은 데이터를 수용 하는 것 때문에 나중에 분석할 수에 대 한 이벤트 정보를 수집 하기 위한 일반적인 선택 하는 Blob 저장소를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-329">For this tutorial, you'll write hello stream tooAzure Blob Storage, which is a typical choice for collecting event information for later analysis, since it accommodates unstructured data .</span></span>

<span data-ttu-id="674d1-330">기존 Blob Storage 계정이 있는 경우 기존 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-330">If you have an existing blob storage account, you can use that.</span></span> <span data-ttu-id="674d1-331">이 자습서에서는 보여줍니다 어떻게 toocreate 새 저장소는이 자습서에 대 한을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-331">For this tutorial, we'll show you how toocreate a new storage account just for this tutorial.</span></span>

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="674d1-332">Azure Blob Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="674d1-332">Create an Azure Blob Storage account</span></span>

1. <span data-ttu-id="674d1-333">Azure 포털 hello toohello 스트리밍 분석 작업 블레이드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-333">In hello Azure portal, return toohello Streaming Analytics job blade.</span></span> <span data-ttu-id="674d1-334">(Hello 블레이드를 닫은 경우 검색할 `sa_frauddetection_job_demo` hello에 **모든 리소스** 블레이드.)</span><span class="sxs-lookup"><span data-stu-id="674d1-334">(If you closed hello blade, search for `sa_frauddetection_job_demo` in hello **All resources** blade.)</span></span>
2. <span data-ttu-id="674d1-335">Hello에 **작업 토폴로지** 섹션에서 hello **출력** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-335">In hello **Job Topology** section, click hello **Output** box.</span></span> 
3. <span data-ttu-id="674d1-336">Hello에 **출력** 블레이드에서 클릭  **+ &nbsp;추가** hello 블 레이 이러한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-336">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="674d1-337">**출력 별칭**: hello 이름 사용 `CallStream-FraudulentCalls`합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-337">**Output alias**: Use hello name `CallStream-FraudulentCalls`.</span></span> 
    * <span data-ttu-id="674d1-338">**싱크**: **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-338">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="674d1-339">**가져오기 옵션**: **현재 구독의 Blob Storage 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-339">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="674d1-340">**저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="674d1-340">**Storage account**.</span></span> <span data-ttu-id="674d1-341">**새 저장소 계정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-341">Select **Create new storage account.**</span></span>
    * <span data-ttu-id="674d1-342">**저장소 계정**(두 번째 상자).</span><span class="sxs-lookup"><span data-stu-id="674d1-342">**Storage account** (second box).</span></span> <span data-ttu-id="674d1-343">`YOURNAMEsademo`를 입력합니다. 여기서 `YOURNAME`은 사용자 이름 또는 다른 고유 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-343">Enter `YOURNAMEsademo`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="674d1-344">hello 이름은 소문자 및 숫자를 사용할 수 및 Azure 전체에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-344">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="674d1-345">**컨테이너**.</span><span class="sxs-lookup"><span data-stu-id="674d1-345">**Container**.</span></span> <span data-ttu-id="674d1-346">`sa-fraudulentcalls-demo`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-346">Enter `sa-fraudulentcalls-demo`.</span></span>
    <span data-ttu-id="674d1-347">hello 저장소 계정 이름과 컨테이너 이름에 사용 되는 함께 tooprovide 다음과 같이 hello blob 저장소에 대 한 URI는</span><span class="sxs-lookup"><span data-stu-id="674d1-347">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![Stream Analytics 작업에 대한 “새 출력” 블레이드](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. <span data-ttu-id="674d1-349">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-349">Click **Create**.</span></span> 

    <span data-ttu-id="674d1-350">Azure는 hello 저장소 계정을 만들고 키를 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-350">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="674d1-351">닫기 hello **출력** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-351">Close hello **Outputs** blade.</span></span> 

## <a name="start-hello-streaming-analytics-job"></a><span data-ttu-id="674d1-352">Hello 스트리밍 분석 작업 시작</span><span class="sxs-lookup"><span data-stu-id="674d1-352">Start hello Streaming Analytics job</span></span>

<span data-ttu-id="674d1-353">hello 작업이 구성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-353">hello job is now configured.</span></span> <span data-ttu-id="674d1-354">입력 (hello 이벤트 허브), (hello 쿼리 toolook 사기성 호출에 대 한), 변환 및 출력 (blob storage)를 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-354">You've specified an input (hello event hub), a transformation (hello query toolook for fraudulent calls), and an output (blob storage).</span></span> <span data-ttu-id="674d1-355">이제 hello 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-355">You can now start hello job.</span></span> 

1. <span data-ttu-id="674d1-356">Hello TelcoGenerator 앱이 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-356">Make sure hello TelcoGenerator app is running.</span></span>

2. <span data-ttu-id="674d1-357">Hello 작업 블레이드에서 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-357">In hello job blade, click **Start**.</span></span>

    ![Hello 스트림 분석 작업 시작](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="674d1-359">Hello에 **시작 작업** 작업 출력의 시작 시간을 선택에 대 한 블레이드 **이제**합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-359">In hello **Start job** blade, for Job output start time, select **Now**.</span></span> 

4. <span data-ttu-id="674d1-360">**시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-360">Click **Start**.</span></span> 

    ![Hello 스트림 분석 작업에 대 한 블레이드 "작업을 시작 합니다."](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="674d1-362">Azure 알리는 hello 작업이 시작 되 고으로 표시 되 면 hello 상태 hello 작업 블레이드에서 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-362">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![Stream Analytics 작업 상태, “실행 중” 표시](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a><span data-ttu-id="674d1-364">변환 하는 hello 데이터 검사</span><span class="sxs-lookup"><span data-stu-id="674d1-364">Examine hello transformed data</span></span>

<span data-ttu-id="674d1-365">이제 Streaming Analytics 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-365">You now have a complete Streaming Analytics job.</span></span> <span data-ttu-id="674d1-366">hello 작업 전화 통화 메타 데이터의 스트림을 검사, 실시간으로 사기성 전화 통화를 찾고 및 이러한 사기성 호출 toostorage에 대 한 정보를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-366">hello job is examining a stream of phone call metadata, looking for fraudulent phone calls in real time, and writing information about those fraudulent calls toostorage.</span></span> 

<span data-ttu-id="674d1-367">toocomplete이이 자습서에서는 toolook hello 스트리밍 분석 작업에서 캡처되는 hello 데이터에서 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-367">toocomplete this tutorial, you might want toolook at hello data being captured by hello Streaming Analytics job.</span></span> <span data-ttu-id="674d1-368">hello 데이터 tooAzure 블로그 저장소 청크 (파일)에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-368">hello data is being written tooAzure Blog Storage in chunks (files).</span></span> <span data-ttu-id="674d1-369">Azure Blob Storage를 읽는 데 아무 도구나 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-369">You can use any tool that reads Azure Blob Storage.</span></span> <span data-ttu-id="674d1-370">Hello 전제 조건 섹션에서에서 설명한 대로, Visual Studio에서 Azure 확장을 사용할 수 있습니다 또는 같은 도구를 사용할 수 있습니다 [Azure 저장소 탐색기](http://storageexplorer.com/) 또는 [Azure 탐색기](http://www.cerebrata.com/products/azure-explorer/introduction)합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-370">As noted in hello Prerequisites section, you can use Azure extensions in Visual Studio, or you can use a tool like [Azure Storage Explorer](http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction).</span></span> 

<span data-ttu-id="674d1-371">Blob 저장소에 파일의 내용을 hello를 살펴보면 hello 다음과 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-371">When you examine hello contents of a file in blob storage, you see something like hello following :</span></span>

![Streaming Analytics 출력이 있는 Azure Blob Storage](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a><span data-ttu-id="674d1-373">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="674d1-373">Clean up resources</span></span>

<span data-ttu-id="674d1-374">Hello 사기 감지 시나리오를 계속 하 고이 자습서에서 만든 hello 리소스를 사용 하는 추가 문서 개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-374">We have additional articles that continue with hello fraud-detection scenario and that use hello resources that you've created in this tutorial.</span></span> <span data-ttu-id="674d1-375">Toocontinue hello 제안 아래를 참조 하십시오 **다음 단계** 나중입니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-375">If you want toocontinue, see hello suggestions under **Next steps** later.</span></span>

<span data-ttu-id="674d1-376">그러나 수행 하는 경우에 만든 hello 리소스를 필요 하지 않습니다 삭제할 수 있습니다 이러한를 불필요 한 요금이 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-376">However, if you're done and you don't need hello resources you've created, you can delete them so that you don't incur unnecessary Azure charges.</span></span> <span data-ttu-id="674d1-377">이 경우 다음 hello 수행을 제안 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-377">In that case, we suggest that you do hello following:</span></span>

1. <span data-ttu-id="674d1-378">Hello 스트리밍 분석 작업을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-378">Stop hello Streaming Analytics job.</span></span> <span data-ttu-id="674d1-379">Hello에 **작업** 블레이드에서 클릭 **중지** hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-379">In hello **Jobs** blade, click **Stop** at hello top.</span></span>
2. <span data-ttu-id="674d1-380">Hello Telco 생성기 앱을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-380">Stop hello Telco Generator app.</span></span> <span data-ttu-id="674d1-381">Hello 앱을 빠르게 hello 명령 창에서 Ctrl + C를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-381">In hello command window where you started hello app, press Ctrl+C.</span></span>
3. <span data-ttu-id="674d1-382">이 자습서에 대해 새 Blob Storage 계정을 만든 경우 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-382">If you created a new blob storage account just for this tutorial, delete it.</span></span> 
4. <span data-ttu-id="674d1-383">Hello 스트리밍 분석 작업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-383">Delete hello Streaming Analytics job.</span></span>
5. <span data-ttu-id="674d1-384">Hello 이벤트 허브를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-384">Delete hello event hub.</span></span>
6. <span data-ttu-id="674d1-385">Hello 이벤트 허브 네임 스페이스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-385">Delete hello event hub namespace.</span></span>

## <a name="get-support"></a><span data-ttu-id="674d1-386">지원 받기</span><span class="sxs-lookup"><span data-stu-id="674d1-386">Get support</span></span>

<span data-ttu-id="674d1-387">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="674d1-387">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="674d1-388">다음 단계</span><span class="sxs-lookup"><span data-stu-id="674d1-388">Next steps</span></span>

<span data-ttu-id="674d1-389">다음 문서는 hello와이 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-389">You can continue this tutorial with hello following articles:</span></span>

* <span data-ttu-id="674d1-390">[Stream Analytics 및 Power BI: 스트리밍 데이터에 대한 실시간 분석 대시보드](stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="674d1-390">[Stream Analytics and Power BI: A real-time analytics dashboard for streaming data](stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="674d1-391">이 문서에서는 toosend hello hello 스트림 분석의 출력을 TelCo tooPower BI 실시간 시각화 및 분석을 위해 작업 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-391">This article shows you how toosend hello TelCo output of hello Stream Analytics job tooPower BI for real-time visualization and analysis.</span></span>
* <span data-ttu-id="674d1-392">[어떻게 Azure 함수를 사용 하는 Azure Redis Cache에서 Azure 스트림 분석에서 toostore 데이터](stream-analytics-functions-redis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-392">[How toostore data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions](stream-analytics-functions-redis.md).</span></span> <span data-ttu-id="674d1-393">이 문서에서는 toouse Azure 함수 toowrite 사기성 tooan Azure Redis 캐시 서비스 버스 큐를 통해 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="674d1-393">This article shows how toouse Azure Functions toowrite fraudulent calls tooan Azure Redis cache via a Service Bus queue.</span></span>

<span data-ttu-id="674d1-394">일반적인 Stream Analytics에 대한 자세한 내용은 다음 문서를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="674d1-394">For more information about Stream Analytics in general, try these articles:</span></span>

* [<span data-ttu-id="674d1-395">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="674d1-395">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="674d1-396">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="674d1-396">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="674d1-397">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="674d1-397">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="674d1-398">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="674d1-398">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
