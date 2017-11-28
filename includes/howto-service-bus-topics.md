## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="bfa3b-101">서비스 버스 토픽 및 구독 정의</span><span class="sxs-lookup"><span data-stu-id="bfa3b-101">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="bfa3b-102">서비스 버스 토픽 및 구독은 *게시/구독* 메시징 통신 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-102">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="bfa3b-103">토픽 및 구독을 사용하는 경우 분산 응용 프로그램의 구성 요소가 서로 직접 통신하지 않고 중간자 역할을 하는 토픽을 통해 메시지를 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-103">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/howto-service-bus-topics/sb-topics-01.png)

<span data-ttu-id="bfa3b-105">각 메시지가 단일 소비자에 의해 처리되는 서비스 버스 큐와 반대로, 토픽과 구독은 게시/구독 패턴을 사용하여 "일 대 다" 형태의 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-105">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="bfa3b-106">하나의 토픽에 여러 구독을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-106">It is possible to register multiple subscriptions to a topic.</span></span> <span data-ttu-id="bfa3b-107">토픽에 메시지를 전송하면 각 구독에서 독립적으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-107">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span></span>

<span data-ttu-id="bfa3b-108">토픽 구독은 토픽에 전송된 메시지의 복사본을 받는 가상 큐와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-108">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span></span> <span data-ttu-id="bfa3b-109">선택적으로 구독별 토픽에 대한 필터 규칙을 등록할 수 있으며, 이렇게 하면 각 토픽 구독에서 받는 토픽 메시지를 필터링 또는 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-109">You can optionally register filter rules for a topic on a per-subscription basis, which enables you to filter or restrict which messages to a topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="bfa3b-110">서비스 버스 토픽 및 구독을 사용하면 다수의 사용자와 응용 프로그램에 대해 많은 수의 메시지를 확장하고 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-110">Service Bus topics and subscriptions enable you to scale and process a very large number of messages across many users and applications.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="bfa3b-111">네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="bfa3b-111">Create a namespace</span></span>
<span data-ttu-id="bfa3b-112">Azure에서 서비스 버스 토픽 및 구독 사용을 시작하려면 먼저 *서비스 네임스페이스*를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-112">To begin using Service Bus topics and subscriptions in Azure, you must first create a *service namespace*.</span></span> <span data-ttu-id="bfa3b-113">네임스페이스는 응용 프로그램 내에서 서비스 버스 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-113">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="bfa3b-114">네임스페이스를 만들려면</span><span class="sxs-lookup"><span data-stu-id="bfa3b-114">To create a namespace:</span></span>

1. <span data-ttu-id="bfa3b-115">[Azure Portal][Azure portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-115">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="bfa3b-116">포털의 왼쪽 탐색 창에서 **새로 만들기**, **엔터프라이즈 통합** 및 **Service Bus**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-116">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="bfa3b-117">**네임스페이스 만들기** 대화 상자에서 네임스페이스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-117">In the **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="bfa3b-118">시스템에서 사용 가능한 이름인지 즉시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-118">The system immediately checks to see if the name is available.</span></span>
4. <span data-ttu-id="bfa3b-119">네임스페이스 이름을 사용할 수 있게 설정한 후 가격 책정 계층(기본, 표준 또는 프리미엄)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-119">After making sure the namespace name is available, choose the pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="bfa3b-120">**구독** 필드에서 네임스페이스를 만들 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-120">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span></span>
6. <span data-ttu-id="bfa3b-121">**리소스 그룹** 필드에서 네임스페이스가 있는 기존 리소스 그룹을 선택하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-121">In the **Resource group** field, choose an existing resource group in which the namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="bfa3b-122">**위치**에서 네임스페이스가 호스트되어야 하는 국가 또는 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-122">In **Location**, choose the country or region in which your namespace should be hosted.</span></span>
   
    ![네임스페이스 만들기][create-namespace]
8. <span data-ttu-id="bfa3b-124">**만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-124">Click the **Create** button.</span></span> <span data-ttu-id="bfa3b-125">이제 시스템이 네임스페이스를 만들고 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-125">The system now creates your namespace and enables it.</span></span> <span data-ttu-id="bfa3b-126">시스템이 계정에 대한 리소스를 프로비전하는 동안 몇 분 정도 기다려야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-126">You might have to wait several minutes as the system provisions resources for your account.</span></span>

### <a name="obtain-the-credentials"></a><span data-ttu-id="bfa3b-127">자격 증명 얻기</span><span class="sxs-lookup"><span data-stu-id="bfa3b-127">Obtain the credentials</span></span>
1. <span data-ttu-id="bfa3b-128">네임스페이스 목록에서 새로 만든 네임스페이스 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-128">In the list of namespaces, click the newly created namespace name.</span></span>
2. <span data-ttu-id="bfa3b-129">**Service Bus 네임스페이스** 블레이드에서 **공유 액세스 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-129">In the **Service Bus namespace** blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="bfa3b-130">**공유 액세스 정책** 블레이드에서 **RootManageSharedAccessKey**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-130">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="bfa3b-132">**정책: RootManageSharedAccessKey** 블레이드에서 **연결 문자열–기본 키** 옆의 복사 단추를 클릭하여 나중에 사용하기 위해 연결 문자열을 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bfa3b-132">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span></span>
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


