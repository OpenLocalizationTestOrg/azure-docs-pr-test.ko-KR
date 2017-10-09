이 구성을 시작 하기 전에 tooyour Azure 계정에에서 로그인 해야 합니다. hello cmdlet Azure 계정에 대 한 hello 로그인 자격 증명을 묻습니다. 로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정을 다운로드 합니다. 자세한 내용은 [리소스 관리자에서 Windows PowerShell 사용](../articles/powershell-azure-resource-manager.md)을 참조하세요.

toolog을 높은 권한으로 PowerShell 콘솔을 열고 및 tooyour 계정을 연결 합니다. 다음 예제에서는 toohelp 연결한 hello를 사용 합니다.

```powershell
Login-AzureRmAccount
```

여러 Azure 구독이 있는 경우 hello 계정에 대 한 hello 구독을 확인 합니다.

```powershell
Get-AzureRmSubscription
```

Toouse hello 구독을 지정 합니다.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```