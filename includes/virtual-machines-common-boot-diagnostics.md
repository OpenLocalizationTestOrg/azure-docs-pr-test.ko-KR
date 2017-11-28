<span data-ttu-id="90f1d-101">이제 Azure에서 두 가지 디버깅 기능에 대한 지원이 제공됩니다. Azure Virtual Machines Resource Manager 배포 모델에 대한 콘솔 출력 및 스크린샷 지원.</span><span class="sxs-lookup"><span data-stu-id="90f1d-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="90f1d-102">자신의 이미지를 Azure로 가져 오거나 플랫폼 이미지 중 하나를 부팅 할 때 Virtual Machines가 부팅 불가능한 상태가 되는 데에는 많은 이유가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-102">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="90f1d-103">이 기능을 사용하면 부팅 오류에서 Virtual Machines를 쉽게 진단하고 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-103">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="90f1d-104">Linux Virtual Machines의 경우 포털에서 콘솔 로그의 출력을 쉽게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-104">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Azure Portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="90f1d-106">그러나 Windows 및 Linux Virtual Machines의 경우 Azure를 사용하면 하이퍼바이저에서 VM의 스크린샷을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-106">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![오류](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="90f1d-108">이 두 가지 기능이 모든 지역의 Azure Virtual Machines에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="90f1d-109">참고로, 스크린샷 및 출력을 저장소 계정에 표시하는 데 최대 10분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-109">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="90f1d-110">일반적인 부팅 오류</span><span class="sxs-lookup"><span data-stu-id="90f1d-110">Common boot errors</span></span>

- [<span data-ttu-id="90f1d-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="90f1d-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="90f1d-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="90f1d-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="90f1d-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="90f1d-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="90f1d-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="90f1d-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="90f1d-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="90f1d-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="90f1d-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="90f1d-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="90f1d-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="90f1d-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="90f1d-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="90f1d-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="90f1d-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="90f1d-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="90f1d-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="90f1d-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="90f1d-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="90f1d-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="90f1d-122">운영 체제를 찾지 못함</span><span class="sxs-lookup"><span data-stu-id="90f1d-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="90f1d-123">부팅 오류 또는 INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="90f1d-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="90f1d-124">새 가상 컴퓨터에서 진단 사용</span><span class="sxs-lookup"><span data-stu-id="90f1d-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="90f1d-125">Preview 포털에서 새 Virtual Machine을 만드는 경우 배포 모델 드롭다운에서 **Azure Resource Manager**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-125">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![리소스 관리자](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="90f1d-127">이러한 진단 파일을 저장할 저장소 계정을 선택하려면 모니터링 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-127">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![VM 만들기](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="90f1d-129">Azure Resource Manager 템플릿에서 배포하는 경우 Virtual Machine 리소스로 이동하고 진단 프로필 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-129">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="90f1d-130">"2015-06-15" API 버전 헤더를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-130">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="90f1d-131">진단 프로필을 사용하면 이러한 로그를 저장할 저장소 계정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-131">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="90f1d-132">부팅 진단이 활성화된 샘플 Virtual Machine을 배포하려면 여기에서 리포지토리를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="90f1d-132">To deploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="90f1d-133">기존 가상 컴퓨터 업데이트</span><span class="sxs-lookup"><span data-stu-id="90f1d-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="90f1d-134">포털을 통해 부팅 진단을 활성화하려면 포털을 통해 기존 Virtual Machine을 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-134">To enable boot diagnostics through the Portal, you can also update an existing Virtual Machine through the Portal.</span></span> <span data-ttu-id="90f1d-135">부팅 진단 옵션을 선택하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-135">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="90f1d-136">적용하려면 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="90f1d-136">Restart the VM to take effect.</span></span>

![기본 VM 업데이트](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

