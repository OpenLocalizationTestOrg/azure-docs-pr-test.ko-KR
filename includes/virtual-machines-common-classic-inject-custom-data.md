


<span data-ttu-id="e3a48-101">이 항목에서는 이러한 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-101">This topic describes how to:</span></span>

* <span data-ttu-id="e3a48-102">프로비전 중에 Azure VM(가상 컴퓨터)에 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="e3a48-103">Windows 및 Linux에 대해 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="e3a48-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="e3a48-104">일부 시스템에서 사용할 수 있는 특수한 도구를 사용하여 사용자 지정 데이터를 자동으로 검색 및 처리</span><span class="sxs-lookup"><span data-stu-id="e3a48-104">Use special tools available on some systems to detect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="e3a48-105">이 문서는 Azure 서비스 관리 API로 생성한 VM을 사용하여 사용자 지정 데이터를 삽입하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-105">This article describes how custom data can be injected by using a VM created with the Azure Service Management API.</span></span> <span data-ttu-id="e3a48-106">Azure 리소스 관리 API를 사용하는 방법은 [예제 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3a48-106">To see how to use the Azure Resource Management API, see [the example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="e3a48-107">Azure 가상 컴퓨터에 사용자 지정 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="e3a48-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="e3a48-108">이 기능은 현재 [Azure 명령줄 인터페이스](https://github.com/Azure/azure-xplat-cli)에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-108">This feature is currently supported only in the [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="e3a48-109">여기서는 데이터가 포함된 `custom-data.txt` 파일을 만든 다음 프로비전 중 VM에 해당 파일을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-109">Here we create a `custom-data.txt` file that contains our data, then inject that in to the VM during provisioning.</span></span> <span data-ttu-id="e3a48-110">`azure vm create` 명령에 대한 모든 옵션을 사용할 수 있지만 다음 예제에서는 한 가지 기본적인 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-110">Although you may use any of the options for the `azure vm create` command, the following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-the-virtual-machine"></a><span data-ttu-id="e3a48-111">가상 컴퓨터에서 사용자 지정 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="e3a48-111">Using custom data in the virtual machine</span></span>
* <span data-ttu-id="e3a48-112">Azure VM이 Windows 기반 VM인 경우 사용자 지정 데이터 파일은 `%SYSTEMDRIVE%\AzureData\CustomData.bin`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-112">If your Azure VM is a Windows-based VM, then the custom data file is saved to `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="e3a48-113">로컬 컴퓨터에서 새 VM으로 전송하기 위해 base64로 인코딩된 경우에도 자동으로 디코딩되며 즉시 열거나 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-113">Although it was base64-encoded to transfer from the local computer to the new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="e3a48-114">이 파일이 있으면 덮어쓰여집니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-114">If the file exists, it is overwritten.</span></span> <span data-ttu-id="e3a48-115">디렉터리에 대한 보안은 **시스템:모든 권한** 및 **관리자:모든 권한**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-115">The security on the directory is set to **System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="e3a48-116">Azure VM이 Linux 기반 VM인 경우 사용자 지정 데이터 파일은 현재 배포에 따라 다음 중 한 곳에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-116">If your Azure VM is a Linux-based VM, then the custom data file will be located in one of the following places depending on your distro.</span></span> <span data-ttu-id="e3a48-117">데이터가 base64로 인코딩되었을 수 있으므로 먼저 데이터를 디코딩해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-117">The data may be base64-encoded, so you may need to decode the data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="e3a48-118">Azure에서 Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="e3a48-118">Cloud-init on Azure</span></span>
<span data-ttu-id="e3a48-119">Azure VM을 Ubuntu 또는 CoreOS 이미지에서 가져온 경우 CustomData를 사용하여 cloud-config를 cloud-init으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData to send a cloud-config to cloud-init.</span></span> <span data-ttu-id="e3a48-120">또는 사용자 지정 데이터 파일이 스크립트인 경우, cloud-init이 스크립트를 실행하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="e3a48-121">Ubuntu 클라우드 이미지</span><span class="sxs-lookup"><span data-stu-id="e3a48-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="e3a48-122">대부분의 Azure Linux 이미지에서 임시 리소스 디스크와 swap 파일을 구성하도록 "/etc/waagent.conf"를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-122">In most Azure Linux images, you would edit "/etc/waagent.conf" to configure the temporary resource disk and swap file.</span></span> <span data-ttu-id="e3a48-123">자세한 내용은 [Azure Linux 에이전트 사용자 가이드](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3a48-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="e3a48-124">그러나 Ubuntu 클라우드 이미지에서 cloud-init을 사용하여 리소스 디스크(즉, "ephemeral" 디스크) 및 swap 파티션을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a48-124">However, on the Ubuntu Cloud Images, you must use cloud-init to configure the resource disk (that is, the "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="e3a48-125">자세한 내용은 Ubuntu wiki에서 [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions)페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3a48-125">See the following page on the Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="e3a48-126">다음 단계: cloud-init 사용</span><span class="sxs-lookup"><span data-stu-id="e3a48-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="e3a48-127">자세한 내용은 [Ubuntu에 대한 cloud-init 설명서](https://help.ubuntu.com/community/CloudInit)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3a48-127">For further information, see the [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="e3a48-128">역할 서비스 관리 REST API 참조 추가</span><span class="sxs-lookup"><span data-stu-id="e3a48-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="e3a48-129">Azure 명령줄 인터페이스</span><span class="sxs-lookup"><span data-stu-id="e3a48-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

