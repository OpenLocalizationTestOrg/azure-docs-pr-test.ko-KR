## <a name="setting-up-powershell-for-resource-manager-templates"></a>리소스 관리자 템플릿에 대한 PowerShell 설정
리소스 관리자와 Azure PowerShell을 사용 하려면, 먼저 toohave hello 올바른 Windows PowerShell 및 Azure PowerShell 버전 필요 합니다.

### <a name="verify-powershell-versions"></a>PowerShell 버전 확인
Windows PowerShell 버전 3.0 또는 4.0이 있는지 확인합니다. toofind hello 버전의 Windows PowerShell을 Windows PowerShell 명령 프롬프트에서 다음이 명령을 입력 합니다.

    $PSVersionTable

Hello 다음 유형의 정보를 받게 됩니다.

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


해당 hello 값을 확인 **PSVersion** 3.0 또는 4.0가 있습니다. 그렇지 않으면 [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) 또는 [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855)을 참조하세요.

### <a name="set-your-azure-account-and-subscription"></a>Azure 계정 및 구독 설정
Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.

Azure PowerShell 명령 프롬프트를 열고 tooAzure이이 명령 사용 하 여 로그온 합니다.

    Login-AzureRmAccount

여러 Azure 구독이 있는 경우 다음 명령을 사용하여 Azure 구독을 나열할 수 있습니다.

    Get-AzureRmSubscription

Hello 다음 유형의 정보를 받게 됩니다.

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

Hello Azure PowerShell 명령 프롬프트에서 다음이 명령을 실행 하 여 hello 현재 Azure 구독을 설정할 수 있습니다. Hello < 및 > 문자를 포함 하는 hello 따옴표 안의 hello 올바른 이름으로 바꿉니다.

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

Azure 구독 및 계정에 대 한 자세한 내용은 참조 [하는 방법: tooyour 구독 연결](/powershell/azureps-cmdlets-docs#step-3-connect)합니다.

