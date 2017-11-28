<span data-ttu-id="55450-101">트리거를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="55450-101">Let's add a trigger.</span></span>

1. <span data-ttu-id="55450-102">Logic Apps 디자이너의 검색 상자에 *sftp*를 입력한 후 **SFTP - 파일을 추가하거나 수정할 때** 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55450-102">Enter *sftp* in the search box on the logic apps designer then select the **SFTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="55450-103">![SFTP 트리거 이미지 1](./media/connectors-create-api-sftp/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="55450-103">![SFTP trigger image 1](./media/connectors-create-api-sftp/trigger-1.png)</span></span>  
2. <span data-ttu-id="55450-104">**파일을 추가하거나 수정할 때** 컨트롤이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="55450-104">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="55450-105">![SFTP 트리거 이미지 2](./media/connectors-create-api-sftp/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="55450-105">![SFTP trigger image 2](./media/connectors-create-api-sftp/trigger-2.png)</span></span>  
3. <span data-ttu-id="55450-106">컨트롤의 오른쪽에 있는 **...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55450-106">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="55450-107">이렇게 하면 폴더 선택 컨트롤이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="55450-107">This opens the folder picker control</span></span>  
   <span data-ttu-id="55450-108">![SFTP 트리거 이미지 3](./media/connectors-create-api-sftp/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="55450-108">![SFTP trigger image 3](./media/connectors-create-api-sftp/action-1.png)</span></span>  
4. <span data-ttu-id="55450-109">**SFTP** 를 선택하여 새롭거나 수정된 파일을 모니터링할 폴더로 루트 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55450-109">Select the **SFTP** to select the root folder as the folder to monitor for new or modified files.</span></span> <span data-ttu-id="55450-110">이제 루트 폴더는 **폴더** 컨트롤에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="55450-110">Notice the root folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="55450-111">![SFTP 트리거 이미지 4](./media/connectors-create-api-sftp/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="55450-111">![SFTP trigger image 4](./media/connectors-create-api-sftp/action-2.png)</span></span>   

<span data-ttu-id="55450-112">이제, 논리 앱은 파일이 특정 SFTP 폴더에서 수정되거나 만들어질 때 워크플로의 다른 트리거 및 동작의 실행을 시작하는 트리거로 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55450-112">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific SFTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="55450-113">논리 앱이 작동하려면 하나 이상의 트리거와 동작이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55450-113">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="55450-114">다음 섹션의 단계에 따라 동작을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="55450-114">Follow the steps in the next section to add an action.</span></span>  
> 
> 

