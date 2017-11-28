
## <a name="start-your-powershell-session"></a><span data-ttu-id="38c13-101">PowerShell 세션 시작</span><span class="sxs-lookup"><span data-stu-id="38c13-101">Start your PowerShell session</span></span>
<span data-ttu-id="38c13-102">우선 최신 [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) 을 설치하고 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38c13-102">First you need to have the latest [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="38c13-103">자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azureps-cmdlets-docs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38c13-103">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

> [!NOTE]
> <span data-ttu-id="38c13-104">이 항목의 예제에서는 [Azure Resource Manager 배포 모델](../articles/azure-resource-manager/resource-group-overview.md)을 사용하므로 예제에 [Azure Resource Manager cmdlet](http://msdn.microsoft.com/library/azure/mt125356.aspx)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="38c13-104">The examples in this topic use [Azure Resource Manager deployment model](../articles/azure-resource-manager/resource-group-overview.md), so examples use the [Azure Resource Manager cmdlets](http://msdn.microsoft.com/library/azure/mt125356.aspx).</span></span> 
> 
> 

<span data-ttu-id="38c13-105">[**Add-AzureRmAccount**](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet을 실행하면 자격 증명을 입력할 수 있는 로그인 화면이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="38c13-105">Run the [**Add-AzureRmAccount**](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet and you will be presented with a sign in screen to enter your credentials.</span></span> <span data-ttu-id="38c13-106">Azure 포털에 로그인하는 데 사용하는 동일한 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38c13-106">Use the same credentials that you use to sign in to the Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="38c13-107">여러 구독이 있는 경우 [**Set-AzureRmContext**](http://msdn.microsoft.com/library/mt619263.aspx) cmdlet을 사용하여 PowerShell 세션이 사용해야 하는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38c13-107">If you have multiple subscriptions use the [**Set-AzureRmContext**](http://msdn.microsoft.com/library/mt619263.aspx) cmdlet to select which subscription your PowerShell session should use.</span></span> <span data-ttu-id="38c13-108">현재 PowerShell 세션이 사용 중인 구독을 보려면 [**Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="38c13-108">To see what subscription the current PowerShell session is using, run [**Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx).</span></span> <span data-ttu-id="38c13-109">모든 구독을 보려면 [**Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx)을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="38c13-109">To see all your subscriptions, run [**Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).</span></span>

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

