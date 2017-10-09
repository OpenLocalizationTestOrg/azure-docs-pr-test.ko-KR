## <a name="set-up-azure-powershell-for-azure-dns"></a>Azure DNS를 위한 Azure PowerShell 설정

### <a name="before-you-begin"></a>시작하기 전에

구성을 시작 하기 전에 다음 항목 hello 수 있는지 확인 하십시오.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.
* Hello tooinstall hello Azure 리소스 관리자 PowerShell cmdlet의 최신 버전이 있어야합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs)합니다.

### <a name="sign-in-tooyour-azure-account"></a>Azure 계정 tooyour에 로그인

PowerShell 콘솔을 열고 tooyour 계정을 연결 합니다. 자세한 내용은 [Resource Manager에서 PowerShell 사용](../articles/azure-resource-manager/powershell-azure-resource-manager.md)을 참조하세요.

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a>Hello 구독 선택
 
Hello 계정에 대 한 hello 구독을 확인 합니다.

```powershell
Get-AzureRmSubscription
```

Azure 구독 toouse 선택 합니다.

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다. 이 위치는 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다. 그러나 모든 DNS 리소스가 하지 지역, 글로벌 되므로 hello 다양 한 리소스 그룹 위치에 어떠한 영향도 미치지 Azure DNS 합니다.

기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛸 수 있습니다.

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a>리소스 공급자 등록

hello Azure DNS 서비스는 hello Microsoft.Network 리소스 공급자에 의해 관리 됩니다. Azure 구독 등록된 toouse Azure DNS를 사용 하려면 먼저이 리소스 공급자 여야 합니다. 이 작업은 각 구독에 대해 한 번만 수행하면 됩니다.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```