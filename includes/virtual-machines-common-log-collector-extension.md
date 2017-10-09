
Microsoft Azure 클라우드 서비스의 문제 진단 필요 hello 문제가 발생 하는 대로 가상 컴퓨터에서 hello 서비스의 로그 파일을 수집 합니다. 요청 시 AzureLogCollector 확장 hello tooperfom 일회성 원격으로 로그온 하지 않고도 – 하나 이상의 클라우드 서비스 Vm (웹 역할 및 작업자 역할) 및 전송 수집 hello 파일 tooan Azure 저장소 계정에서 로그 수집을 사용할 수 있습니다. hello Vm의 tooany 합니다.

> [!NOTE]
> 대부분의 hello 기록 정보에 대 한 설명은 http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp에서 찾을 수 있습니다.
> 
> 

Hello 유형의 파일 toobe 수집에 종속는 컬렉션의 두 가지 모드가 있습니다.

* Azure 게스트 에이전트만 로그(GA). 이 컬렉션 모드는 모든 hello 로그 관련된 tooAzure 게스트 에이전트 및 기타 Azure 구성 요소를 포함합니다.
* 모든 로그(전체). 이 컬렉션 모드는 GA 모드에서 모든 파일을 수집합니다. 또한 다음을 수집합니다.
  
  * 시스템 및 응용 프로그램 이벤트 로그
  * HTTP 오류 로그
  * IIS 로그
  * 설정 로그
  * 기타 시스템 로그

두 컬렉션 모드에서 추가 데이터 수집 폴더 구조를 다음 hello의 컬렉션을 사용 하 여 지정할 수 있습니다.

* **이름**: 수집 hello 이름 hello hello zip 파일 toobe 내의 하위 폴더 이름으로 사용 되는 hello 컬렉션입니다.
* **위치**: hello 경로 toohello 폴더에 hello 가상 컴퓨터 파일에 수집 됩니다.
* **SearchPattern**: hello 패턴의 파일 toobe hello 이름 수집 합니다. 기본값은 “*”입니다.
* **재귀**: 경우 hello 파일 hello 폴더 아래에 재귀적으로 수집할지 됩니다.

