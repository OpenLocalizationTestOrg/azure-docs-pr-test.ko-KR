<span data-ttu-id="2d03b-101">이제 Azure에서 두 가지 디버깅 기능에 대한 지원이 제공됩니다. Azure Virtual Machines Resource Manager 배포 모델에 대한 콘솔 출력 및 스크린샷 지원.</span><span class="sxs-lookup"><span data-stu-id="2d03b-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="2d03b-102">설정할 때 사용자 고유의 이미지 tooAzure 이거나도 부팅 중 hello 플랫폼 이미지, 가상 컴퓨터를 부팅할 수 없는 상태로 가져옵니다 하는 이유는 여러 가지 이유가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d03b-102">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="2d03b-103">Tooeasily 있습니다를 진단 하 고 가상 컴퓨터 부팅 실패에서 복구 이러한 기능 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d03b-103">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="2d03b-104">Linux 가상 컴퓨터에 대 한 hello 출력 hello 포털에서에서 콘솔 로그를 쉽게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d03b-104">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="2d03b-106">그러나 Windows와 Linux 가상 컴퓨터에 대 한 Azure가 해줍니다 toosee를 hello 하이퍼바이저에서 hello VM의 스크린샷:</span><span class="sxs-lookup"><span data-stu-id="2d03b-106">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![오류](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="2d03b-108">이 두 가지 기능이 모든 지역의 Azure Virtual Machines에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d03b-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="2d03b-109">참고, 스크린샷 및 출력 저장소 계정에 분 tooappear too10 차지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d03b-109">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="2d03b-110">일반적인 부팅 오류</span><span class="sxs-lookup"><span data-stu-id="2d03b-110">Common boot errors</span></span>

- [<span data-ttu-id="2d03b-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="2d03b-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="2d03b-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="2d03b-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="2d03b-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="2d03b-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="2d03b-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="2d03b-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="2d03b-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="2d03b-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="2d03b-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="2d03b-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="2d03b-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="2d03b-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="2d03b-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="2d03b-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="2d03b-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="2d03b-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="2d03b-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="2d03b-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="2d03b-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="2d03b-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="2d03b-122">운영 체제를 찾지 못함</span><span class="sxs-lookup"><span data-stu-id="2d03b-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="2d03b-123">부팅 오류 또는 INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="2d03b-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="2d03b-124">새 가상 컴퓨터에서 진단 사용</span><span class="sxs-lookup"><span data-stu-id="2d03b-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="2d03b-125">Hello 미리 보기 포털에서에서 새 가상 컴퓨터를 만들 때 선택 hello **Azure 리소스 관리자** hello 배포 모델 드롭다운에서:</span><span class="sxs-lookup"><span data-stu-id="2d03b-125">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![리소스 관리자](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="2d03b-127">이러한 진단 파일 hello 모니터링 옵션 tooselect hello 저장소 계정 tooplace 하려는 위치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d03b-127">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![VM 만들기](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="2d03b-129">Azure 리소스 관리자 템플릿을 배포 하는 경우 tooyour 가상 컴퓨터 리소스를 이동 하 고 hello 진단 프로필 섹션을 추가 하세요.</span><span class="sxs-lookup"><span data-stu-id="2d03b-129">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="2d03b-130">Toouse hello "2015-06-15" API 버전 헤더를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d03b-130">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="2d03b-131">hello 진단 프로필 tooselect hello 저장소 계정을 저장할 tooput 이러한 로그 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d03b-131">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

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

<span data-ttu-id="2d03b-132">toodeploy 부트 진단을 사용, 체크 아웃 여기의 리포지토리에서 샘플 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="2d03b-132">toodeploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="2d03b-133">기존 가상 컴퓨터 업데이트</span><span class="sxs-lookup"><span data-stu-id="2d03b-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="2d03b-134">hello 포털을 통해 tooenable 부트 진단을 hello 포털을 통해 기존 가상 컴퓨터를 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d03b-134">tooenable boot diagnostics through hello Portal, you can also update an existing Virtual Machine through hello Portal.</span></span> <span data-ttu-id="2d03b-135">Hello 부트 진단이 저장 및 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d03b-135">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="2d03b-136">Hello VM tootake 효과 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d03b-136">Restart hello VM tootake effect.</span></span>

![기본 VM 업데이트](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

