
1. <span data-ttu-id="f6e76-101">로그인에 나열 된 hello 단계를 사용 하 여 Azure 구독을 tooyour [hello Azure CLI 1.0에서에서 tooAzure 연결](../articles/xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-101">Sign in tooyour Azure subscription using hello steps listed in [Connect tooAzure from hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="f6e76-102">다음과 같이 hello 클래식 배포 모드에 있는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-102">Make sure you are in hello Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="f6e76-103">확인 hello Linux 이미지 tooload hello 제공 되는 이미지에서 다음과 같이 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-103">Find out hello Linux image that you want tooload from hello available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="f6e76-104">Windows 명령 프롬프트 창에서 grep 대신 **find** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="f6e76-105">사용 하 여 `azure vm create` toocreate hello 이전 목록에서 hello Linux 이미지를 사용 하 여 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-105">Use `azure vm create` toocreate a VM with hello Linux image from hello previous list.</span></span> <span data-ttu-id="f6e76-106">이 단계에서는 클라우드 서비스 및 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="f6e76-107">이 VM tooan 기존 클라우드 서비스와 연결할 수도 수는 `-c` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-107">You could also connect this VM tooan existing cloud service with a `-c` option.</span></span> <span data-ttu-id="f6e76-108">Hello로 toohello Linux 가상 컴퓨터에서 SSH 끝점 toolog 만들기 `-e` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-108">Create an SSH endpoint toolog in toohello Linux virtual machine with hello `-e` option.</span></span> <span data-ttu-id="f6e76-109">hello 다음 예제에서는 V `myVM` hello를 사용 하 여 `Ubuntu-14_04_4-LTS` hello에 이미지 `West US` 위치, 사용자 이름을 추가 하 고 `ops`:</span><span class="sxs-lookup"><span data-stu-id="f6e76-109">hello following example creates a VM named `myVM` using hello `Ubuntu-14_04_4-LTS` image in hello `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="f6e76-110">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="f6e76-110">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > <span data-ttu-id="f6e76-111">Linux 가상 컴퓨터에 대 한 hello 제공 해야 `-e` 옵션 `vm create`합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-111">For a Linux virtual machine, you must provide hello `-e` option in `vm create`.</span></span> <span data-ttu-id="f6e76-112">Hello 가상 컴퓨터를 만든 후 가능한 tooenable SSH 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-112">It is not possible tooenable SSH after hello virtual machine has been created.</span></span> <span data-ttu-id="f6e76-113">에 대 한 자세한 내용은 SSH, 읽을 [어떻게 tooUse와 Azure에서 Linux에 SSH](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-113">For more details on SSH, read [How tooUse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="f6e76-114">Hello를 사용 하 여 hello VM의 hello 특성을 확인할 수 있습니다 `azure vm show` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-114">You can verify hello attributes of hello VM by using hello `azure vm show` command.</span></span> <span data-ttu-id="f6e76-115">hello 다음 예에서는 나열 hello 라는 VM에 대 한 정보 `myVM`:</span><span class="sxs-lookup"><span data-stu-id="f6e76-115">hello following example lists information for hello VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="f6e76-116">Hello로 VM을 시작 `azure vm start` 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-116">Start your VM with hello `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="f6e76-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6e76-117">Next steps</span></span>
<span data-ttu-id="f6e76-118">이러한 모든 Azure CLI 1.0 가상 컴퓨터 명령에 대 한 세부 정보를 참조 하세요 hello [hello 클래식 배포 API 사용 하 여 hello Azure CLI 1.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e76-118">For details on all these Azure CLI 1.0 virtual machine commands, read hello [Using hello Azure CLI 1.0 with hello Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

