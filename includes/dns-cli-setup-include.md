## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="724dc-101">Azure DNS용 Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="724dc-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="724dc-102">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="724dc-102">Before you begin</span></span>

<span data-ttu-id="724dc-103">구성을 시작 하기 전에 다음 항목 hello 수 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="724dc-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="724dc-104">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="724dc-104">An Azure subscription.</span></span> <span data-ttu-id="724dc-105">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="724dc-106">Hello 최신 버전의 hello Windows, Linux 또는 MAC.에 사용할 수 있는 Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-106">Install hello latest version of hello Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="724dc-107">자세한 내용은 [설치 hello Azure CLI](../articles/cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-107">More information is available at [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="724dc-108">Azure 계정 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="724dc-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="724dc-109">콘솔 창을 열고 자격 증명을 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="724dc-110">자세한 내용은 참조 [tooAzure hello Azure CLI에서에서 로그인](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="724dc-110">For more information, see [Log in tooAzure from hello Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="724dc-111">CLI 모드 전환</span><span class="sxs-lookup"><span data-stu-id="724dc-111">Switch CLI mode</span></span>

<span data-ttu-id="724dc-112">Azure DNS는 Azure 리소스 관리자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="724dc-113">CLI 모드 toouse Azure 리소스 관리자 명령 전환 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-113">Make sure you switch CLI mode toouse Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a><span data-ttu-id="724dc-114">Hello 구독 선택</span><span class="sxs-lookup"><span data-stu-id="724dc-114">Select hello subscription</span></span>

<span data-ttu-id="724dc-115">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-115">Check hello subscriptions for hello account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="724dc-116">Azure 구독 toouse 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-116">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="724dc-117">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="724dc-117">Create a resource group</span></span>

<span data-ttu-id="724dc-118">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="724dc-119">이것은 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-119">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="724dc-120">그러나 모든 DNS 리소스가 하지 지역, 글로벌 되므로 hello 다양 한 리소스 그룹 위치에 어떠한 영향도 미치지 Azure DNS 합니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-120">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="724dc-121">기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="724dc-122">리소스 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="724dc-122">Register resource provider</span></span>

<span data-ttu-id="724dc-123">hello Azure DNS 서비스는 hello Microsoft.Network 리소스 공급자에 의해 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-123">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="724dc-124">Azure 구독 등록된 toouse Azure DNS를 사용 하려면 먼저이 리소스 공급자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-124">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="724dc-125">이 작업은 각 구독에 대해 한 번만 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="724dc-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

