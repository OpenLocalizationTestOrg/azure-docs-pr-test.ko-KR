

## <a name="use-the-portal-to-move-a-vm-to-a-different-subscription"></a><span data-ttu-id="465b8-101">포털을 사용하여 다른 구독으로 VM 이동</span><span class="sxs-lookup"><span data-stu-id="465b8-101">Use the portal to move a VM to a different subscription</span></span>
<span data-ttu-id="465b8-102">포털을 사용하여 다른 구독으로 연결된 리소스인 VM을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-102">You can move a VM and it's associated resources to a different subscription using the portal.</span></span>

1. <span data-ttu-id="465b8-103">[Azure 포털](https://portal.azure.com)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-103">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="465b8-104">**찾아보기** > **Virtual Machines**를 클릭하고 목록에서 이동하려는 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-104">Click **Browse** > **Virtual machines** and select the VM you would like to move from the list.</span></span>
   
    ![연필 아이콘을 클릭하여 리소스 이동 블레이드를 여는 Essentials 섹션 스크린샷](./media/virtual-machines-common-move-vm/move-button.png)
3. <span data-ttu-id="465b8-106">**Essentials** 섹션에서 구독 이름 옆에 있는 **구독 변경** 연필 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-106">In the **Essentials** section, click on the **Change subscription** pencil icon next to the subscription name.</span></span> <span data-ttu-id="465b8-107">**리소스 이동** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-107">The **Move resources** blade will open.</span></span>
   
    ![리소스 이동 블레이드의 스크린샷](./media/virtual-machines-common-move-vm/move.png)
4. <span data-ttu-id="465b8-109">이동할 각 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-109">Select each of the resources to move.</span></span> <span data-ttu-id="465b8-110">대부분의 경우에는 나열된 모든 선택적 리소스를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-110">In most cases, you should move all of the listed optional resources.</span></span>
5. <span data-ttu-id="465b8-111">VM을 이동할 **구독** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-111">Select the **Subscription** where you want the VM to be moved.</span></span>
6. <span data-ttu-id="465b8-112">기존 **리소스 그룹** 을 선택하거나 만들 새 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-112">Select an existing **Resource group** or type a name to have a new resource group created.</span></span>
7. <span data-ttu-id="465b8-113">완료되면 새 리소스 ID가 생성될 것이며, 해당 VM이 이동된 후에는 이 ID를 함께 사용해야 한다는 사실을 이해했음을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-113">When you are done, select that you understand that new resource IDs will be created and those need to be used with the VM once it is moved, then click **OK**.</span></span>

## <a name="use-the-portal-to-move-a-vm-to-another-resource-group"></a><span data-ttu-id="465b8-114">포털을 사용하여 다른 리소스 그룹으로 VM 이동</span><span class="sxs-lookup"><span data-stu-id="465b8-114">Use the portal to move a VM to another resource group</span></span>
<span data-ttu-id="465b8-115">포털을 사용하여 다른 리소스 그룹으로 연결된 리소스인 VM을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-115">You can move a VM and it's associated resources to another resource group using the portal.</span></span>

1. <span data-ttu-id="465b8-116">[Azure 포털](https://portal.azure.com)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-116">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="465b8-117">**찾아보기** > **리소스 그룹**을 클릭하고 VM을 포함하는 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-117">Click **Browse** > **Resource groups** and select the resource group that contains the VM.</span></span>
3. <span data-ttu-id="465b8-118">**리소스 그룹** 블레이드에서 메뉴의 **이동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-118">In the **Resource group** blade, select **Move** from the menu.</span></span>
   
    ![리소스 그룹 메뉴에 있는 이동 단추의 스크린샷](./media/virtual-machines-common-move-vm/move-rg.png)
4. <span data-ttu-id="465b8-120">**리소스 이동** 블레이드에서 이동할 리소스를 선택한 다음 기존 리소스 그룹 이름을 입력하거나 새 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="465b8-120">In the **Move resources** blade, select the resources to be moved and then either type an existing resource group name or choose to create a new resource group.</span></span> <span data-ttu-id="465b8-121">완료되면 새 리소스 ID가 생성될 것이며, 해당 VM이 이동된 후에는 이 ID를 함께 사용해야 한다는 사실을 이해했음을 선택하고 **확인**</span><span class="sxs-lookup"><span data-stu-id="465b8-121">When you are done, select that you understand that new resource IDs will be created and those need to be used with the VM once it is moved, then click **OK**</span></span>
   
    ![리소스 이동 블레이드의 스크린샷](./media/virtual-machines-common-move-vm/move-rg-list.png)