## <a name="prerequisites"></a>필수 조건
* 확장 toosave 생성 된 zip 파일에 대 한 저장소 계정을 toohave를 해야합니다.
* Azure PowerShell Cmdlets V0.8.0 이상을 사용하고 있는지 확인해야 합니다. 자세한 내용은 [Azure 다운로드](https://azure.microsoft.com/downloads/)를 참조하세요.

## <a name="add-hello-extension"></a>Hello 확장 추가
사용할 수 있습니다 [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlet 또는 [서비스 관리 REST Api](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector 확장 합니다.

클라우드 서비스에 대 한 기존 Azure Powershell cmdlet을 hello **Set-azureserviceextension**, 클라우드 서비스 역할 인스턴스에서 사용 되는 tooenable hello 확장 될 수 있습니다. 이 확장은이 cmdlet을 통해 사용 하도록 설정 될 때마다 선택 된 역할의 선택 된 hello 역할 인스턴스에서 로그 수집이 트리거됩니다.

가상 컴퓨터에 대 한 기존 Azure Powershell cmdlet을 hello **Set-azurevmextension**, 가상 컴퓨터에서 사용 되는 tooenable hello 확장 될 수 있습니다. 이 확장 hello cmdlet을 통해 사용 하도록 설정 될 때마다 각 인스턴스에서 로그 수집이 트리거됩니다.

내부적으로이 확장 프로그램에서는 hello PublicConfiguration JSON 기반 및 PrivateConfiguration 합니다. hello 다음은 공용 및 개인 구성에 대 한 샘플 JSON의 hello 레이아웃입니다.

### <a name="publicconfiguration"></a>PublicConfiguration
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a>PrivateConfiguration
    {

    }

> [!NOTE]
> 이 확장은 **privateConfiguration**이 필요하지 않습니다. Hello에 대 한 빈 구조를 제공 하기만 하면 **– PrivateConfiguration** 인수입니다.
> 
> 

Hello 2 중 하나를 따라 다음 단계 tooadd hello AzureLogCollector tooone 또는 클라우드 서비스 또는 가상 컴퓨터는 컬렉션에 각 VM toorun hello 트리거와 tooAzure 계정 hello 수집 된 파일을 보낼 선택 된 역할의 인스턴스 지정 합니다.

## <a name="adding-as-a-service-extension"></a>서비스 확장으로 추가
1. Hello 지침 tooconnect Azure PowerShell tooyour 구독을 따릅니다.
2. Hello 서비스 이름, 슬롯, 역할 및 역할 인스턴스 toowhich tooadd 원하는 하 고 hello AzureLogCollector 확장을 사용 하도록 지정 합니다.
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. 파일을 수집 하는 hello 추가 데이터 폴더를 지정 (이 단계는 선택 사항).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > 토큰을 사용할 수 있습니다 `%roleroot%` 고정된 드라이브를 사용 하지 않으므로 toospecify hello 역할 루트 드라이브입니다.
   > 
   > 
4. Hello Azure 저장소 계정 이름 및 키 toowhich 수집 된 파일은 업로드를 제공 합니다.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. 클라우드 서비스에 대 한 다음과 tooenable hello AzureLogCollector 확장으로 hello SetAzureServiceLogCollector.ps1 (hello 문서의 hello 끝에 포함 됨)를 호출 합니다. Hello 실행이 완료 되 면 아래에 업로드 하는 hello 파일을 찾을 수 있습니다.`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

hello 다음은 hello 정의 toohello 스크립트를 전달 하는 hello 매개 변수입니다. (아래에 복사됩니다.)

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* *ServiceName*: 클라우드 서비스 이름입니다.
* *역할*: "WebRole1" 또는 "WorkerRole1"과 같은 역할 목록입니다.
* *인스턴스*: 역할 인스턴스의 hello 이름의 목록을 쉼표로 구분 된 와일드 카드 문자열 hello를 사용 하세요 ("*") 모든 역할 인스턴스에 대 한 합니다.
* *슬롯*: 슬롯 이름입니다. “프로덕션” 또는 “스테이징”입니다.
* *모드*: 컬렉션 모드입니다. "Full" 또는 "GA"입니다.
* *StorageAccountName*: 수집된 데이터를 저장하기 위한 Azure 저장소 계정의 이름입니다.
* *StorageAccountKey*: Azure 저장소 계정 키의 이름입니다.
* *AdditionalDataLocationList*: hello 구조를 다음 목록:
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a>VM 확장으로 추가
Hello 지침 tooconnect Azure PowerShell tooyour 구독을 따릅니다.

1. Hello 서비스 이름, VM 및 hello 컬렉션 모드를 지정 합니다.
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. Hello Azure 저장소 계정 이름 및 키 toowhich 수집 된 파일은 업로드를 제공 합니다.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. 클라우드 서비스에 대 한 다음과 tooenable hello AzureLogCollector 확장으로 hello SetAzureVMLogCollector.ps1 (hello 문서의 hello 끝에 포함 됨)를 호출 합니다. Hello 실행이 완료 되 면 https://YouareStorageAccountName.blob.core.windows.net/vmlogs hello 업로드 파일을 찾을 수 있습니다.

hello 다음은 hello 정의 toohello 스크립트를 전달 하는 hello 매개 변수입니다. (아래에 복사됩니다.)

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* ServiceName: 클라우드 서비스 이름입니다.
* Hello VM의 VMName hello 이름입니다.
* 모드: 컬렉션 모드입니다. "Full" 또는 "GA"입니다.
* StorageAccountName: 수집된 데이터를 저장하기 위한 Azure 저장소 계정의 이름입니다.
* StorageAccountKey: Azure 저장소 계정 키의 이름입니다.
* AdditionalDataLocationList: hello 구조를 다음에는 목록:

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a>확장 PowerShell 스크립트 파일
SetAzureServiceLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


SetAzureVMLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a>다음 단계
이제 매우 간단한 위치에서 로그를 검사하거나 복사할 수 있습니다.

