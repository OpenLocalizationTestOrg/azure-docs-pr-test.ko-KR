1. <span data-ttu-id="4ccb9-101">Azure 가상 컴퓨터를 만들고 실행한 후에 Azure Portal의 Virtual Machines 아이콘을 클릭하면 VM을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccb9-101">After the Azure virtual machine is created and running, click the Virtual Machines icon in the Azure portal to view your VMs.</span></span>

1. <span data-ttu-id="4ccb9-102">새 VM에 대한 줄임표(**...**)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccb9-102">Click the ellipsis, **...**, for your new VM.</span></span>

1. <span data-ttu-id="4ccb9-103">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccb9-103">Click **Connect**.</span></span>

   ![포털에서 VM에 연결](./media/virtual-machines-sql-server-remote-desktop-connect/azure-virtual-machine-connect.png)

1. <span data-ttu-id="4ccb9-105">브라우저가 VM에 대해 다운로드한 **RDP** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4ccb9-105">Open the **RDP** file that your browser downloads for the VM.</span></span>

1. <span data-ttu-id="4ccb9-106">원격 데스크톱 연결이 이 원격 연결의 게시자를 식별할 수 없다고 알립니다.</span><span class="sxs-lookup"><span data-stu-id="4ccb9-106">The Remote Desktop Connection notifies you that the publisher of this remote connection cannot be identified.</span></span> <span data-ttu-id="4ccb9-107">**연결**을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccb9-107">Click **Connect** to continue.</span></span>

1. <span data-ttu-id="4ccb9-108">**Windows 보안** 대화 상자에서 **다른 계정 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccb9-108">In the **Windows Security** dialog, click **Use a different account**.</span></span> <span data-ttu-id="4ccb9-109">**More choices**(옵션 더 보기)를 클릭해야 보일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccb9-109">You might have to click **More choices** to see this.</span></span> <span data-ttu-id="4ccb9-110">VM을 만들 때 구성한 사용자 이름과 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccb9-110">Specify the user name and password that you configured when you created the VM.</span></span> <span data-ttu-id="4ccb9-111">사용자 이름 앞에 백슬래시를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccb9-111">You must add a backslash before the user name.</span></span>

   ![원격 데스크톱 인증](./media/virtual-machines-sql-server-remote-desktop-connect/remote-desktop-connect.png)

1. <span data-ttu-id="4ccb9-113">**확인**을 클릭하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccb9-113">Click **OK** to connect.</span></span>