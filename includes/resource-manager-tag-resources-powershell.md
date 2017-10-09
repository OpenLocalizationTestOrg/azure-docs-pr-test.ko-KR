태그와 작동 하는 방식에 중요 한 변경을 포함 하는 hello AzureRm.Resources 모듈의 버전 3.0. 계속하기 전에 버전을 확인하세요.

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

3.0 이상 버전을 표시 하는 결과이 항목의 예제 hello 환경과 함께 작동 합니다. 버전 3.0 이상이 없을 경우 이 항목을 진행하기 전에 PowerShell 갤러리 또는 웹 플랫폼 설치 관리자를 사용하여 [버전을 업데이트](/powershell/azureps-cmdlets-docs/)합니다.

```powershell
Version
-------
3.5.0
```

toosee hello에 대 한 기존 태그는 *리소스 그룹*를 사용 하 여:

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

해당 스크립트에는 형식에 따라 hello 반환 합니다.

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

toosee hello에 대 한 기존 태그는 *를 지정 된 리소스 ID를 갖는 리소스*를 사용 하 여:

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

또는 toosee hello에 대 한 기존 태그는 *지정된 된 이름 및 리소스 그룹에 있는 리소스*를 사용 하 여:

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

tooget *특정 태그가 있는 리소스 그룹을*를 사용 하 여:

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

tooget *특정 태그를 포함 하는 리소스가*를 사용 하 여:

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

태그 tooa 리소스 또는 리소스 그룹을 적용할 때마다 해당 리소스 또는 리소스 그룹에 기존 태그 hello 덮어씁니다. 따라서 hello 리소스 또는 리소스 그룹에 기존 태그에 있는지 여부에 따라 다른 방법을 사용 해야 합니다. 

tooadd 태그 tooa *기존 태그 없이 리소스 그룹*를 사용 하 여:

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

tooadd 태그 tooa *기존 태그에 있는 리소스 그룹*hello 기존 태그, hello 새 태그를 추가 하 고 검색 hello 태그 다시 적용 합니다.

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

tooadd 태그 tooa *기존 태그 없이 리소스*를 사용 하 여:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooadd 태그 tooa *기존 태그에 있는 리소스*를 사용 하 여:

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooapply 모든 리소스 그룹 tooits 리소스에서 태그를 삽입 하 고 *hello 리소스에 대 한 기존 태그를 유지 하지*, 다음 스크립트는 hello를 사용 하 여:

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

tooapply 모든 리소스 그룹 tooits 리소스에서 태그를 삽입 하 고 *중복 되지 않는 리소스에 대 한 기존 태그 유지*, 다음 스크립트는 hello를 사용 하 여:

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

tooremove 모든 태그는 빈 해시 테이블을 전달 합니다.

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



