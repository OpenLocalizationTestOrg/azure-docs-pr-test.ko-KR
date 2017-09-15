


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="d3906-101">템플릿을 통해 가상 컴퓨터에 태그 지정</span><span class="sxs-lookup"><span data-stu-id="d3906-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="d3906-102">먼저 템플릿을 통한 태그 지정을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="d3906-103">[이 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) 은 계산(가상 컴퓨터), 저장소(저장소 계정) 및 네트워크(공용 IP 주소, 가상 네트워크 및 네트워크 인터페이스) 리소스에 태그를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on the following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="d3906-104">이 템플릿은 Windows VM에 대한 것이지만 Linux VM에도 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="d3906-105">**템플릿 링크** 에서 [Azure에 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags)단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-105">Click the **Deploy to Azure** button from the [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="d3906-106">이렇게 하면 이 템플릿을 배포할 수 있는 [Azure 포털](https://portal.azure.com/) 로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-106">This will navigate to the [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![태그가 포함된 간단한 배포](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="d3906-108">이 템플릿에는 *부서*, *응용 프로그램* 및 *만든 사람* 태그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-108">This template includes the following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="d3906-109">다른 태그 이름을 사용하려는 경우 템플릿에서 직접 이러한 태그를 추가/편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-109">You can add/edit these tags directly in the template if you would like different tag names.</span></span>

![템플릿의 Azure 태그](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="d3906-111">여기서 볼 수 있듯이 태그는 콜론(:)으로 구분된 키/값 쌍으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-111">As you can see, the tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="d3906-112">다음 형식으로 태그를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-112">The tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="d3906-113">편집을 마친 후 선택한 태그와 함께 템플릿 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-113">Save the template file after you finish editing it with the tags of your choice.</span></span>

<span data-ttu-id="d3906-114">이어서 **매개 변수 편집** 섹션에서 태그의 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-114">Next, in the **Edit Parameters** section, you can fill out the values for your tags.</span></span>

![Azure 포털에서 태그 편집](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="d3906-116">**만들기** 를 클릭하여 태그 값과 함께 이 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-116">Click **Create** to deploy this template with your tag values.</span></span>

## <a name="tagging-through-the-portal"></a><span data-ttu-id="d3906-117">포털을 통해 태그 지정</span><span class="sxs-lookup"><span data-stu-id="d3906-117">Tagging through the Portal</span></span>
<span data-ttu-id="d3906-118">태그와 함께 리소스를 만든 후 포털에서 태그를 표시, 추가 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-118">After creating your resources with tags, you can view, add, and delete tags in the portal.</span></span>

<span data-ttu-id="d3906-119">태그 아이콘을 선택하여 태그를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-119">Select the tags icon to view your tags:</span></span>

![Azure 포털의 태그 아이콘](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="d3906-121">사용자 고유의 키/값 쌍을 정의하여 포털을 통해 새 태그를 추가하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-121">Add a new tag through the portal by defining your own Key/Value pair, and save it.</span></span>

![Azure 포털에서 새 태그 추가](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="d3906-123">이제 리소스에 대한 태그 목록에 새 태그가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d3906-123">Your new tag should now appear in the list of tags for your resource.</span></span>

![Azure 포털에서 저장된 새 태그](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

