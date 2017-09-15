<span data-ttu-id="13b4d-101">AzureRm.Resources 모듈 버전 3.0에서는 태그 사용 방법이 크게 달라졌습니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-101">Version 3.0 of the AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="13b4d-102">계속하기 전에 버전을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="13b4d-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="13b4d-103">버전이 3.0 이상일 경우 이 항목의 예제가 해당 환경에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-103">If your results show version 3.0 or later, the examples in this topic work with your environment.</span></span> <span data-ttu-id="13b4d-104">버전 3.0 이상이 없을 경우 이 항목을 진행하기 전에 PowerShell 갤러리 또는 웹 플랫폼 설치 관리자를 사용하여 [버전을 업데이트](/powershell/azureps-cmdlets-docs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="13b4d-105">*리소스 그룹*에 대한 기존 태그를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-105">To see the existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="13b4d-106">그러면 스크립트가 다음 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-106">That script returns the following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="13b4d-107">*지정된 리소스 ID를 포함한 리소스*에 대한 기존 태그를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-107">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="13b4d-108">또는 *지정된 이름 및 리소스 그룹을 포함한 리소스*에 대한 기존 태그를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-108">Or, to see the existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="13b4d-109">*특정 태그가 있는 리소스 그룹*을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-109">To get *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="13b4d-110">*특정 태그가 있는 리소스*를 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-110">To get *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="13b4d-111">리소스 또는 리소스 그룹에 태그를 적용할 때마다 해당 리소스 또는 리소스 그룹의 기존 태그가 덮어써집니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-111">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="13b4d-112">따라서 리소스 또는 리소스 그룹에 기존 태그가 있는지에 따라 다른 방법을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-112">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="13b4d-113">*기존 태그를 포함하지 않는 리소스 그룹*에 태그를 추가하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-113">To add tags to a *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="13b4d-114">*기존 태그를 포함하는 리소스 그룹*에 태그를 추가하려면 기존 태그를 검색하고, 새 태그를 추가하고, 태그를 다시 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-114">To add tags to a *resource group that has existing tags*, retrieve the existing tags, add the new tag, and reapply the tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="13b4d-115">*기존 태그를 포함하지 않는 리소스*에 태그를 추가하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-115">To add tags to a *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="13b4d-116">*기존 태그를 포함하는 리소스*에 태그를 추가하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-116">To add tags to a *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="13b4d-117">*리소스의 기존 태그를 유지하지 않고* 리소스 그룹의 모든 태그를 리소스에 적용하려면 다음 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-117">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="13b4d-118">*리소스의 중복되지 않는 기존 태그를 유지하지 않고* 리소스 그룹의 모든 태그를 리소스에 적용하려면 다음 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-118">To apply all tags from a resource group to its resources, and *retain existing tags on resources that are not duplicates*, use the following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="13b4d-119">모든 태그를 제거하려면 빈 해시 테이블을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="13b4d-119">To remove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



