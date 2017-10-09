
## <a name="start-your-powershell-session"></a>PowerShell 세션 시작
첫째, 있습니다 해야가 hello 최신 Azure PowerShell 설치 및 실행 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs)합니다.

> [!NOTE]
> SQL 데이터베이스의 여러 가지 새로운 기능이 hello를 사용 하는 경우에 지원 됩니다 [Azure 리소스 관리자 배포 모델](../articles/azure-resource-manager/resource-group-overview.md)예제 hello를 사용 하므로 [Azure SQL 데이터베이스 PowerShell cmdlet](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx) 리소스 관리자에 대 한 . hello 서비스 관리 (클래식) 배포 모델 [Azure SQL 데이터베이스 서비스 관리 cmdlet](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) 이전 버전과 호환성을 위해 사용할 수 있지만 리소스 관리자 cmdlet hello를 사용 하는 것이 좋습니다.
> 
> 

Hello 실행 [ **추가 AzureRmAccount** ](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) cmdlet과 있습니다 나타납니다 로그인 화면 tooenter 자격 증명입니다. 사용 하 여 hello 동일 toosign toohello Azure 포털에서에서 사용 하는 자격 증명입니다.

```PowerShell
Add-AzureRmAccount
```

여러 구독이 있는 경우 사용 하 여 hello [ **집합 AzureRmContext** ](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) cmdlet tooselect 어떤 구독 PowerShell 세션에서 사용 하도록 합니다. 어떤 구독이 현재 PowerShell 세션을 사용 하는 hello toosee 실행 [ **Get AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx)합니다. 모든 구독을 실행 하는 toosee [ **Get AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx)합니다.

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
