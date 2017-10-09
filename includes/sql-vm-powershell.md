
## <a name="start-your-powershell-session"></a>PowerShell 세션 시작
먼저 toohave hello 최신 [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) 설치 하 고 실행 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs)합니다.

> [!NOTE]
> 에서 예제가 항목에서는 hello [Azure 리소스 관리자 배포 모델](../articles/azure-resource-manager/resource-group-overview.md)예제 hello를 사용 하므로 [Azure 리소스 관리자 cmdlet](http://msdn.microsoft.com/library/azure/mt125356.aspx)합니다. 
> 
> 

Hello 실행 [ **추가 AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet 하 고 나타납니다 화면 tooenter 로그인 자격 증명입니다. 사용 하 여 hello 동일 toosign toohello Azure 포털에서에서 사용 하는 자격 증명입니다.

    Add-AzureRmAccount

구독이 여러 개 있는 경우 hello 사용할 [ **집합 AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) cmdlet tooselect 어떤 구독 PowerShell 세션에서 사용 하도록 합니다. 어떤 구독이 현재 PowerShell 세션을 사용 하는 hello toosee 실행 [ **Get AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx)합니다. 모든 구독을 실행 하는 toosee [ **Get AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx)합니다.

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

