


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="acadb-101">템플릿을 통해 가상 컴퓨터에 태그 지정</span><span class="sxs-lookup"><span data-stu-id="acadb-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="acadb-102">먼저 템플릿을 통한 태그 지정을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="acadb-103">[이 템플릿은](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) hello 다음 리소스에서 끝 태그를 삽입: (가상 컴퓨터) 컴퓨팅, 저장소 (저장소 계정) 및 네트워크 (공용 IP 주소, 가상 네트워크 및 네트워크 인터페이스).</span><span class="sxs-lookup"><span data-stu-id="acadb-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on hello following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="acadb-104">이 템플릿은 Windows VM에 대한 것이지만 Linux VM에도 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="acadb-105">Hello 클릭 **tooAzure 배포** hello에서 단추 [템플릿 링크](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags)합니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-105">Click hello **Deploy tooAzure** button from hello [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="acadb-106">이것은 toohello 탐색 [Azure 포털](https://portal.azure.com/) 이 서식 파일을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-106">This will navigate toohello [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![태그가 포함된 간단한 배포](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="acadb-108">이 템플릿에 hello 태그: *부서*, *응용 프로그램*, 및 *만든*합니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-108">This template includes hello following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="acadb-109">있습니다 수 추가/편집 hello 서식 파일에서 직접 이러한 태그 다른 태그 이름을 넣으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-109">You can add/edit these tags directly in hello template if you would like different tag names.</span></span>

![템플릿의 Azure 태그](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="acadb-111">볼 수 있듯이 hello 태그는 콜론 (:)으로 구분 하는 키/값 쌍으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-111">As you can see, hello tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="acadb-112">이 형식 hello 태그를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-112">hello tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="acadb-113">사용자가 선택한 hello 태그를 사용 하 여 편집을 마친 후 hello 서식 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-113">Save hello template file after you finish editing it with hello tags of your choice.</span></span>

<span data-ttu-id="acadb-114">다음으로 hello **매개 변수 편집** 섹션을 채울 수 hello 값 태그에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-114">Next, in hello **Edit Parameters** section, you can fill out hello values for your tags.</span></span>

![Azure 포털에서 태그 편집](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="acadb-116">클릭 **만들기** toodeploy 태그 값이 포함 된이 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-116">Click **Create** toodeploy this template with your tag values.</span></span>

## <a name="tagging-through-hello-portal"></a><span data-ttu-id="acadb-117">Hello 포털을 통해 태그 지정</span><span class="sxs-lookup"><span data-stu-id="acadb-117">Tagging through hello Portal</span></span>
<span data-ttu-id="acadb-118">리소스 태그를 만든 후 보기, 추가 및 hello 포털에서 태그를 삭제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-118">After creating your resources with tags, you can view, add, and delete tags in hello portal.</span></span>

<span data-ttu-id="acadb-119">태그 아이콘 tooview 태그를 삽입 선택 hello:</span><span class="sxs-lookup"><span data-stu-id="acadb-119">Select hello tags icon tooview your tags:</span></span>

![Azure 포털의 태그 아이콘](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="acadb-121">고유한 키/값 쌍을 정의 하 여 hello 포털을 통해 새 태그를 추가 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-121">Add a new tag through hello portal by defining your own Key/Value pair, and save it.</span></span>

![Azure 포털에서 새 태그 추가](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="acadb-123">이제 새 태그를 리소스에 대 한 태그의 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="acadb-123">Your new tag should now appear in hello list of tags for your resource.</span></span>

![Azure 포털에서 저장된 새 태그](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

