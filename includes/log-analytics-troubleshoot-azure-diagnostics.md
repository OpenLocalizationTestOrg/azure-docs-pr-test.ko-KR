### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="0557c-101">Azure Diagnostics 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0557c-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="0557c-102">다음과 같은 오류 메시지를 받으면 Microsoft.insights 리소스 공급자가 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0557c-102">If you receive the following error message, the Microsoft.insights resource provider is not registered:</span></span>

`Failed to update diagnostics for 'resource'. {"code":"Forbidden","message":"Please register the subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="0557c-103">리소스 공급자를 등록하려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0557c-103">To register the resource provider, perform the following steps in the Azure portal:</span></span>

1.  <span data-ttu-id="0557c-104">왼쪽의 탐색 창에서 *구독* 클릭</span><span class="sxs-lookup"><span data-stu-id="0557c-104">In the navigation pane on the left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="0557c-105">오류 메시지에서 식별된 구독 선택</span><span class="sxs-lookup"><span data-stu-id="0557c-105">Select the subscription identified in the error message</span></span>
3.  <span data-ttu-id="0557c-106">*리소스 공급자* 클릭</span><span class="sxs-lookup"><span data-stu-id="0557c-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="0557c-107">*Microsoft.insights* 공급자 찾기</span><span class="sxs-lookup"><span data-stu-id="0557c-107">Find the *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="0557c-108">*등록* 링크 클릭</span><span class="sxs-lookup"><span data-stu-id="0557c-108">Click the *Register* link</span></span>

![Microsoft.insights 리소스 공급자 등록](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="0557c-110">*Microsoft.insights* 리소스 공급자가 등록되면 진단 구성을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="0557c-110">Once the *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="0557c-111">PowerShell에서 다음과 같은 오류 메시지가 나타나면 PowerShell의 버전을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0557c-111">In PowerShell, if you receive the following error message, you need to update your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="0557c-112">PowerShell의 버전을 2016년 11월(v2.3.0)로 업데이트하거나 나중에 [Azure PowerShell cmdlet 시작](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) 문서의 지침을 사용하여 릴리스합니다.</span><span class="sxs-lookup"><span data-stu-id="0557c-112">Update your version of PowerShell to the November 2016 (v2.3.0), or later, release using the instructions in the [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
