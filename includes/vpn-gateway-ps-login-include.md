<span data-ttu-id="30d13-101">이 구성을 시작 하기 전에 tooyour Azure 계정에에서 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d13-101">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="30d13-102">hello cmdlet Azure 계정에 대 한 hello 로그인 자격 증명을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="30d13-102">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="30d13-103">로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d13-103">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span> <span data-ttu-id="30d13-104">자세한 내용은 [리소스 관리자에서 Windows PowerShell 사용](../articles/powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d13-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="30d13-105">toolog을 높은 권한으로 PowerShell 콘솔을 열고 및 tooyour 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d13-105">toolog in, open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="30d13-106">다음 예제에서는 toohelp 연결한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d13-106">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="30d13-107">여러 Azure 구독이 있는 경우 hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d13-107">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="30d13-108">Toouse hello 구독을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d13-108">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```