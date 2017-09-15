## <a name="use-the-azure-portal"></a><span data-ttu-id="36278-101">Azure Portal 사용</span><span class="sxs-lookup"><span data-stu-id="36278-101">Use the Azure portal</span></span>
1. <span data-ttu-id="36278-102">다시 배포하려는 VM을 선택하고 *설정* 블레이드에서 *다시 배포* 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36278-102">Select the VM you wish to redeploy, then select the *Redeploy* button in the *Settings* blade.</span></span> <span data-ttu-id="36278-103">다음 예제와 같이 '다시 배포' 단추가 포함된 **지원 및 문제 해결** 섹션을 보기 위해 아래로 스크롤해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36278-103">You may need to scroll down to see the **Support and Troubleshooting** section that contains the 'Redeploy' button as in the following example:</span></span>
   
    ![Azure VM 블레이드](./media/virtual-machines-common-redeploy-to-new-node/vmoverview.png)
2. <span data-ttu-id="36278-105">작업을 확인하려면 *다시 배포* 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36278-105">To confirm the operation, select the *Redeploy* button:</span></span>
   
    ![VM 다시 배포 블레이드](./media/virtual-machines-common-redeploy-to-new-node/redeployvm.png)
3. <span data-ttu-id="36278-107">VM이 다시 배포 준비가 완료되면 다음 예제와 같이 VM의 **상태**가 *업데이트 중*으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="36278-107">The **Status** of the VM changes to *Updating* as the VM prepares to redeploy, as shown in the following example:</span></span>
   
    ![VM 업데이트 중](./media/virtual-machines-common-redeploy-to-new-node/vmupdating.png)
4. <span data-ttu-id="36278-109">그런 후 새 Azure 호스트에서 VM이 부팅되면 다음 예제와 같이 **상태**가 *시작 중*으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="36278-109">The **Status** then changes to *Starting* as the VM boots up on a new Azure host, as shown in the following example:</span></span>
   
    ![VM 시작 중](./media/virtual-machines-common-redeploy-to-new-node/vmstarting.png)
5. <span data-ttu-id="36278-111">VM이 부팅 프로세스를 완료하면 **상태** 가 *실행 중*으로 돌아가 VM이 정상적으로 다시 배포되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="36278-111">After the VM finishes the boot process, the **Status** then returns to *Running*, indicating the VM has been successfully redeployed:</span></span>
   
    ![VM 실행 중](./media/virtual-machines-common-redeploy-to-new-node/vmrunning.png)

