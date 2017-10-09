## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="2bac6-101">리소스 관리자 템플릿에 대한 PowerShell 설정</span><span class="sxs-lookup"><span data-stu-id="2bac6-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="2bac6-102">리소스 관리자와 Azure PowerShell을 사용 하려면, 먼저 toohave hello 올바른 Windows PowerShell 및 Azure PowerShell 버전 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-102">Before you can use Azure PowerShell with Resource Manager, you will need toohave hello right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="2bac6-103">PowerShell 버전 확인</span><span class="sxs-lookup"><span data-stu-id="2bac6-103">Verify PowerShell versions</span></span>
<span data-ttu-id="2bac6-104">Windows PowerShell 버전 3.0 또는 4.0이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="2bac6-105">toofind hello 버전의 Windows PowerShell을 Windows PowerShell 명령 프롬프트에서 다음이 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-105">toofind hello version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="2bac6-106">Hello 다음 유형의 정보를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-106">You will receive hello following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="2bac6-107">해당 hello 값을 확인 **PSVersion** 3.0 또는 4.0가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-107">Verify that hello value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="2bac6-108">그렇지 않으면 [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) 또는 [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bac6-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="2bac6-109">Azure 계정 및 구독 설정</span><span class="sxs-lookup"><span data-stu-id="2bac6-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="2bac6-110">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="2bac6-111">Azure PowerShell 명령 프롬프트를 열고 tooAzure이이 명령 사용 하 여 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-111">Open an Azure PowerShell command prompt and log on tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="2bac6-112">여러 Azure 구독이 있는 경우 다음 명령을 사용하여 Azure 구독을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="2bac6-113">Hello 다음 유형의 정보를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-113">You will receive hello following type of information:</span></span>

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

<span data-ttu-id="2bac6-114">Hello Azure PowerShell 명령 프롬프트에서 다음이 명령을 실행 하 여 hello 현재 Azure 구독을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-114">You can set hello current Azure subscription by running these commands at hello Azure PowerShell command prompt.</span></span> <span data-ttu-id="2bac6-115">Hello < 및 > 문자를 포함 하는 hello 따옴표 안의 hello 올바른 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-115">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="2bac6-116">Azure 구독 및 계정에 대 한 자세한 내용은 참조 [하는 방법: tooyour 구독 연결](/powershell/azureps-cmdlets-docs#step-3-connect)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bac6-116">For more information about Azure subscriptions and accounts, see [How to: Connect tooyour subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

