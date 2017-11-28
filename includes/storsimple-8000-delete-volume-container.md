<!--author=alkohli last changed: 01/13/17-->

<span data-ttu-id="c68ec-101">볼륨 컨테이너가 볼륨에 연결된 경우 해당 볼륨을 먼저 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-101">If the volume container has associated volumes, take those volumes offline first.</span></span> <span data-ttu-id="c68ec-102">[볼륨을 오프라인으로 전환](../articles/storsimple/storsimple-manage-volumes.md#take-a-volume-offline)단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-102">Follow the steps in [Take a volume offline](../articles/storsimple/storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="c68ec-103">볼륨이 오프라인이 되면 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-103">After the volumes are offline, you can delete them.</span></span> <span data-ttu-id="c68ec-104">볼륨 컨테이너에 연결된 볼륨이 없으면 볼륨 컨테이너를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-104">When the volume container has no associated volumes, delete the volume container.</span></span> <span data-ttu-id="c68ec-105">볼륨 컨테이너를 삭제하려면 다음 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-105">Perform the following procedure to delete a volume container.</span></span>

#### <a name="to-delete-a-volume-container"></a><span data-ttu-id="c68ec-106">볼륨 컨테이너를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="c68ec-106">To delete a volume container</span></span>
1. <span data-ttu-id="c68ec-107">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-107">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="c68ec-108">장치를 선택하여 클릭하고 **설정 > 관리 > 볼륨 컨테이너**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-108">Select and click the device and then go to **Settings > Manage > Volume containers**.</span></span>

    ![볼륨 컨테이너 블레이드](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

2. <span data-ttu-id="c68ec-110">테이블 형식의 볼륨 컨테이너 목록에서 삭제하려는 볼륨 컨테이너를 선택하고 **...**를 마우스 오른쪽 단추로 클릭한 후 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-110">From the tabular list of volume containers, select the volume container you want to delete, right click **...** and then select **Delete**.</span></span>

    ![볼륨 컨테이너 삭제](./media/storsimple-8000-delete-volume-container/deletevolumecontainer1.png)

3. <span data-ttu-id="c68ec-112">볼륨 컨테이너에 연결된 볼륨이 없으면 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-112">If a volume container has no associated volumes, then it can be deleted.</span></span> <span data-ttu-id="c68ec-113">확인 대화 상자가 나타나면 볼륨 컨테이너를 삭제한 결과를 설명하는 확인란을 검토 및 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-113">When prompted for confirmation, review and select the checkbox stating the impact of deleting the volume container.</span></span> <span data-ttu-id="c68ec-114">**삭제**를 클릭하면 볼륨 컨테이너가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-114">Click **Delete** to then delete the volume container.</span></span>

    ![삭제 확인](./media/storsimple-8000-delete-volume-container/deletevolumecontainer2.png)

<span data-ttu-id="c68ec-116">삭제된 볼륨 컨테이너를 반영하도록 볼륨 컨테이너 목록이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="c68ec-116">The list of volume containers is updated to reflect the deleted volume container.</span></span>

![](./media/storsimple-8000-delete-volume-container/deletevolumecontainer5.png)


