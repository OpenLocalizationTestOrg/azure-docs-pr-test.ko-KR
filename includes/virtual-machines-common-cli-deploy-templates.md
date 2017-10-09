
* [<span data-ttu-id="0ec62-101">Azure에서 가상 컴퓨터 빨리 만들기</span><span class="sxs-lookup"><span data-stu-id="0ec62-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="0ec62-102">템플릿에서 Azure의 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="0ec62-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="0ec62-103">사용자 지정 이미지에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="0ec62-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="0ec62-104">가상 네트워크 및 부하 분산 장치를 사용하는 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="0ec62-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="0ec62-105">리소스 그룹 제거</span><span class="sxs-lookup"><span data-stu-id="0ec62-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="0ec62-106">리소스 그룹 배포에 대 한 hello 로그 표시</span><span class="sxs-lookup"><span data-stu-id="0ec62-106">Show hello log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="0ec62-107">가상 컴퓨터에 대한 정보 표시</span><span class="sxs-lookup"><span data-stu-id="0ec62-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="0ec62-108">Tooa Linux 기반 가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="0ec62-108">Connect tooa Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="0ec62-109">가상 컴퓨터 중지</span><span class="sxs-lookup"><span data-stu-id="0ec62-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="0ec62-110">가상 컴퓨터 시작</span><span class="sxs-lookup"><span data-stu-id="0ec62-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="0ec62-111">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="0ec62-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="0ec62-112">준비</span><span class="sxs-lookup"><span data-stu-id="0ec62-112">Getting ready</span></span>
<span data-ttu-id="0ec62-113">Azure 리소스 그룹과 hello Azure CLI를 사용 하려면 먼저 toohave hello 오른쪽 Azure CLI 버전 및 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-113">Before you can use hello Azure CLI with Azure resource groups, you need toohave hello right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="0ec62-114">Hello Azure CLI 없는 경우 [설치](../articles/cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-114">If you don't have hello Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-too090-or-later"></a><span data-ttu-id="0ec62-115">Azure CLI 버전 too0.9.0 업데이트 이상 버전</span><span class="sxs-lookup"><span data-stu-id="0ec62-115">Update your Azure CLI version too0.9.0 or later</span></span>
<span data-ttu-id="0ec62-116">형식 `azure --version` 설치 된 버전 0.9.0 이미 있는지 toosee 이상.</span><span class="sxs-lookup"><span data-stu-id="0ec62-116">Type `azure --version` toosee whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="0ec62-117">기본 설치 관리자 hello 중 하나를 사용 하 여 사용 중인 버전 0.9.0 아니거나 tooupdate 필요 이상 버전에서는 또는 **npm** 입력 하 여 `npm update -g azure-cli`합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-117">If your version is not 0.9.0 or later, you need tooupdate it by using one of hello native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="0ec62-118">또한 Azure CLI Docker 컨테이너 hello 다음을 사용 하 여 실행할 수 있습니다 [Docker 이미지](https://registry.hub.docker.com/u/microsoft/azure-cli/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-118">You can also run Azure CLI as a Docker container by using hello following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="0ec62-119">Docker 호스트에서 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-119">From a Docker host, run hello following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="0ec62-120">Azure 계정 및 구독 설정</span><span class="sxs-lookup"><span data-stu-id="0ec62-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="0ec62-121">Azure 구독은 아직 없지만 MSDN 구독은 있는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="0ec62-122">또는 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="0ec62-123">이제 [tooyour Azure 계정에에서 대화형 로그온](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) 입력 하 여 `azure login` 고 대화형 로그인 경험 tooyour Azure 계정에 대 한 hello 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-123">Now [log in tooyour Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following hello prompts for an interactive login experience tooyour Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="0ec62-124">회사 또는 학교 ID 2 단계 인증을 사용할 수 없는, 있습니다 수를 아는 경우 **도** 사용 `azure login -u` 에 ID toolog ळ ा hello와 함께 작동 *없이* 대화형 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with hello work or school ID toolog in *without* an interactive session.</span></span> <span data-ttu-id="0ec62-125">회사 또는 학교 ID 하지 않는 경우 다음을 할 수 있습니다 [개인 Microsoft 계정에서 회사 또는 학교 id를 만들려면](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog hello에서 같은 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello same way.</span></span>
>
>

<span data-ttu-id="0ec62-126">계정에는 둘 이상의 구독이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="0ec62-127">`azure account list`를 입력하여 구독을 나열할 수 있으며, 다음과 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="0ec62-128">Hello 다음을 입력 하 여 hello 현재 Azure 구독을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-128">You can set hello current Azure subscription by typing hello following.</span></span> <span data-ttu-id="0ec62-129">Hello 이름 또는 hello 하는 구독 ID에서 원하는 toomanage hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-129">Use hello subscription name or hello ID that has hello resources you want toomanage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a><span data-ttu-id="0ec62-130">Toohello Azure CLI 리소스 그룹 모드 전환</span><span class="sxs-lookup"><span data-stu-id="0ec62-130">Switch toohello Azure CLI resource group mode</span></span>
<span data-ttu-id="0ec62-131">기본적으로 Azure CLI hello hello 서비스 관리 모드에서 시작 (**asm** 모드).</span><span class="sxs-lookup"><span data-stu-id="0ec62-131">By default, hello Azure CLI starts in hello service management mode (**asm** mode).</span></span> <span data-ttu-id="0ec62-132">Hello tooswitch tooresource 그룹 모드를 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-132">Type hello following tooswitch tooresource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="0ec62-133">Azure 리소스 템플릿 및 리소스 그룹 이해</span><span class="sxs-lookup"><span data-stu-id="0ec62-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="0ec62-134">대부분의 응용 프로그램은 다양한 리소스 유형(예: 하나 이상의 VM 및 저장소 계정, SQL 데이터베이스, 가상 네트워크 또는 콘텐츠 배달 네트워크)의 조합으로 구축되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="0ec62-135">기본 Azure 서비스 관리 API hello와 hello Azure 클래식 포털 표현 이러한 항목-서비스 접근 방식을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-135">hello default Azure service management API and hello Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="0ec62-136">이 방법을 사용 해야 toodeploy 및 hello 개별 서비스를 개별적으로 관리 (또는 작업을 수행 하는 다른 도구를 찾을), 배포의 단일 논리 단위 아니라 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-136">This approach requires you toodeploy and manage hello individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="0ec62-137">*그러나 Azure 리소스 관리자 템플릿*, toodeploy 있습니다 수 및 선언적 방식으로 하나의 논리적 배포 단위로 이러한 다른 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-137">*Azure Resource Manager templates*, however, make it possible for you toodeploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="0ec62-138">명령적 지시 Azure 어떤 toodeploy 하나의 명령 다음에 다른, 대신-hello 리소스 및 관련된 구성 및 배포 매개 변수 모두-JSON 파일의 전체 배포에 설명 하 고이 Azure toodeploy 하나로 이러한 리소스 설명 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-138">Instead of imperatively telling Azure what toodeploy one command after another, you describe your entire deployment in a JSON file -- all of hello resources and associated configuration and deployment parameters -- and tell Azure toodeploy those resources as one group.</span></span>

<span data-ttu-id="0ec62-139">Hello를 관리할 수 있습니다에 Azure CLI 리소스 관리 명령을 사용 하 여 hello 그룹 리소스의 전체 수명 주기:</span><span class="sxs-lookup"><span data-stu-id="0ec62-139">You can then manage hello overall life cycle of hello group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="0ec62-140">중지, 시작 또는 hello 그룹 내의 hello 리소스를 모두 한 번에 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-140">Stop, start, or delete all of hello resources within hello group at once.</span></span>
* <span data-ttu-id="0ec62-141">보안 권한 아래로 규칙 toolock 역할 기반 액세스 제어 (RBAC)에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-141">Apply Role-Based Access Control (RBAC) rules toolock down security permissions on them.</span></span>
* <span data-ttu-id="0ec62-142">작업을 감사합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-142">Audit operations.</span></span>
* <span data-ttu-id="0ec62-143">추가 메타데이터로 리소스에 태그를 지정하여 추적을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="0ec62-144">Azure 리소스 그룹 및 수 있는 작업 수에 대 한 hello에 대 한 기타 등등 학습할 수 있는 [Azure 리소스 관리자 개요](../articles/azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-144">You can learn lots more about Azure resource groups and what they can do for you in hello [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="0ec62-145">템플릿 작성에 관심이 있다면 [Azure 리소스 관리자 템플릿 작성](../articles/resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ec62-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="0ec62-146"><a id="quick-create-a-vm-in-azure"></a>작업: Azure에서 VM 빠르게 만들기</span><span class="sxs-lookup"><span data-stu-id="0ec62-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="0ec62-147">어떤 이미지를 알고 있는 경우에 따라 하 고 해당 이미지에서 VM을 지금 당장 필요한 및 중요 하지 않으면 hello 인프라에 대해 자세히-미정 tootest 결과가 있는 클린 VM에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about hello infrastructure -- maybe you have tootest something on a clean VM.</span></span> <span data-ttu-id="0ec62-148">이 경우에 원하는 toouse hello `azure vm quick-create` 명령을 실행 하 고 VM 및 인프라 hello 인수 필요한 toocreate를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-148">That's when you want toouse hello `azure vm quick-create` command, and pass hello arguments necessary toocreate a VM and its infrastructure.</span></span>

<span data-ttu-id="0ec62-149">먼저 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="0ec62-150">두 번째로 이미지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-150">Second, you'll need an image.</span></span> <span data-ttu-id="0ec62-151">hello Azure CLI로 이미지 toofind 참조 [Navigating PowerShell 및 Azure CLI hello를 사용 하 여 Azure 가상 컴퓨터 이미지를 선택 하 고](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-151">toofind an image with hello Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0ec62-152">그러나 이 문서에서는 다음과 같이 많이 사용되는 간단한 이미지 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="0ec62-153">이 quick-create에서는 CoreOS의 Stable 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="0ec62-154">ComputeImageVersion에 대 한 제공할 수 있습니다 놓는 '최신' hello 매개 변수 hello Azure CLI 및 두 hello 템플릿 언어에 따라.</span><span class="sxs-lookup"><span data-stu-id="0ec62-154">For ComputeImageVersion, you can also simply supply 'latest' as hello parameter in both hello template language and in hello Azure CLI.</span></span> <span data-ttu-id="0ec62-155">따라서 스크립트 또는 템플릿 toomodify 필요 없이 hello 이미지의 최신 및 패치 버전을 hello를 사용 하면 tooalways 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-155">This will allow you tooalways use hello latest and patched version of hello image without having toomodify your scripts or templates.</span></span> <span data-ttu-id="0ec62-156">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="0ec62-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="0ec62-157">PublisherName</span></span> | <span data-ttu-id="0ec62-158">제안</span><span class="sxs-lookup"><span data-stu-id="0ec62-158">Offer</span></span> | <span data-ttu-id="0ec62-159">SKU</span><span class="sxs-lookup"><span data-stu-id="0ec62-159">Sku</span></span> | <span data-ttu-id="0ec62-160">버전</span><span class="sxs-lookup"><span data-stu-id="0ec62-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0ec62-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="0ec62-161">OpenLogic</span></span> |<span data-ttu-id="0ec62-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="0ec62-162">CentOS</span></span> |<span data-ttu-id="0ec62-163">7</span><span class="sxs-lookup"><span data-stu-id="0ec62-163">7</span></span> |<span data-ttu-id="0ec62-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="0ec62-164">7.0.201503</span></span> |
| <span data-ttu-id="0ec62-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="0ec62-165">OpenLogic</span></span> |<span data-ttu-id="0ec62-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="0ec62-166">CentOS</span></span> |<span data-ttu-id="0ec62-167">7.1</span><span class="sxs-lookup"><span data-stu-id="0ec62-167">7.1</span></span> |<span data-ttu-id="0ec62-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="0ec62-168">7.1.201504</span></span> |
| <span data-ttu-id="0ec62-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0ec62-169">CoreOS</span></span> |<span data-ttu-id="0ec62-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0ec62-170">CoreOS</span></span> |<span data-ttu-id="0ec62-171">베타</span><span class="sxs-lookup"><span data-stu-id="0ec62-171">Beta</span></span> |<span data-ttu-id="0ec62-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="0ec62-172">647.0.0</span></span> |
| <span data-ttu-id="0ec62-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0ec62-173">CoreOS</span></span> |<span data-ttu-id="0ec62-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0ec62-174">CoreOS</span></span> |<span data-ttu-id="0ec62-175">Stable</span><span class="sxs-lookup"><span data-stu-id="0ec62-175">Stable</span></span> |<span data-ttu-id="0ec62-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="0ec62-176">633.1.0</span></span> |
| <span data-ttu-id="0ec62-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="0ec62-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="0ec62-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="0ec62-178">DynamicsNAV</span></span> |<span data-ttu-id="0ec62-179">2015</span><span class="sxs-lookup"><span data-stu-id="0ec62-179">2015</span></span> |<span data-ttu-id="0ec62-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="0ec62-180">8.0.40459</span></span> |
| <span data-ttu-id="0ec62-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="0ec62-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="0ec62-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="0ec62-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="0ec62-183">2013</span><span class="sxs-lookup"><span data-stu-id="0ec62-183">2013</span></span> |<span data-ttu-id="0ec62-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="0ec62-184">1.0.0</span></span> |
| <span data-ttu-id="0ec62-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="0ec62-185">msopentech</span></span> |<span data-ttu-id="0ec62-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="0ec62-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="0ec62-187">Standard</span><span class="sxs-lookup"><span data-stu-id="0ec62-187">Standard</span></span> |<span data-ttu-id="0ec62-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="0ec62-188">1.0.0</span></span> |
| <span data-ttu-id="0ec62-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="0ec62-189">msopentech</span></span> |<span data-ttu-id="0ec62-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="0ec62-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="0ec62-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="0ec62-191">Enterprise</span></span> |<span data-ttu-id="0ec62-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="0ec62-192">1.0.0</span></span> |
| <span data-ttu-id="0ec62-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="0ec62-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="0ec62-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="0ec62-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="0ec62-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="0ec62-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="0ec62-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="0ec62-196">12.0.2430</span></span> |
| <span data-ttu-id="0ec62-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="0ec62-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="0ec62-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="0ec62-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="0ec62-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="0ec62-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="0ec62-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="0ec62-200">12.0.2430</span></span> |
| <span data-ttu-id="0ec62-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="0ec62-201">Canonical</span></span> |<span data-ttu-id="0ec62-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="0ec62-202">UbuntuServer</span></span> |<span data-ttu-id="0ec62-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="0ec62-203">12.04.5-LTS</span></span> |<span data-ttu-id="0ec62-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="0ec62-204">12.04.201504230</span></span> |
| <span data-ttu-id="0ec62-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="0ec62-205">Canonical</span></span> |<span data-ttu-id="0ec62-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="0ec62-206">UbuntuServer</span></span> |<span data-ttu-id="0ec62-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="0ec62-207">14.04.2-LTS</span></span> |<span data-ttu-id="0ec62-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="0ec62-208">14.04.201503090</span></span> |
| <span data-ttu-id="0ec62-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="0ec62-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="0ec62-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="0ec62-210">WindowsServer</span></span> |<span data-ttu-id="0ec62-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="0ec62-211">2012-Datacenter</span></span> |<span data-ttu-id="0ec62-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="0ec62-212">3.0.201503</span></span> |
| <span data-ttu-id="0ec62-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="0ec62-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="0ec62-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="0ec62-214">WindowsServer</span></span> |<span data-ttu-id="0ec62-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="0ec62-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="0ec62-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="0ec62-216">4.0.201503</span></span> |
| <span data-ttu-id="0ec62-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="0ec62-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="0ec62-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="0ec62-218">WindowsServer</span></span> |<span data-ttu-id="0ec62-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="0ec62-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="0ec62-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="0ec62-220">5.0.201504</span></span> |
| <span data-ttu-id="0ec62-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="0ec62-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="0ec62-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="0ec62-222">WindowsServerEssentials</span></span> |<span data-ttu-id="0ec62-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="0ec62-223">WindowsServerEssentials</span></span> |<span data-ttu-id="0ec62-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="0ec62-224">1.0.141204</span></span> |
| <span data-ttu-id="0ec62-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="0ec62-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="0ec62-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="0ec62-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="0ec62-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="0ec62-227">2012R2</span></span> |<span data-ttu-id="0ec62-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="0ec62-228">4.3.4665</span></span> |

<span data-ttu-id="0ec62-229">Hello를 입력 하 여 VM을 만들기만 `azure vm quick-create` 명령에 대 한 준비 되 고 hello 묻는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-229">Just create your VM by entering hello `azure vm quick-create` command and being ready for hello prompts.</span></span> <span data-ttu-id="0ec62-230">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="0ec62-231">이제 새 VM으로 전환하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="0ec62-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>작업: 템플릿에서 Azure의 VM 배포</span><span class="sxs-lookup"><span data-stu-id="0ec62-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="0ec62-233">이 섹션에서는 toodeploy 새 Azure VM에에서 Azure CLI hello 함께 서식 파일을 사용 하 여 hello 지침을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-233">Use hello instructions in these sections toodeploy a new Azure VM by using a template with hello Azure CLI.</span></span> <span data-ttu-id="0ec62-234">이 서식 파일은 새 가상 네트워크와는 달리 지역 및 단일 서브넷에 단일 가상 컴퓨터를 만듭니다 `azure vm quick-create`, 원하는 대로 정확 하 게 toodescribe 있습니다 수 있도록 하 고 오류 없이 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you toodescribe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="0ec62-235">다음은 이 템플릿에서 만드는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a><span data-ttu-id="0ec62-236">1 단계: hello JSON 파일 hello 템플릿 매개 변수를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-236">Step 1: Examine hello JSON file for hello template parameters</span></span>
<span data-ttu-id="0ec62-237">다음은 hello 템플릿에 대 한 hello JSON 파일의 hello 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-237">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="0ec62-238">(또한 hello 서식 파일에 있는 [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="0ec62-238">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="0ec62-239">Hello 디자이너 toogive 많은 매개 변수를 선택 또는 선택 toooffer 더 수정 하는 템플릿을 만들어 일부만 되었을 하므로 템플릿은 유연 하 고,입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-239">Templates are flexible, so hello designer may have chosen toogive you lots of parameters or chosen toooffer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="0ec62-240">순서 toocollect hello 정보에서 매개 변수로 toopass hello 템플릿이 필요 hello 템플릿 파일 (이 항목 아래 템플릿 인라인 있음)을 열고 확인 hello **매개 변수** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-240">In order toocollect hello information you need toopass hello template as parameters, open hello template file (this topic has a template inline, below) and examine hello **parameters** values.</span></span>

<span data-ttu-id="0ec62-241">이 경우 hello 템플릿이 묻는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-241">In this case, hello template below will ask for:</span></span>

* <span data-ttu-id="0ec62-242">고유한 저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="0ec62-242">A unique storage account name.</span></span>
* <span data-ttu-id="0ec62-243">Hello VM에 대 한 관리자 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-243">An admin user name for hello VM.</span></span>
* <span data-ttu-id="0ec62-244">암호</span><span class="sxs-lookup"><span data-stu-id="0ec62-244">A password.</span></span>
* <span data-ttu-id="0ec62-245">Hello world toouse 외부에 대 한 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-245">A domain name for hello outside world toouse.</span></span>
* <span data-ttu-id="0ec62-246">Ubuntu Server 버전 번호 -- 목록 중 하나만 허용</span><span class="sxs-lookup"><span data-stu-id="0ec62-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="0ec62-247">자세한 내용은 [사용자 이름 및 암호 요구 사항](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ec62-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="0ec62-248">이러한 값을 사용 하도록 결정 되 면 준비 toocreate에 대 한 그룹 하 고 Azure 구독에이 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-248">Once you decide on these values, you're ready toocreate a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="0ec62-249">2 단계: hello 템플릿을 사용 하 여 hello 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="0ec62-249">Step 2: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="0ec62-250">매개 변수 값을 준비 했으면 템플릿 배포에 대 한 리소스 그룹 만들기 하며 다음 hello 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy hello template.</span></span>

<span data-ttu-id="0ec62-251">toocreate hello 리소스 그룹으로 형식 `azure group create <group name> <location>` hello 그룹 및 toodeploy 넣을 hello 데이터 센터 위치 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-251">toocreate hello resource group, type `azure group create <group name> <location>` with hello name of hello group you want and hello datacenter location into which you want toodeploy.</span></span> <span data-ttu-id="0ec62-252">이 작업은 신속하게 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="0ec62-253">지금은 toocreate hello 배포, 호출 `azure group deployment create` 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-253">Now toocreate hello deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="0ec62-254">hello 템플릿 파일 (JSON 템플릿 tooa 로컬 파일 위에 hello 저장) 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-254">hello template file (if you saved hello above JSON template tooa local file).</span></span>
* <span data-ttu-id="0ec62-255">(원할 경우 hello 파일 GitHub 또는 일부 다른 웹 주소에 toopoint) URI 템플릿.</span><span class="sxs-lookup"><span data-stu-id="0ec62-255">A template URI (if you want toopoint at hello file in GitHub or some other web address).</span></span>
* <span data-ttu-id="0ec62-256">toodeploy 넣을 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-256">hello resource group into which you want toodeploy.</span></span>
* <span data-ttu-id="0ec62-257">배포 이름(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="0ec62-257">An optional deployment name.</span></span>

<span data-ttu-id="0ec62-258">입력 정보 요청된 toosupply hello 매개 변수 값의 hello JSON 파일의 hello "parameters" 섹션에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-258">You will be prompted toosupply hello values of parameters in hello "parameters" section of hello JSON file.</span></span> <span data-ttu-id="0ec62-259">모든 hello 매개 변수 값을 지정한 경우 배포 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-259">When you have specified all hello parameter values, your deployment will begin.</span></span>

<span data-ttu-id="0ec62-260">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="0ec62-261">Hello 다음 유형의 정보를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-261">You will receive hello following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <span data-ttu-id="0ec62-262"><a id="create-a-custom-vm-image"></a>작업: 사용자 지정 VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="0ec62-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="0ec62-263">위의 서식 파일의 기본 사용법 hello를 살펴 보았으며, 따라서 म 수를 사용 하 여 비슷한 지침 toocreate 사용자 지정 VM Azure에서 특정.vhd 파일 로부터 통해 템플릿을 사용 하 여 hello Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-263">You've seen hello basic usage of templates above, so now we can use similar instructions toocreate a custom VM from a specific .vhd file in Azure by using a template via hello Azure CLI.</span></span> <span data-ttu-id="0ec62-264">hello 차이점은이 템플릿은 지정 된 가상 하드 디스크 (VHD)에서 단일 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-264">hello difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="0ec62-265">Hello 서식 파일에 대 한 hello JSON 파일을 검사 하는 1 단계:</span><span class="sxs-lookup"><span data-stu-id="0ec62-265">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="0ec62-266">예를 들어이 섹션을 사용 하는 hello 서식 파일에 대 한 hello JSON 파일의 hello 콘텐츠는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-266">Here are hello contents of hello JSON file for hello template that this section uses as an example.</span></span> <span data-ttu-id="0ec62-267">(또한 hello 서식 파일에 있는 [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="0ec62-267">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="0ec62-268">다시, 기본값이 없는 hello 매개 변수에 대 한 tooenter 원하는 toofind hello 값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-268">Again, you will need toofind hello values you want tooenter for hello parameters that do not have default values.</span></span> <span data-ttu-id="0ec62-269">Hello를 실행 하는 경우 `azure group deployment create` 명령, Azure CLI hello 라는 tooenter 하면 해당 값 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-269">When you run hello `azure group deployment create` command, hello Azure CLI will prompt you tooenter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a><span data-ttu-id="0ec62-270">2 단계: hello VHD 받기</span><span class="sxs-lookup"><span data-stu-id="0ec62-270">Step 2: Obtain hello VHD</span></span>
<span data-ttu-id="0ec62-271">이 경우 .vhd가 반드시 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="0ec62-272">이미 Azure에 있는 VHD를 사용하거나 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="0ec62-273">Windows 기반 가상 컴퓨터에 대 한 참조 [만들기 및 업로드 Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="0ec62-274">Linux 기반 가상 컴퓨터에 대 한 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains hello Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="0ec62-275">3 단계: hello 템플릿을 사용 하 여 hello 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="0ec62-275">Step 3: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="0ec62-276">이제 준비 toocreate hello.vhd에 따라 새 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="0ec62-276">Now you're ready toocreate a new virtual machine based on hello .vhd.</span></span> <span data-ttu-id="0ec62-277">사용 하 여, 그룹 toodeploy 만들기 `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="0ec62-277">Create a group toodeploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="0ec62-278">그런 다음 hello를 사용 하 여 hello 배포를 만들 `--template-uri` hello 템플릿에서 직접 옵션 toocall (하거나 hello를 사용할 수 있습니다 `--template-file` 옵션 toouse 로컬로 저장 된 파일).</span><span class="sxs-lookup"><span data-stu-id="0ec62-278">Then create hello deployment by using hello `--template-uri` option toocall in hello template directly (or you can use hello `--template-file` option toouse a file that you have saved locally).</span></span> <span data-ttu-id="0ec62-279">Hello 템플릿에 지정한 기본값을 사용 하므로 메시지가 표시 됩니다만 몇 가지 사항에 대 한 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-279">Note that because hello template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="0ec62-280">서로 다른 위치에서 hello 서식 파일을 배포 하는 경우 일부 명명 충돌과 hello 기본값 (특히 hello DNS 이름 만들면) 헤드로 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-280">If you deploy hello template in different places, you may find that some naming collisions occur with hello default values (particularly hello DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="0ec62-281">출력은 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-281">Output looks something like hello following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <span data-ttu-id="0ec62-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>작업: 가상 네트워크 및 외부 부하 분산 장치를 사용하는 여러 VM 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="0ec62-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="0ec62-283">이 서식 파일에는 포트 80에는 부하 분산 규칙을 구성 및 부하 분산 장치 아래의 toocreate 두 개의 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-283">This template allows you toocreate two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="0ec62-284">또한 이 템플릿에서는 저장소 계정, 가상 네트워크, 공용 IP 주소, 가용성 집합 및 네트워크 인터페이스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="0ec62-285">이러한 단계 toodeploy Azure PowerShell 명령을 통해 hello GitHub 서식 파일 저장소에서 리소스 관리자 템플릿을 사용 하 여 가상 네트워크 및 부하 분산 장치를 사용 하는 다중 VM 응용 프로그램을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-285">Follow these steps toodeploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in hello GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="0ec62-286">Hello 서식 파일에 대 한 hello JSON 파일을 검사 하는 1 단계:</span><span class="sxs-lookup"><span data-stu-id="0ec62-286">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="0ec62-287">다음은 hello 템플릿에 대 한 hello JSON 파일의 hello 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-287">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="0ec62-288">Hello 가장 최신 버전을 원하는 경우 것 찾았으며 [서식 파일에 대 한 hello GitHub 리포지토리에서](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-288">If you want hello most recent version, it's located [at hello GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="0ec62-289">이 항목에서는 hello `--template-uri` hello 서식 파일에서 스위치 toocall hello 사용할 수도 `--template-file` toopass 로컬 버전을 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-289">This topic uses hello `--template-uri` switch toocall in hello template, but you can also use hello `--template-file` switch toopass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a><span data-ttu-id="0ec62-290">2 단계: hello 템플릿을 사용 하 여 hello 배포 만들기</span><span class="sxs-lookup"><span data-stu-id="0ec62-290">Step 2: Create hello deployment by using hello template</span></span>
<span data-ttu-id="0ec62-291">사용 하 여 hello 서식 파일에 대 한 리소스 그룹 만들기 `azure group create <location>`합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-291">Create a resource group for hello template by using `azure group create <location>`.</span></span> <span data-ttu-id="0ec62-292">그런 다음 사용 하 여 해당 리소스 그룹에 배포를 만드는 `azure group deployment create` 하 고 전달 hello 리소스 그룹, 배포 이름을 전달 하 고 매개 변수에 기본값을 갖지 않은 hello 서식 파일에 대 한 hello 메시지에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing hello resource group, passing a deployment name, and answering hello prompts for parameters in hello template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="0ec62-293">이제 hello를 사용 하 여 `azure group deployment create` 명령과 hello `--template-uri` toodeploy hello 서식 파일 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-293">Now use hello `azure group deployment create` command and hello `--template-uri` option toodeploy hello template.</span></span> <span data-ttu-id="0ec62-294">아래와 같이 메시지가 표시되면 매개 변수 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="0ec62-295">이 템플릿은 Windows Server 이미지를 배포하지만 Linux 이미지로 간단하게 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="0ec62-296">여러 웜 관리자와 toocreate Docker 클러스터를 선택 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0ec62-296">Want toocreate a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="0ec62-297">[가능합니다](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="0ec62-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="0ec62-298"><a id="remove-a-resource-group"></a>작업: 리소스 그룹 제거</span><span class="sxs-lookup"><span data-stu-id="0ec62-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="0ec62-299">Tooa 리소스 그룹을 다시 배포할 수 없지만 하나 완료 된 후 사용 하 여 삭제할 수 있습니다 `azure group delete <group name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-299">Remember that you can redeploy tooa resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="0ec62-300"><a id="show-the-log-for-a-resource-group-deployment"></a>리소스 그룹 배포에 대 한 hello 로그를 표시 하는 작업:</span><span class="sxs-lookup"><span data-stu-id="0ec62-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show hello log for a resource group deployment</span></span>
<span data-ttu-id="0ec62-301">템플릿을 만들거나 사용할 때 일반적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="0ec62-302">그룹에 대 한 hello 호출 toodisplay hello 배포 로그 `azure group log show <groupname>`, 많은 양의 발생 한 시간-또는 하지 않은 이유를 이해 하는 데 유용한 정보를 표시 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-302">hello call toodisplay hello deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="0ec62-303">(배포 문제 해결에 대한 자세한 내용 및 문제에 대한 기타 정보는 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md)을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="0ec62-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="0ec62-304">특정 오류 tootarget, 예를 들어 사용할 수 있습니다와 같은 도구 **jq** 좀 더 정확 하 게, toocorrect 필요한는 개별 오류와 같은 tooquery 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-304">tootarget specific failures, for example, you might use tools like **jq** tooquery things a bit more precisely, such as which individual failures you need toocorrect.</span></span> <span data-ttu-id="0ec62-305">hello 다음 예제에서는 **jq** 배포에 대 한 로그 tooparse **lbgroup**찾고 오류에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-305">hello following example uses **jq** tooparse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="0ec62-306">잘못되어 수정하거나 다시 시도할 항목을 매우 신속하게 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="0ec62-307">사례를 따르는 hello에서 hello 서식 파일에 된 Vm을 만들 두 hello에 동시 잠금을 hello.vhd에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-307">In hello following case, hello template had been creating two VMs at hello same time, which created a lock on hello .vhd.</span></span> <span data-ttu-id="0ec62-308">(Hello 서식 파일을 수정한 후 hello 배포 성공 신속 하 게 합니다.)</span><span class="sxs-lookup"><span data-stu-id="0ec62-308">(After we modified hello template, hello deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="0ec62-309"><a id="display-information-about-a-virtual-machine"></a>작업: 가상 컴퓨터에 대한 정보 표시</span><span class="sxs-lookup"><span data-stu-id="0ec62-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="0ec62-310">Hello를 사용 하 여 리소스 그룹에 특정 Vm에 대 한 정보를 볼 수 `azure vm show <groupname> <vmname>` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-310">You can see information about specific VMs in your resource group by using hello `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="0ec62-311">그룹에 있는 둘 이상의 VM가 있으면 먼저 해야 toolist hello Vm 그룹에서 사용 하 여 `azure vm list <groupname>`합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-311">If you have more than one VM in your group, you might first need toolist hello VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="0ec62-312">그런 다음 myVM1을 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="0ec62-313">Tooprogrammatically 저장소 콘솔 명령의 hello 출력을 조작 하는 경우에 toouse 같은 도구는 JSON을 구문 분석을 설정할 수 있습니다 있습니다  **[jq](https://github.com/stedolan/jq)**  또는  **[jsawk](https://github.com/micha/jsawk)** , 또는 hello 작업에 대 한 좋은 되는 언어 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-313">If you want tooprogrammatically store and manipulate hello output of your console commands, you may want toouse a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for hello task.</span></span>
>
>

## <span data-ttu-id="0ec62-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>작업: tooa Linux 기반 가상 컴퓨터에 로그온</span><span class="sxs-lookup"><span data-stu-id="0ec62-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on tooa Linux-based virtual machine</span></span>
<span data-ttu-id="0ec62-315">일반적으로 Linux 컴퓨터에 연결 된 toothrough SSH 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-315">Typically Linux machines are connected toothrough SSH.</span></span> <span data-ttu-id="0ec62-316">자세한 내용은 참조 [어떻게 toouse와 Azure에서 Linux에 SSH](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-316">For more information, see [How toouse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="0ec62-317"><a id="stop-a-virtual-machine"></a>작업: VM 중지</span><span class="sxs-lookup"><span data-stu-id="0ec62-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="0ec62-318">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="0ec62-319">경우이 매개 변수 tookeep hello의 가상 IP (VIP) hello vnet 사용 하 여 해당 vnet의 마지막 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-319">Use this parameter tookeep hello virtual IP (VIP) of hello vnet in case it's hello last VM in that vnet.</span></span> <br><br> <span data-ttu-id="0ec62-320">Hello를 사용 하는 경우 `StayProvisioned` 매개 변수를 계속 청구 됩니다 hello VM에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-320">If you use hello `StayProvisioned` parameter, you'll still be billed for hello VM.</span></span>
>
>

## <span data-ttu-id="0ec62-321"><a id="start-a-virtual-machine"></a>작업: VM 시작</span><span class="sxs-lookup"><span data-stu-id="0ec62-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="0ec62-322">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="0ec62-323"><a id="attach-a-data-disk"></a>작업: 데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="0ec62-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="0ec62-324">또한 해야 toodecide tooattach 새 디스크 또는 하나를 포함 하는지 여부를 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-324">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="0ec62-325">새 디스크에 대 한 hello 명령 hello.vhd 파일 만들고 연결 hello에 동일한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-325">For a new disk, hello command creates hello .vhd file and attaches it in hello same command.</span></span>

<span data-ttu-id="0ec62-326">새 디스크 tooattach이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-326">tooattach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="0ec62-327">기존의 데이터 디스크를 tooattach이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-327">tooattach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="0ec62-328">그런 다음 Linux에서와 마찬가지로 toomount hello 디스크에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-328">Then you'll need toomount hello disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ec62-329">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ec62-329">Next steps</span></span>
<span data-ttu-id="0ec62-330">훨씬 더 많은 사용 예제를 보려면 Azure CLI hello로 **arm** 모드 참조 [Mac, Linux 및 Windows Azure 리소스 관리자에 대 한 Azure CLI를 사용 하 여 hello](../articles/xplat-cli-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-330">For far more examples of Azure CLI usage with hello **arm** mode, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="0ec62-331">Azure 리소스와 해당 개념에 대해 자세히 toolearn 참조 [Azure 리소스 관리자 개요](../articles/azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ec62-331">toolearn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="0ec62-332">사용할 수 있는 더 많은 템플릿은 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/) 및 [템플릿을 사용하는 응용 프로그램 프레임워크](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ec62-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
