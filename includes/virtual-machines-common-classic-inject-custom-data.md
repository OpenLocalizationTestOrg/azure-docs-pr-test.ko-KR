


<span data-ttu-id="ddaa2-101">이 항목에서는 이러한 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-101">This topic describes how to:</span></span>

* <span data-ttu-id="ddaa2-102">프로비전 중에 Azure VM(가상 컴퓨터)에 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="ddaa2-103">Windows 및 Linux에 대해 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="ddaa2-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="ddaa2-104">일부 시스템 toodetect에서 사용할 수 있는 특수 도구를 사용 하 고 사용자 지정 데이터를 자동으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-104">Use special tools available on some systems toodetect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="ddaa2-105">이 문서에서는 방법을 사용자 지정 데이터 설명 hello Azure 서비스 관리 API를 사용 하 여 만든 VM을 사용 하 여 삽입 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-105">This article describes how custom data can be injected by using a VM created with hello Azure Service Management API.</span></span> <span data-ttu-id="ddaa2-106">toouse hello Azure 리소스 관리 API를 확인 하려면 어떻게 toosee [hello 예제 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-106">toosee how toouse hello Azure Resource Management API, see [hello example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="ddaa2-107">Azure 가상 컴퓨터에 사용자 지정 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="ddaa2-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="ddaa2-108">이 기능은 현재 hello에만 지원 됩니다 [Azure 명령줄 인터페이스](https://github.com/Azure/azure-xplat-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-108">This feature is currently supported only in hello [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="ddaa2-109">만들 여기는 `custom-data.txt` 우리의 데이터가 포함 된 파일 다음 삽입 하는 toohello VM의에서 프로 비전 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-109">Here we create a `custom-data.txt` file that contains our data, then inject that in toohello VM during provisioning.</span></span> <span data-ttu-id="ddaa2-110">Hello에 대 한 hello 옵션 중 하나를 사용할 수 있지만 `azure vm create` 명령, hello 다음 한 가지 기본적인 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-110">Although you may use any of hello options for hello `azure vm create` command, hello following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a><span data-ttu-id="ddaa2-111">사용자 지정 데이터를 사용 하 여 hello 가상 컴퓨터에서</span><span class="sxs-lookup"><span data-stu-id="ddaa2-111">Using custom data in hello virtual machine</span></span>
* <span data-ttu-id="ddaa2-112">Azure VM은 Windows 기반 VM 경우 hello 사용자 지정 데이터 파일은 너무 저장`%SYSTEMDRIVE%\AzureData\CustomData.bin`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-112">If your Azure VM is a Windows-based VM, then hello custom data file is saved too`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="ddaa2-113">Hello 로컬 컴퓨터 toohello에서 base64 인코딩 tootransfer를 없었지만 새 VM은 자동으로 디코딩된 및 열거나 수 즉시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-113">Although it was base64-encoded tootransfer from hello local computer toohello new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ddaa2-114">Hello 파일이 있으면 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-114">If hello file exists, it is overwritten.</span></span> <span data-ttu-id="ddaa2-115">hello 디렉터리에 hello 보안 설정이 너무**시스템: 모든 권한** 및 **관리자: 모든 권한**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-115">hello security on hello directory is set too**System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="ddaa2-116">Azure VM이 Linux 기반 VM hello 사용자 지정 데이터 파일에 배치 됩니다 hello 다음 중 하나에 배포판에 따라 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-116">If your Azure VM is a Linux-based VM, then hello custom data file will be located in one of hello following places depending on your distro.</span></span> <span data-ttu-id="ddaa2-117">hello 데이터가 toodecode hello 데이터를 먼저 할 수 있도록 base64 인코딩된 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-117">hello data may be base64-encoded, so you may need toodecode hello data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="ddaa2-118">Azure에서 Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="ddaa2-118">Cloud-init on Azure</span></span>
<span data-ttu-id="ddaa2-119">Ubuntu 또는 CoreOS 이미지에서 Azure VM이 있는 경우 CustomData toosend 클라우드 구성을 toocloud 초기화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="ddaa2-120">또는 사용자 지정 데이터 파일이 스크립트인 경우, cloud-init이 스크립트를 실행하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="ddaa2-121">Ubuntu 클라우드 이미지</span><span class="sxs-lookup"><span data-stu-id="ddaa2-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="ddaa2-122">대부분의 Azure Linux 이미지에서 편집 하는 "/ etc/waagent.conf" tooconfigure hello 일시적인 리소스 디스크와 스왑 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-122">In most Azure Linux images, you would edit "/etc/waagent.conf" tooconfigure hello temporary resource disk and swap file.</span></span> <span data-ttu-id="ddaa2-123">자세한 내용은 [Azure Linux 에이전트 사용자 가이드](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="ddaa2-124">그러나 hello Ubuntu 클라우드 이미지를 사용 해야 클라우드 init tooconfigure hello 리소스 디스크 (즉, hello "임시" 디스크) 및 교환 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-124">However, on hello Ubuntu Cloud Images, you must use cloud-init tooconfigure hello resource disk (that is, hello "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="ddaa2-125">참조 페이지에 나오는 자세한 세부 정보에 대 한 hello Ubuntu wiki에 hello: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-125">See hello following page on hello Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="ddaa2-126">다음 단계: cloud-init 사용</span><span class="sxs-lookup"><span data-stu-id="ddaa2-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="ddaa2-127">자세한 내용은 참조 hello [Ubuntu 용 클라우드 init 설명서](https://help.ubuntu.com/community/CloudInit)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddaa2-127">For further information, see hello [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="ddaa2-128">역할 서비스 관리 REST API 참조 추가</span><span class="sxs-lookup"><span data-stu-id="ddaa2-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="ddaa2-129">Azure 명령줄 인터페이스</span><span class="sxs-lookup"><span data-stu-id="ddaa2-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

