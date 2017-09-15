## <a name="prepare-to-authenticate-azure-resource-manager-requests"></a><span data-ttu-id="4c12c-101">Azure Resource Manager 요청 인증 준비</span><span class="sxs-lookup"><span data-stu-id="4c12c-101">Prepare to authenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="4c12c-102">Azure AD(Active Directory)에서 [Azure Resource Manager][lnk-authenticate-arm]를 사용하여 리소스에서 수행하는 모든 작업을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-102">You must authenticate all the operations that you perform on resources using the [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="4c12c-103">가장 쉽게 구성할 수 있는 방법은 PowerShell 또는 Azure CLI를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-103">The easiest way to configure this is to use PowerShell or Azure CLI.</span></span>

<span data-ttu-id="4c12c-104">계속하기 전에 [Azure PowerShell cmdlet][lnk-powershell-install]을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-104">Install the [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="4c12c-105">다음 단계는 PowerShell을 사용하여 AD 응용 프로그램에 대해 암호 인증을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-105">The following steps show how to set up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="4c12c-106">표준 PowerShell 세션에서 이러한 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="4c12c-107">다음 명령을 사용하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-107">Log in to your Azure subscription using the following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="4c12c-108">Azure 구독이 여러 개 있는 경우 Azure에 로그인하면 자격 증명과 연결된 모든 Azure 구독에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-108">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="4c12c-109">다음 명령을 사용하여 사용할 수 있는 Azure 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-109">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="4c12c-110">다음 명령을 사용하여 IoT Hub를 관리하는 명령을 실행하는 데 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-110">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="4c12c-111">이전 명령의 출력에서 구독 이름 또는 ID를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-111">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="4c12c-112">**TenantId** 및 **SubscriptionId**를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="4c12c-113">나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-113">You need them later.</span></span>
3. <span data-ttu-id="4c12c-114">다음 명령을 사용하여 새 Azure Active Directory 응용 프로그램을 만듭니다. 자리 표시자는 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-114">Create a new Azure Active Directory application using the following command, replacing the place holders:</span></span>
   
   * <span data-ttu-id="4c12c-115">**{표시 이름}:** **MySampleApp**과 같은 응용 프로그램의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="4c12c-116">**{홈페이지 URL}:** **http://mysampleapp/home**과 같은 앱의 홈페이지의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-116">**{Home page URL}:** the URL of the home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="4c12c-117">이 URL이 실제 응용 프로그램을 가리킬 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-117">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="4c12c-118">**{응용 프로그램 식별자}:** **http://mysampleapp**과 같은 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="4c12c-119">이 URL이 실제 응용 프로그램을 가리킬 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-119">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="4c12c-120">**{암호}:** 앱에서 인증하기 위해 사용할 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-120">**{Password}:** A password that you use to authenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="4c12c-121">만든 응용 프로그램의 **ApplicationId** 를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-121">Make a note of the **ApplicationId** of the application you created.</span></span> <span data-ttu-id="4c12c-122">나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-122">You need this later.</span></span>
5. <span data-ttu-id="4c12c-123">다음 명령을 사용하여 새 서비스 주체를 만듭니다. 이전 단계에서 **{MyApplicationId}**를 **ApplicationId**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-123">Create a new service principal using the following command, replacing **{MyApplicationId}** with the **ApplicationId** from the previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="4c12c-124">다음 명령을 사용하여 역할 할당을 설정합니다. **{MyApplicationId}**를 **ApplicationId**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-124">Set up a role assignment using the following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="4c12c-125">이제 사용자 지정 C# 응용 프로그램에서 인증할 수 있는 Azure AD 응용 프로그램을 만드는 작업을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-125">You have now finished creating the Azure AD application that enables you to authenticate from your custom C# application.</span></span> <span data-ttu-id="4c12c-126">이 자습서의 뒷부분에서 다음 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4c12c-126">You need the following values later in this tutorial:</span></span>

* <span data-ttu-id="4c12c-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="4c12c-127">TenantId</span></span>
* <span data-ttu-id="4c12c-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="4c12c-128">SubscriptionId</span></span>
* <span data-ttu-id="4c12c-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="4c12c-129">ApplicationId</span></span>
* <span data-ttu-id="4c12c-130">암호</span><span class="sxs-lookup"><span data-stu-id="4c12c-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
