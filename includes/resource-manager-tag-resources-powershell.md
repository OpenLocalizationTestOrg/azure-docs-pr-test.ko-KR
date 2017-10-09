<span data-ttu-id="f5ca4-101">태그와 작동 하는 방식에 중요 한 변경을 포함 하는 hello AzureRm.Resources 모듈의 버전 3.0.</span><span class="sxs-lookup"><span data-stu-id="f5ca4-101">Version 3.0 of hello AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="f5ca4-102">계속하기 전에 버전을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f5ca4-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="f5ca4-103">3.0 이상 버전을 표시 하는 결과이 항목의 예제 hello 환경과 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ca4-103">If your results show version 3.0 or later, hello examples in this topic work with your environment.</span></span> <span data-ttu-id="f5ca4-104">버전 3.0 이상이 없을 경우 이 항목을 진행하기 전에 PowerShell 갤러리 또는 웹 플랫폼 설치 관리자를 사용하여 [버전을 업데이트](/powershell/azureps-cmdlets-docs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ca4-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="f5ca4-105">toosee hello에 대 한 기존 태그는 *리소스 그룹*를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f5ca4-105">toosee hello existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="f5ca4-106">해당 스크립트에는 형식에 따라 hello 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ca4-106">That script returns hello following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="f5ca4-107">toosee hello에 대 한 기존 태그는 *를 지정 된 리소스 ID를 갖는 리소스*를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f5ca4-107">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="f5ca4-108">또는 toosee hello에 대 한 기존 태그는 *지정된 된 이름 및 리소스 그룹에 있는 리소스*를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f5ca4-108">Or, toosee hello existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="f5ca4-109">tooget *특정 태그가 있는 리소스 그룹을*를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f5ca4-109">tooget *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="f5ca4-110">tooget *특정 태그를 포함 하는 리소스가*를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f5ca4-110">tooget *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="f5ca4-111">태그 tooa 리소스 또는 리소스 그룹을 적용할 때마다 해당 리소스 또는 리소스 그룹에 기존 태그 hello 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="f5ca4-111">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="f5ca4-112">따라서 hello 리소스 또는 리소스 그룹에 기존 태그에 있는지 여부에 따라 다른 방법을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ca4-112">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="f5ca4-113">tooadd 태그 tooa *기존 태그 없이 리소스 그룹*를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f5ca4-113">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="f5ca4-114">tooadd 태그 tooa *기존 태그에 있는 리소스 그룹*hello 기존 태그, hello 새 태그를 추가 하 고 검색 hello 태그 다시 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ca4-114">tooadd tags tooa *resource group that has existing tags*, retrieve hello existing tags, add hello new tag, and reapply hello tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="f5ca4-115">tooadd 태그 tooa *기존 태그 없이 리소스*를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f5ca4-115">tooadd tags tooa *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="f5ca4-116">tooadd 태그 tooa *기존 태그에 있는 리소스*를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f5ca4-116">tooadd tags tooa *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="f5ca4-117">tooapply 모든 리소스 그룹 tooits 리소스에서 태그를 삽입 하 고 *hello 리소스에 대 한 기존 태그를 유지 하지*, 다음 스크립트는 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f5ca4-117">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="f5ca4-118">tooapply 모든 리소스 그룹 tooits 리소스에서 태그를 삽입 하 고 *중복 되지 않는 리소스에 대 한 기존 태그 유지*, 다음 스크립트는 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f5ca4-118">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources that are not duplicates*, use hello following script:</span></span>

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

<span data-ttu-id="f5ca4-119">tooremove 모든 태그는 빈 해시 테이블을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ca4-119">tooremove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



