## <a name="overview"></a><span data-ttu-id="669f2-101">개요</span><span class="sxs-lookup"><span data-stu-id="669f2-101">Overview</span></span>
<span data-ttu-id="669f2-102">[Azure 마켓플레이스](https://azure.microsoft.com/marketplace/)의 이미지를 배포하여 리소스 그룹에 새 가상 컴퓨터(VM)를 만드는 경우 기본 OS 드라이브는 127GB입니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), the default OS drive is 127 GB.</span></span> <span data-ttu-id="669f2-103">VM에 데이터 디스크를 추가할 수 있고(선택한 SKU에 따라 추가할 수 있는 양이 달라짐) 응용 프로그램 및 CPU 사용량이 많은 워크로드는 이러한 추가 디스크에 설치하는 것이 좋지만, 고객이 다음과 같은 특정 시나리오를 지원하기 위해 OS 드라이브를 확장해야 하는 경우가 자주 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-103">Even though it’s possible to add data disks to the VM (how many depending upon the SKU you’ve chosen) and moreover it’s recommended to install applications and CPU intensive workloads on these addendum disks, oftentimes customers need to expand the OS drive to support certain scenarios such as following:</span></span>

1. <span data-ttu-id="669f2-104">OS 드라이브에 구성 요소를 설치하는 기존 응용 프로그램을 지원하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="669f2-105">OS 드라이브가 더 큰 온-프레미스로 실제 PC 또는 가상 컴퓨터를 마이그레이션하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="669f2-106">Azure는 리소스를 만들고 작업하기 위한 두 가지 배포 모델로 리소스 관리자와 클래식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="669f2-107">이 문서에서는 리소스 관리자 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-107">This article covers using the Resource Manager model.</span></span> <span data-ttu-id="669f2-108">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

## <a name="resize-the-os-drive"></a><span data-ttu-id="669f2-109">OS 드라이브 크기 조정</span><span class="sxs-lookup"><span data-stu-id="669f2-109">Resize the OS drive</span></span>
<span data-ttu-id="669f2-110">이 문서에서는 [Azure Powershell](/powershell/azureps-cmdlets-docs)의 리소스 관리자 모듈을 사용하여 OS 드라이브의 크기를 조정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-110">In this article we’ll accomplish the task of resizing the OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="669f2-111">관리 모드에서 Powershell ISE 또는 Powershell 창을 열고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-111">Open your Powershell ISE or Powershell window in administrative mode and follow the steps below:</span></span>

1. <span data-ttu-id="669f2-112">리소스 관리 모드에서 Microsoft Azure 계정에 로그인하고 다음과 같이 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-112">Sign-in to your Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="669f2-113">다음과 같이 리소스 그룹 이름 및 VM 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="669f2-114">다음과 같이 VM에 대한 참조를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-114">Obtain a reference to your VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="669f2-115">다음과 같이 VM을 중지한 후 디스크의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-115">Stop the VM before resizing the disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="669f2-116">드디어 기다리던 순간이 왔습니다!</span><span class="sxs-lookup"><span data-stu-id="669f2-116">And here comes the moment we’ve been waiting for!</span></span> <span data-ttu-id="669f2-117">다음과 같이 OS 디스크의 크기를 원하는 값으로 설정하고 VM을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-117">Set the size of the OS disk to the desired value and update the VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="669f2-118">새 크기가 기존 디스크 크기보다 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-118">The new size should be greater than the existing disk size.</span></span> <span data-ttu-id="669f2-119">허용되는 최대 크기는 1023GB입니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-119">The maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="669f2-120">VM이 업데이트될 때까지 몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-120">Updating the VM may take a few seconds.</span></span> <span data-ttu-id="669f2-121">명령 실행이 완료되면 다음과 같이 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-121">Once the command finishes executing, restart the VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="669f2-122">이것으로 끝입니다!</span><span class="sxs-lookup"><span data-stu-id="669f2-122">And that’s it!</span></span> <span data-ttu-id="669f2-123">이제 VM에 RDP를 실행하고, 컴퓨터 관리(또는 디스크 관리)를 열고, 새로 할당된 공간을 사용하여 드라이브를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-123">Now RDP into the VM, open Computer Management (or Disk Management) and expand the drive using the newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="669f2-124">요약</span><span class="sxs-lookup"><span data-stu-id="669f2-124">Summary</span></span>
<span data-ttu-id="669f2-125">이 문서에서는 Powershell의 Azure Resource Manager 모듈을 사용하여 IaaS 가상 컴퓨터의 OS 드라이브를 확장했습니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-125">In this article, we used Azure Resource Manager modules of Powershell to expand the OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="669f2-126">참조하실 수 있도록 아래에 전체 스크립트를 다시 작성해 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-126">Reproduced below is the complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="669f2-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="669f2-127">Next Steps</span></span>
<span data-ttu-id="669f2-128">이 문서에서는 VM의 OS 디스크를 확장하는 방법에 초점을 두었지만, 작성한 스크립트에서 코드 한 줄만 변경하면 VM에 연결된 데이터 디스크를 확장하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-128">Though in this article, we focused primarily on expanding the OS disk of the VM, the developed script may also be used for expanding the data disks attached to the VM by changing a single line of code.</span></span> <span data-ttu-id="669f2-129">예를 들어 VM에 연결된 첫 번째 데이터 디스크를 확장하려면 아래와 같이 ```StorageProfile```의 ```OSDisk``` 개체를 ```DataDisks``` 배열로 바꾸고 숫자 인덱스를 사용하여 첫 번째 연결된 데이터 디스크의 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-129">For example, to expand the first data disk attached to the VM, replace the ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index to obtain a reference to first attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="669f2-130">마찬가지로, 위와 같이 인덱스를 사용하여 또는 아래와 같이 디스크의 ```Name``` 속성을 사용하여 VM에 연결된 다른 데이터 디스크를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669f2-130">Similarly you may reference other data disks attached to the VM, either by using an index as shown above or the ```Name``` property of the disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="669f2-131">Azure Resource Manager VM에 디스크를 연결하는 방법은 이 [문서](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="669f2-131">If you want to find out how to attach disks to an Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

