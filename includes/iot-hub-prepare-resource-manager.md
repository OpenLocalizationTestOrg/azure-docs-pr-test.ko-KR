## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a><span data-ttu-id="5b61d-101">Azure 리소스 관리자 요청 tooauthenticate 준비</span><span class="sxs-lookup"><span data-stu-id="5b61d-101">Prepare tooauthenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="5b61d-102">Hello를 사용 하 여 리소스에서 수행 하는 모든 hello 작업을 인증 해야 [Azure 리소스 관리자] [ lnk-authenticate-arm] 와 Azure AD (Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5b61d-102">You must authenticate all hello operations that you perform on resources using hello [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="5b61d-103">가장 쉬운 방법은 tooconfigure hello toouse PowerShell 또는 Azure CLI입니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-103">hello easiest way tooconfigure this is toouse PowerShell or Azure CLI.</span></span>

<span data-ttu-id="5b61d-104">Hello 설치 [Azure PowerShell cmdlet] [ lnk-powershell-install] 계속 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="5b61d-104">Install hello [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="5b61d-105">단계 표시 방법을 따르는 hello tooset PowerShell을 사용 하 여 AD 응용 프로그램에 대 한 암호 인증을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-105">hello following steps show how tooset up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="5b61d-106">표준 PowerShell 세션에서 이러한 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="5b61d-107">다음 명령을 hello를 사용 하 여 Azure 구독 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-107">Log in tooyour Azure subscription using hello following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="5b61d-108">TooAzure 로그인 여러 Azure 구독이 있는 경우 tooall 액세스 부여 hello 자격 증명으로 연결 된 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="5b61d-108">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="5b61d-109">다음 명령을 toolist hello 있습니다 사용할 수 있는 Azure 구독 toouse hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-109">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="5b61d-110">다음 명령은 tooselect 구독 toouse toorun hello 명령을 toomanage IoT 허브를 지정 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-110">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="5b61d-111">Hello 이전 명령의 hello 출력에서 hello 구독 이름 또는 ID를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-111">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="5b61d-112">**TenantId** 및 **SubscriptionId**를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="5b61d-113">나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-113">You need them later.</span></span>
3. <span data-ttu-id="5b61d-114">다음 명령을, hello 자리 표시자를 대체 하는 hello를 사용 하 여 새 Azure Active Directory 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-114">Create a new Azure Active Directory application using hello following command, replacing hello place holders:</span></span>
   
   * <span data-ttu-id="5b61d-115">**{표시 이름}:** **MySampleApp**과 같은 응용 프로그램의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="5b61d-116">**{홈 페이지 URL}:** 와 같은 응용 프로그램의 hello 홈 페이지의 URL을 hello **http://mysampleapp/home**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-116">**{Home page URL}:** hello URL of hello home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="5b61d-117">이 URL toopoint tooa 실제 응용 프로그램이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-117">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="5b61d-118">**{응용 프로그램 식별자}:** **http://mysampleapp**과 같은 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="5b61d-119">이 URL toopoint tooa 실제 응용 프로그램이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-119">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="5b61d-120">**{Password}:** tooauthenticate 응용 프로그램과 함께 사용 하는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-120">**{Password}:** A password that you use tooauthenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="5b61d-121">Hello 메모 **ApplicationId** 만든 hello 응용 프로그램의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-121">Make a note of hello **ApplicationId** of hello application you created.</span></span> <span data-ttu-id="5b61d-122">나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-122">You need this later.</span></span>
5. <span data-ttu-id="5b61d-123">다음 명령을, 대체 hello를 사용 하 여 새 서비스 사용자를 만들 **{MyApplicationId}** hello로 **ApplicationId** hello 이전 단계에서:</span><span class="sxs-lookup"><span data-stu-id="5b61d-123">Create a new service principal using hello following command, replacing **{MyApplicationId}** with hello **ApplicationId** from hello previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="5b61d-124">다음 명령을, 대체 hello를 사용 하 여 역할 할당을 설정 **{MyApplicationId}** 와 프로그램 **ApplicationId**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-124">Set up a role assignment using hello following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="5b61d-125">이제 사용자 지정 C# 응용 프로그램에서 tooauthenticate 수 있는 hello Azure AD 응용 프로그램을 만드는 작업이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-125">You have now finished creating hello Azure AD application that enables you tooauthenticate from your custom C# application.</span></span> <span data-ttu-id="5b61d-126">다음 값에는이 자습서의 뒷부분에 나오는 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b61d-126">You need hello following values later in this tutorial:</span></span>

* <span data-ttu-id="5b61d-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="5b61d-127">TenantId</span></span>
* <span data-ttu-id="5b61d-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="5b61d-128">SubscriptionId</span></span>
* <span data-ttu-id="5b61d-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="5b61d-129">ApplicationId</span></span>
* <span data-ttu-id="5b61d-130">암호</span><span class="sxs-lookup"><span data-stu-id="5b61d-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
