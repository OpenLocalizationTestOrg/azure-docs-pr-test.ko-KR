### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="914ee-101">Azure Diagnostics 문제 해결</span><span class="sxs-lookup"><span data-stu-id="914ee-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="914ee-102">Hello 다음과 같은 오류 메시지가 표시 되 면 hello Microsoft.insights 리소스 공급자가 등록 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="914ee-102">If you receive hello following error message, hello Microsoft.insights resource provider is not registered:</span></span>

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="914ee-103">tooregister hello 리소스 공급자 hello hello Azure 포털의에서 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="914ee-103">tooregister hello resource provider, perform hello following steps in hello Azure portal:</span></span>

1.  <span data-ttu-id="914ee-104">Hello hello 왼쪽의 탐색 창에서 클릭 *구독*</span><span class="sxs-lookup"><span data-stu-id="914ee-104">In hello navigation pane on hello left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="914ee-105">Hello 오류 메시지에서 확인 하는 hello 구독 선택</span><span class="sxs-lookup"><span data-stu-id="914ee-105">Select hello subscription identified in hello error message</span></span>
3.  <span data-ttu-id="914ee-106">*리소스 공급자* 클릭</span><span class="sxs-lookup"><span data-stu-id="914ee-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="914ee-107">Hello *Microsoft.insights* 공급자</span><span class="sxs-lookup"><span data-stu-id="914ee-107">Find hello *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="914ee-108">Hello 클릭 *등록* 링크</span><span class="sxs-lookup"><span data-stu-id="914ee-108">Click hello *Register* link</span></span>

![Microsoft.insights 리소스 공급자 등록](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="914ee-110">한 번 hello *Microsoft.insights* 리소스 공급자가 등록 진단 구성 프로그램을 다시 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="914ee-110">Once hello *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="914ee-111">PowerShell을 hello 다음과 같은 오류 메시지가 표시 되 면 PowerShell 버전에서 tooupdate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="914ee-111">In PowerShell, if you receive hello following error message, you need tooupdate your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="914ee-112">2016 년 11 월 (v2.3.0) PowerShell toohello의 버전을 업데이트 또는 hello 지침을 사용 하 여 hello에를 릴리스 이상에서는 [Azure PowerShell cmdlet과 함께 시작](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) 문서.</span><span class="sxs-lookup"><span data-stu-id="914ee-112">Update your version of PowerShell toohello November 2016 (v2.3.0), or later, release using hello instructions in hello [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
