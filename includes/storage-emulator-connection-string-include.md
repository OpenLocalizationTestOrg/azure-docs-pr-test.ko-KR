<span data-ttu-id="ab7ab-101">저장소 에뮬레이터 hello 공유 키 인증에 대 한 단일 고정 계정과 잘 알려진 인증 키를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-101">hello storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="ab7ab-102">이 계정과 키는 hello만 공유 된 키 자격 증명 hello 저장소 에뮬레이터와 함께 사용 하기 위해 허용.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-102">This account and key are hello only Shared Key credentials permitted for use with hello storage emulator.</span></span> <span data-ttu-id="ab7ab-103">아래에 이 계정과 키의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="ab7ab-104">클라이언트 인증 코드의 테스트 hello 기능에 대해서만 hello 인증 키 hello 저장소 에뮬레이터에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-104">hello authentication key supported by hello storage emulator is intended only for testing hello functionality of your client authentication code.</span></span> <span data-ttu-id="ab7ab-105">보안 기능은 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-105">It does not serve any security purpose.</span></span> <span data-ttu-id="ab7ab-106">Hello 저장소 에뮬레이터와 함께 프로덕션 저장소 계정 및 키를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-106">You cannot use your production storage account and key with hello storage emulator.</span></span> <span data-ttu-id="ab7ab-107">하지 프로덕션 데이터와 함께 hello 개발 계정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-107">You should not use hello development account with production data.</span></span>
> 
> <span data-ttu-id="ab7ab-108">hello 저장소 에뮬레이터만 HTTP 통해 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-108">hello storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="ab7ab-109">그러나 HTTPS는 hello 프로토콜 프로덕션 Azure 저장소 계정 리소스에 액세스 하기 위한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-109">However, HTTPS is hello recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a><span data-ttu-id="ab7ab-110">바로 가기를 사용 하 여 toohello 에뮬레이터 계정을 연결 하세요.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-110">Connect toohello emulator account using a shortcut</span></span>
<span data-ttu-id="ab7ab-111">hello 가장 쉬운 방법은 tooconnect toohello 저장소 에뮬레이터에서 응용 프로그램은 tooconfigure hello 바로 가기 참조 하는 응용 프로그램 구성 파일에서 연결 문자열을 `UseDevelopmentStorage=true`합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-111">hello easiest way tooconnect toohello storage emulator from your application is tooconfigure a connection string in your application's configuration file that references hello shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="ab7ab-112">연결 문자열 toohello 저장소 에뮬레이터의 예로 *app.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="ab7ab-112">Here's an example of a connection string toohello storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a><span data-ttu-id="ab7ab-113">Hello 잘 알려진 계정 이름과 키를 사용 하 여 toohello 에뮬레이터 계정을 연결 하세요.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-113">Connect toohello emulator account using hello well-known account name and key</span></span>
<span data-ttu-id="ab7ab-114">toocreate 참조 hello 에뮬레이터 계정 이름 및 키를 지정 해야 hello 끝점 서비스를 각각 hello에 대 한 연결 문자열 hello 연결 문자열에 hello 에뮬레이터에서 toouse를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-114">toocreate a connection string that references hello emulator account name and key, you must specify hello endpoints for each of hello services you wish toouse from hello emulator in hello connection string.</span></span> <span data-ttu-id="ab7ab-115">이 소프트웨어는 hello 연결 문자열은 프로덕션 저장소 계정에 대 한 것과 다른 hello 에뮬레이터 끝점 참조를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-115">This is necessary so that hello connection string will reference hello emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="ab7ab-116">예를 들어 연결 문자열의 hello 값은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-116">For example, hello value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="ab7ab-117">이 값은 위에 표시 된 동일 toohello 바로 가기 `UseDevelopmentStorage=true`합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-117">This value is identical toohello shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="ab7ab-118">HTTP 프록시 지정</span><span class="sxs-lookup"><span data-stu-id="ab7ab-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="ab7ab-119">Hello 저장소 에뮬레이터에 대 한 서비스를 테스트할 때 HTTP 프록시 toouse를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-119">You can also specify an HTTP proxy toouse when you're testing your service against hello storage emulator.</span></span> <span data-ttu-id="ab7ab-120">이 hello 저장소 서비스에 대 한 작업을 디버깅 하는 동안 HTTP 요청 및 응답을 관찰 하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-120">This can be useful for observing HTTP requests and responses while you're debugging operations against hello storage services.</span></span> <span data-ttu-id="ab7ab-121">프록시, toospecify 추가 hello `DevelopmentStorageProxyUri` toohello 연결 문자열 옵션 및 해당 값 toohello 프록시 URI를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-121">toospecify a proxy, add hello `DevelopmentStorageProxyUri` option toohello connection string, and set its value toohello proxy URI.</span></span> <span data-ttu-id="ab7ab-122">예를 들어 다음은 toohello 저장소 에뮬레이터를 가리키고 HTTP 프록시를 구성 하는 연결 문자열이입니다.</span><span class="sxs-lookup"><span data-stu-id="ab7ab-122">For example, here is a connection string that points toohello storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

