## <a name="what-is-queue-storage"></a><span data-ttu-id="80be6-101">큐 저장소 정의</span><span class="sxs-lookup"><span data-stu-id="80be6-101">What is Queue Storage?</span></span>
<span data-ttu-id="80be6-102">Azure 큐 저장소는 많은 수의 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 사용 하 여 인증 된 호출을 통해 hello world에 메시지를 저장 하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-102">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="80be6-103">단일 큐 메시지의 크기 (kb) too64 될 수 있습니다 및 큐 수많은 메시지 저장소 계정의 toohello 총 용량 한계를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-103">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

<span data-ttu-id="80be6-104">큐 저장소의 일반적인 사용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-104">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="80be6-105">작업 tooprocess의 백로그를 비동기적으로 만들기</span><span class="sxs-lookup"><span data-stu-id="80be6-105">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="80be6-106">Azure 웹 역할 tooan Azure 작업자 역할에서 메시지를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-106">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="80be6-107">큐 서비스 개념</span><span class="sxs-lookup"><span data-stu-id="80be6-107">Queue Service Concepts</span></span>
<span data-ttu-id="80be6-108">hello를 큐 서비스는 hello를 다음과 같은 구성 요소가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-108">hello Queue service contains hello following components:</span></span>

![Queue1](./media/storage-queue-concepts-include/queue1.png)

* <span data-ttu-id="80be6-110">**URL 형식:** 큐는 주소 지정 가능한 URL 형식에 따라 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="80be6-110">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="80be6-111">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="80be6-111">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="80be6-112">url hello hello 다이어그램의 큐를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-112">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="80be6-113">**저장소 계정:** 저장소 계정을 통해 모든 액세스 tooAzure 저장소 작업은 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-113">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="80be6-114">저장소 계정 용량에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](../articles/storage/common/storage-scalability-targets.md) (영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="80be6-114">See [Azure Storage Scalability and Performance Targets](../articles/storage/common/storage-scalability-targets.md) for details about storage account capacity.</span></span>
* <span data-ttu-id="80be6-115">**큐:** 큐에는 메시지 집합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-115">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="80be6-116">모든 메시지는 큐에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-116">All messages must be in a queue.</span></span> <span data-ttu-id="80be6-117">Note 해당 hello 큐 이름은 모두 소문자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-117">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="80be6-118">큐의 명명에 대한 자세한 내용은 [큐 및 메타데이터 명명](https://msdn.microsoft.com/library/azure/dd179349.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80be6-118">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>
* <span data-ttu-id="80be6-119">**메시지:** A 메시지, 모든 형식으로의 too64 KB를 합니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-119">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="80be6-120">hello 메시지 hello 큐에 남아 있을 수 있는 최대 시간 7 일입니다.</span><span class="sxs-lookup"><span data-stu-id="80be6-120">hello maximum time that a message can remain in hello queue is 7 days.</span></span>

