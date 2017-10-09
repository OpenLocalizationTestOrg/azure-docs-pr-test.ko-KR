## <a name="overview"></a><span data-ttu-id="1315f-101">개요</span><span class="sxs-lookup"><span data-stu-id="1315f-101">Overview</span></span>
<span data-ttu-id="1315f-102">이미지를 배포 하 여 리소스 그룹에 새 가상 컴퓨터 (VM)을 만들 하는 때 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/), hello 기본 운영 체제 드라이브는 127GB입니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), hello default OS drive is 127 GB.</span></span> <span data-ttu-id="1315f-103">가능한 tooadd 데이터 디스크 toohello (hello SKU에 개수 따라 사용자가 선택한) VM 이며 또한도 권장된 tooinstall 응용 프로그램 및 추 록 디스크에 CPU 집약적인 작업을 하는 경우에 종종의 고객이 원하는 tooexpand hello OS 다음과 같은 특정 시나리오 toosupport 드라이브:</span><span class="sxs-lookup"><span data-stu-id="1315f-103">Even though it’s possible tooadd data disks toohello VM (how many depending upon hello SKU you’ve chosen) and moreover it’s recommended tooinstall applications and CPU intensive workloads on these addendum disks, oftentimes customers need tooexpand hello OS drive toosupport certain scenarios such as following:</span></span>

1. <span data-ttu-id="1315f-104">OS 드라이브에 구성 요소를 설치하는 기존 응용 프로그램을 지원하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="1315f-105">OS 드라이브가 더 큰 온-프레미스로 실제 PC 또는 가상 컴퓨터를 마이그레이션하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1315f-106">Azure는 리소스를 만들고 작업하기 위한 두 가지 배포 모델로 리소스 관리자와 클래식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="1315f-107">이 문서에서는 hello 리소스 관리자 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-107">This article covers using hello Resource Manager model.</span></span> <span data-ttu-id="1315f-108">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

## <a name="resize-hello-os-drive"></a><span data-ttu-id="1315f-109">Hello 운영 체제 드라이브의 크기를 조정합니다</span><span class="sxs-lookup"><span data-stu-id="1315f-109">Resize hello OS drive</span></span>
<span data-ttu-id="1315f-110">이 문서에서는의 리소스 관리자 모듈을 사용 하 여 hello 운영 체제 드라이브를 크기 조정 hello 작업을 수행 합니다 [Azure Powershell](/powershell/azureps-cmdlets-docs)합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-110">In this article we’ll accomplish hello task of resizing hello OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="1315f-111">관리 모드에서 Powershell ISE 또는 Powershell 창을 열고 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-111">Open your Powershell ISE or Powershell window in administrative mode and follow hello steps below:</span></span>

1. <span data-ttu-id="1315f-112">로그인 tooyour Microsoft Azure 리소스 관리 모드에서 계정 및 구독을 다음과 같이 선택:</span><span class="sxs-lookup"><span data-stu-id="1315f-112">Sign-in tooyour Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="1315f-113">다음과 같이 리소스 그룹 이름 및 VM 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="1315f-114">다음과 같이 참조 tooyour를 VM을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-114">Obtain a reference tooyour VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="1315f-115">다음과 같이 hello 디스크의 크기를 조정 하기 전에 hello VM을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-115">Stop hello VM before resizing hello disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="1315f-116">및 여기에서는 왔습니다 hello 순간에!</span><span class="sxs-lookup"><span data-stu-id="1315f-116">And here comes hello moment we’ve been waiting for!</span></span> <span data-ttu-id="1315f-117">Hello 크기 hello OS 디스크 toohello 원하는 값을 설정 하 고 hello VM을 다음과 같이 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-117">Set hello size of hello OS disk toohello desired value and update hello VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="1315f-118">hello 새 크기 hello 기존 디스크 크기 보다 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-118">hello new size should be greater than hello existing disk size.</span></span> <span data-ttu-id="1315f-119">최대 허용 hello 1,023 GB입니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-119">hello maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="1315f-120">업데이트 hello VM에는 몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-120">Updating hello VM may take a few seconds.</span></span> <span data-ttu-id="1315f-121">Hello 명령이 완료 되 면 실행 되 면 다음과 같이 hello VM 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-121">Once hello command finishes executing, restart hello VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="1315f-122">이것으로 끝입니다!</span><span class="sxs-lookup"><span data-stu-id="1315f-122">And that’s it!</span></span> <span data-ttu-id="1315f-123">VM hello에 RDP 이제 컴퓨터 관리 (또는 디스크 관리) 열고 새로 할당 된 공간 hello를 사용 하 여 hello 드라이브를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-123">Now RDP into hello VM, open Computer Management (or Disk Management) and expand hello drive using hello newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="1315f-124">요약</span><span class="sxs-lookup"><span data-stu-id="1315f-124">Summary</span></span>
<span data-ttu-id="1315f-125">이 문서에서는 Powershell tooexpand hello IaaS 가상 컴퓨터의 운영 체제 드라이브의 Azure 리소스 관리자 모듈을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-125">In this article, we used Azure Resource Manager modules of Powershell tooexpand hello OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="1315f-126">아래 재현 하는 것은 hello 전체 스크립트 참조용입니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-126">Reproduced below is hello complete script for your reference:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1315f-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1315f-127">Next Steps</span></span>
<span data-ttu-id="1315f-128">이 문서에서는 확장 hello VM의 OS hello 디스크에 주로 집중, 있지만 hello 개발 된 스크립트 사용할 수도 있습니다 코드 한 줄을 변경 하 여 hello 데이터 디스크가 연결 된 toohello VM 확장을 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-128">Though in this article, we focused primarily on expanding hello OS disk of hello VM, hello developed script may also be used for expanding hello data disks attached toohello VM by changing a single line of code.</span></span> <span data-ttu-id="1315f-129">예를 들어 tooexpand hello 첫 번째 데이터 연결 된 toohello VM 디스크, hello 대체 ```OSDisk``` 개체의 ```StorageProfile``` 와 ```DataDisks``` 배열 하 고 아래와 같이 숫자 인덱스 tooobtain 참조 toofirst 연결 된 데이터 디스크를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="1315f-129">For example, tooexpand hello first data disk attached toohello VM, replace hello ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index tooobtain a reference toofirst attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="1315f-130">마찬가지로 다른 데이터 디스크 연결 된 toohello 위와 같이 인덱스를 사용 하 여 VM을 참조할 수도 있습니다 hello ```Name``` 아래 그림과 같이 hello 디스크의 속성:</span><span class="sxs-lookup"><span data-stu-id="1315f-130">Similarly you may reference other data disks attached toohello VM, either by using an index as shown above or hello ```Name``` property of hello disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="1315f-131">Toofind tooattach tooan Azure 리소스 관리자 VM 디스크를 어떻게 아웃 하려는 경우이 옵션을 선택 [문서](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="1315f-131">If you want toofind out how tooattach disks tooan Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

