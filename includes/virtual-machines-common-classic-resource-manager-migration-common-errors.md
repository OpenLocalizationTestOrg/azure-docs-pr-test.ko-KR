# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a>클래식 tooAzure 리소스 관리자 마이그레이션 동안 일반적인 오류
이 문서 카탈로그 Azure 클래식 배포 모델 toohello Azure 리소스 관리자 스택에서 IaaS 리소스 hello 마이그레이션하는 동안 가장 일반적인 오류 및 완화 hello 합니다.

## <a name="list-of-errors"></a>오류 목록
| 오류 문자열 | 해결 방법 |
| --- | --- |
| 내부 서버 오류 |어떤 경우에는 다시 시도하면 사라지는 일시적인 오류입니다. Toopersist, 계속 진행 하는 경우 [Azure 지원에 문의](../articles/azure-supportability/how-to-create-azure-support-request.md) 플랫폼 로그에 대 한 확인을 요구 합니다. <br><br> **참고:** hello 인시던트는 hello 지원 팀에서 추적 되 면 마십시오 된 자체 마이그레이션을이 할 수 있습니다 하는 대로 사용자 환경에서 의도 하지 않은 결과입니다. |
| 마이그레이션은 PaaS 배포(웹/작업자)이기 때문에 HostedService {hosted-service-name}에서 배포 {deployment-name}에 지원되지 않습니다. |배포가 웹/작업자 역할을 포함하는 경우에 발생합니다. 마이그레이션은 가상 컴퓨터에만 지원 하므로 hello 웹/작업자 역할 hello 배포에서 제거 하 고 마이그레이션을 다시 시도 하십시오. |
| 템플릿 {template-name} 배포에 실패했습니다. CorrelationId={guid} |마이그레이션 서비스의 hello 백 엔드에 hello Azure 리소스 관리자 스택에서 Azure 리소스 관리자 템플릿 toocreate 리소스를 사용 했습니다. 템플릿 idempotent 이므로 일반적으로 안전 하 게 다시 시도할 수 있습니다이 오류가 나타나면 hello 마이그레이션 작업 tooget 합니다. 이 오류가 계속 발생 toopersist 경우 [Azure 지원에 문의](../articles/azure-supportability/how-to-create-azure-support-request.md) hello 상관 관계 Id를 지정 합니다. <br><br> **참고:** hello 인시던트는 hello 지원 팀에서 추적 되 면 마십시오 된 자체 마이그레이션을이 할 수 있습니다 하는 대로 사용자 환경에서 의도 하지 않은 결과입니다. |
| hello 가상 네트워크 {가상 네트워크 이름 간} 존재 하지 않습니다. |이 hello 새 Azure 포털에 hello 가상 네트워크를 만든 경우 발생할 수 있습니다. hello 실제 가상 네트워크 이름 hello 패턴을 따르는 "그룹 * <VNET name>" |
| HostedService {hosted-service-name}에서 VM {vm-name}에는 Azure Resource Manager에서 지원되지 않는 확장 {extension-name}이 포함되어 있습니다. Toouninstall 좋습니다 마이그레이션을 사용 하 여 계속 하기 전에 VM hello 옵니다. |BGInfo 1.*과 같은 XML 확장은 Azure Resource Manager에서 지원되지 않습니다. 따라서 이러한 확장을 마이그레이션할 수 없습니다. 이러한 확장은 가상 컴퓨터에 설치 된 hello 왼쪽된을 하는 경우는 hello 마이그레이션을 완료 하기 전에 자동으로 제거 됩니다. |
| HostedService {hosted-service-name}에서 VM {vm-name}은 현재 마이그레이션에 지원되지 않는 VMSnapshot/VMSnapshotLinux 확장을 포함합니다. Hello VM에서에서 제거 하 고 hello 마이그레이션이 완료 된 후 Azure 리소스 관리자를 사용 하 여 다시 추가 |Azure 백업에 대 한 hello 가상 컴퓨터 구성 되어 있는 hello 시나리오입니다. Https://aka.ms/vmbackupmigration에 hello 해결 방법 따라 이므로 현재 지원 되지 않는 시나리오 |
| HostedService {호스팅된 서비스-이름}에서 {vm name} VM 확장 {확장 이름} 상태 hello VM에서에서 보고 되지 않습니다 포함 되어 있습니다. 따라서 이 VM은 마이그레이션할 수 없습니다. 보고 되 고 해당 hello 확장 상태를 확인 하거나 hello 확장 hello VM에서에서 제거한 마이그레이션을 다시 시도 하세요. <br><br> HostedService {hosted-service-name}에서 VM {vm-name}에는 확장 {extension-name} 보고 처리기 상태 {handler-status}가 포함되어 있습니다. 따라서 VM hello 마이그레이션할 수 없습니다. Hello 확장 처리기 상태 보고 되 고 {처리기 status} 있는지 확인 하거나 hello VM에서에서 제거 하 고 마이그레이션을 다시 시도 하세요. <br><br> HostedService {호스팅된 서비스-이름}에서 {vm name} VM 용 VM 에이전트가 보고 하는 hello 전반적인 에이전트 상태를 준비 되지 않았습니다. 따라서 VM hello 마이그레이션할 수 없습니다, 문서가 마이그레이션할 확장명입니다. VM 에이전트는 hello Ready로 전체 에이전트 상태를 보고 확인 합니다. Toohttps://aka.ms/classiciaasmigrationfaqs를 참조 하십시오. |Azure 게스트 에이전트 및 VM 확장의 상태 아웃 바운드 인터넷 액세스 toohello VM 저장소 계정 toopopulate 필요합니다. 상태 실패의 일반적인 원인은 다음과 같습니다. <li> toohello 아웃 바운드 액세스를 차단 하는 네트워크 보안 그룹 인터넷 <li> Hello VNET에 온-프레미스 DNS 서버 및 DNS 연결 손실 됩니다. <br><br> Toosee 지원 되지 않는 상태를 계속 진행 하면이 검사 hello 확장 tooskip를 제거 하 고 마이그레이션을 사용 하 여 앞으로 진행할 수 있습니다. |
| 마이그레이션에는 여러 가용성 집합이 있기 때문에 HostedService {hosted-service-name}에서 배포 {deployment-name}에 지원되지 않습니다. |현재, 1 이하의 가용성 집합을 가진 호스티드 서비스만 마이그레이션할 수 있습니다. 이 문제를 해결 toowork 가용성 집합 및 다른 가용성 집합 tooa 해당 가상 컴퓨터 호스 티 드 서비스에 추가 하는 hello를 이동 하십시오. |
| HostedService의 {배포 이름} 배포에 대 한 마이그레이션이 지원 되지 않습니다 {호스트-서비스-이름 hello HostedService 하나를 포함 하는 경우에 hello 가용성 집합의 일부가 아닌 Vm에 있기 때문입니다. |이 시나리오에 대 한 hello 해결은 tooeither 이동 단일 가용성에 모든 hello 가상 컴퓨터 설정 또는 hello hello 호스팅된 서비스의 가용성 집합에서 모든 가상 컴퓨터를 제거 합니다. |
| 저장소 계정/HostedService/가상 네트워크 {가상 네트워크 이름 간}는 마이그레이션 중 hello 프로세스 중에서 이므로 이므로 변경할 수 없습니다. |이 오류는 hello 리소스에 hello "준비" 마이그레이션 작업이 완료 되 고 toohello 리소스를 변경 하는 작업이 트리거될 때 발생 합니다. "준비" 작업 후 hello 관리 평면에 hello 잠금 때문에 모든 변경 내용을 toohello 리소스 차단 됩니다. toounlock hello 관리 평면 hello "커밋" 마이그레이션 작업 toocomplete 마이그레이션 실행할 수 있습니다 또는 hello "중단" 마이그레이션 작업 tooroll 다시 hello "준비" 작업 합니다. |
| RoleStateUnknown 상태인 VM {vm-name}이 있기 때문에 HostedService {hosted-service-name}에 대한 마이그레이션이 허용되지 않습니다. 만 hello hello 다음 중 하나에 VM이 상태는 경우-실행 중, 중지 됨, 할당 취소 중지에서는 마이그레이션이 허용 됩니다. |hello VM 수 모드로 전환 hello HostedService 다시 부팅 등의 업데이트 작업 중 때 일반적으로 수행 됨 상태 전환을 통해 확장 등을 설치 합니다. 마이그레이션을 시도 하기 전에 hello HostedService에 업데이트 작업이 toocomplete hello에 대 한이 좋습니다. |
| HostedService {호스팅된 서비스-이름}의 {배포 이름} 배포 인 물리적 blob 크기 {size-of-the-vhd-blob-backing-the-data-disk} 바이트 hello VM 데이터 디스크가 논리적 크기 {와 일치 하지 않습니다 데이터 디스크 {데이터 디스크 이름}와 {vm name}는 VM이 포함 size-of-the-data-disk-specified-in-the-vm-api} 바이트 수입니다. 마이그레이션은 hello Azure 리소스 관리자 VM에 대 한 hello 데이터 디스크에 대 한 크기를 지정 하지 않고 계속 진행 됩니다. | 이 오류는 hello VM API 모델의 hello 크기를 업데이트 하지 않고 hello VHD blob 크기를 조정할 경우 발생 합니다. 자세한 마이그레이션 단계는 [다음](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes)과 같습니다.|
| 클라우드 서비스 {클라우드 서비스 이름}에서 {VM 이름} VM에 대해 미디어 링크 {데이터 디스크 URI}를 사용하여 데이터 디스크 {데이터 디스크 이름}에 대해 유효성 검사를 수행하는 동안 저장소 예외가 발생합니다. 해당 hello VHD 미디어 링크는이 가상 컴퓨터에 액세스할 수 있는지 확인 하십시오 | 이 오류는 hello의 hello 디스크 VM 삭제 되었거나 더 이상 액세스할 수 없는 경우에 발생할 수 있습니다. VM이 존재 하는 hello에 대 한 hello 디스크가 있는지 확인 하십시오.|
| HostedService {cloud-service-name}의 VM {vm-name}에는 Azure Resource Manager에서 지원되지 않는 BLOB 이름 {vhd-blob-name}의 MediaLink {vhd-uri}가 있는 디스크가 포함되어 있습니다. | Hello blob의 hello 이름에는 "/"를 현재 계산 리소스 공급자에서 지원 되지 않는 것이 오류가 발생 합니다. |
| 가 hello 지역 범위에 속하지 않으므로 HostedService {클라우드 서비스 이름}의 {배포 이름} 배포에 대 한 마이그레이션이 허용 되지 않습니다. 이 배포 tooregional 범위를 이동 하기 위한 toohttp://aka.ms/regionalscope를 참조 하십시오. | 2014에서 Azure는 네트워킹 리소스에서에서 이동 합니다. 클러스터 수준 범위 tooregional 범위를 발표 했습니다. 자세한 내용은 [http://aka.ms/regionalscope]를 참조하세요(http://aka.ms/regionalscope). 이 오류는 마이그레이션되는 hello 배포 하지 않았습니다. 업데이트 작업을 자동으로 tooa 지역 범위로 이동 하는 경우에 발생 합니다. 최상의 방법은 tooeither 끝점 tooa VM을 추가 하거나 데이터는 toohello VM 디스크와 다음 마이그레이션을 다시 시도 합니다. <br> 참조 [어떻게 azure에서 클래식 Windows 가상 컴퓨터 끝점을 tooset](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) 또는 [hello 클래식 배포 모델을 사용 하 여 만든 데이터 디스크 tooa Windows 가상 컴퓨터를 연결 합니다.](../articles/virtual-machines/windows/classic/attach-disk.md)|


## <a name="detailed-mitigations"></a>자세한 마이그레이션

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a>데이터 디스크를 물리적 blob 크기 (바이트)를 사용 하 여 VM hello VM 데이터 디스크가 논리적 크기 (바이트)을 일치 하지 않습니다.

이 hello 데이터 디스크의 논리 크기를 가져올 수 hello 실제 VHD blob 크기와 동기화 하는 경우 발생 합니다. 이 쉽게 확인할 수 hello 다음 명령을 사용 하 여:

#### <a name="verifying-hello-issue"></a>Hello 문제를 확인 하는 중

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a>Hello 문제를 완화합니다.

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a>마이그레이션을 완료 한 후 VM tooa 다른 구독 이동

Hello 마이그레이션 프로세스를 완료 한 후 toomove hello VM tooanother 구독을 할 수 있습니다. 그러나 암호/인증서에 있는 경우 참조 하는 주요 자격 증명 모음 리소스 hello VM 이동 hello 현재 지원 되지 않습니다. 아래 지침 hello tooworkaround hello 문제를 수 있습니다. 

#### <a name="powershell"></a>PowerShell
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a>Azure CLI 2.0

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
