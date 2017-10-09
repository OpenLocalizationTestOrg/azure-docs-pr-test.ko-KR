## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="d25ce-101">Azure DNS를 위한 Azure PowerShell 설정</span><span class="sxs-lookup"><span data-stu-id="d25ce-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="d25ce-102">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d25ce-102">Before you begin</span></span>

<span data-ttu-id="d25ce-103">구성을 시작 하기 전에 다음 항목 hello 수 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d25ce-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="d25ce-104">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="d25ce-104">An Azure subscription.</span></span> <span data-ttu-id="d25ce-105">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d25ce-106">Hello tooinstall hello Azure 리소스 관리자 PowerShell cmdlet의 최신 버전이 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-106">You need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="d25ce-107">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs)합니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="d25ce-108">Azure 계정 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="d25ce-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="d25ce-109">PowerShell 콘솔을 열고 tooyour 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-109">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="d25ce-110">자세한 내용은 [Resource Manager에서 PowerShell 사용](../articles/azure-resource-manager/powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d25ce-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a><span data-ttu-id="d25ce-111">Hello 구독 선택</span><span class="sxs-lookup"><span data-stu-id="d25ce-111">Select hello subscription</span></span>
 
<span data-ttu-id="d25ce-112">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-112">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="d25ce-113">Azure 구독 toouse 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-113">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="d25ce-114">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d25ce-114">Create a resource group</span></span>

<span data-ttu-id="d25ce-115">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d25ce-116">이 위치는 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-116">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="d25ce-117">그러나 모든 DNS 리소스가 하지 지역, 글로벌 되므로 hello 다양 한 리소스 그룹 위치에 어떠한 영향도 미치지 Azure DNS 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-117">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="d25ce-118">기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="d25ce-119">리소스 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="d25ce-119">Register resource provider</span></span>

<span data-ttu-id="d25ce-120">hello Azure DNS 서비스는 hello Microsoft.Network 리소스 공급자에 의해 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-120">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="d25ce-121">Azure 구독 등록된 toouse Azure DNS를 사용 하려면 먼저이 리소스 공급자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-121">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="d25ce-122">이 작업은 각 구독에 대해 한 번만 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25ce-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```