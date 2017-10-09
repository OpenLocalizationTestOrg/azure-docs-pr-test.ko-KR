<span data-ttu-id="8ff77-101">연결 된 tooa 가상 컴퓨터가 있는 데이터 디스크를 더 이상 해야 하는 경우 쉽게 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-101">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="8ff77-102">디스크를 분리 hello 디스크 hello 가상 컴퓨터에서 제거 되지만 hello Azure 저장소 계정에서에서 hello 디스크를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-102">Detaching a disk removes hello disk from hello virtual machine, but doesn't delete hello disk from hello Azure storage account.</span></span>

<span data-ttu-id="8ff77-103">Hello toouse hello 디스크에 기존 데이터를 다시 선택 하면 다시 연결할 수 toohello 동일한 가상 컴퓨터 이거나 다른 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="8ff77-104">운영 체제 디스크 toodetach 먼저 toodelete hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="8ff77-104">toodetach an operating system disk, you first need toodelete hello virtual machine.</span></span>
>

## <a name="find-hello-disk"></a><span data-ttu-id="8ff77-105">Hello 디스크 찾기</span><span class="sxs-lookup"><span data-stu-id="8ff77-105">Find hello disk</span></span>
<span data-ttu-id="8ff77-106">디스크 hello 또는 tooverify hello 이름을 모르는 경우 분리 하기 전에, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-106">If you don't know hello name of hello disk or want tooverify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="8ff77-107">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8ff77-108">클릭 **가상 컴퓨터**을 다음 선택 hello 적절 한 VM 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-108">Click **Virtual Machines**, and then select hello appropriate VM.</span></span>

3. <span data-ttu-id="8ff77-109">클릭 **디스크** hello 따라 왼쪽 가장자리 hello 가상 컴퓨터 대시보드의 아래 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-109">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="8ff77-110">가상 컴퓨터 대시보드 hello hello 이름과 연결 된 모든 디스크의 형식을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-110">hello virtual machine dashboard lists hello name and type of all attached disks.</span></span> <span data-ttu-id="8ff77-111">예를 들어, 이 화면에는 한 개의 운영 체제(OS) 디스크와 한 개의 데이터 디스크가 있는 가상 컴퓨터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![데이터 디스크 찾기](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a><span data-ttu-id="8ff77-113">Hello 디스크를 분리</span><span class="sxs-lookup"><span data-stu-id="8ff77-113">Detach hello disk</span></span>
1. <span data-ttu-id="8ff77-114">Hello Azure 포털에서에서 클릭 **가상 컴퓨터**, 한 다음 원하는 toodetach hello 데이터 디스크에 있는 hello 가상 컴퓨터의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-114">From hello Azure portal, click **Virtual Machines**, and then click hello name of hello virtual machine that has hello data disk you want toodetach.</span></span>

2. <span data-ttu-id="8ff77-115">클릭 **디스크** hello 따라 왼쪽 가장자리 hello 가상 컴퓨터 대시보드의 아래 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-115">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="8ff77-116">Toodetach hello 디스크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-116">Click hello disk you want toodetach.</span></span>

  ![Hello 디스크 toodetach 식별](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="8ff77-118">Hello 명령 모음에서 클릭 **분리**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ff77-118">From hello command bar, click **Detach**.</span></span>

  ![Hello 찾을 detach 명령](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="8ff77-120">Hello 확인 창에서 클릭 **예** toodetach hello 디스크.</span><span class="sxs-lookup"><span data-stu-id="8ff77-120">In hello confirmation window, click **Yes** toodetach hello disk.</span></span>

  ![Hello 디스크를 분리를 확인 합니다.](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="8ff77-122">hello 디스크 저장소에 남아 있지만 더 이상 연결 된 tooa 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="8ff77-122">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>
