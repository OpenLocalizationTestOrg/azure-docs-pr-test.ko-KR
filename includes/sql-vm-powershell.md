
## <a name="start-your-powershell-session"></a><span data-ttu-id="19a53-101">PowerShell 세션 시작</span><span class="sxs-lookup"><span data-stu-id="19a53-101">Start your PowerShell session</span></span>
<span data-ttu-id="19a53-102">먼저 toohave hello 최신 [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) 설치 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a53-102">First you need toohave hello latest [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="19a53-103">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs)합니다.</span><span class="sxs-lookup"><span data-stu-id="19a53-103">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

> [!NOTE]
> <span data-ttu-id="19a53-104">에서 예제가 항목에서는 hello [Azure 리소스 관리자 배포 모델](../articles/azure-resource-manager/resource-group-overview.md)예제 hello를 사용 하므로 [Azure 리소스 관리자 cmdlet](http://msdn.microsoft.com/library/azure/mt125356.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="19a53-104">hello examples in this topic use [Azure Resource Manager deployment model](../articles/azure-resource-manager/resource-group-overview.md), so examples use hello [Azure Resource Manager cmdlets](http://msdn.microsoft.com/library/azure/mt125356.aspx).</span></span> 
> 
> 

<span data-ttu-id="19a53-105">Hello 실행 [ **추가 AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet 하 고 나타납니다 화면 tooenter 로그인 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="19a53-105">Run hello [**Add-AzureRmAccount**](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet and you will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="19a53-106">사용 하 여 hello 동일 toosign toohello Azure 포털에서에서 사용 하는 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="19a53-106">Use hello same credentials that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="19a53-107">구독이 여러 개 있는 경우 hello 사용할 [ **집합 AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) cmdlet tooselect 어떤 구독 PowerShell 세션에서 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a53-107">If you have multiple subscriptions use hello [**Set-AzureRmContext**](http://msdn.microsoft.com/library/mt619263.aspx) cmdlet tooselect which subscription your PowerShell session should use.</span></span> <span data-ttu-id="19a53-108">어떤 구독이 현재 PowerShell 세션을 사용 하는 hello toosee 실행 [ **Get AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="19a53-108">toosee what subscription hello current PowerShell session is using, run [**Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx).</span></span> <span data-ttu-id="19a53-109">모든 구독을 실행 하는 toosee [ **Get AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="19a53-109">toosee all your subscriptions, run [**Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).</span></span>

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

