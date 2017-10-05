---
title: "Azure Backup에 대한 보고서 구성"
description: "이 문서에서는 Recovery Services 자격 증명 모음을 사용하여 Azure Backup에 대한 Power BI 보고서를 구성하는 방법을 설명합니다."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 86e465f1-8996-4a40-b582-ccf75c58ab87
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4629665e6fbe26c26eb45af7509de338367c4e18
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-backup-reports"></a><span data-ttu-id="480b9-103">Azure Backup 보고서 구성</span><span class="sxs-lookup"><span data-stu-id="480b9-103">Configure Azure Backup reports</span></span>
<span data-ttu-id="480b9-104">이 문서에서는 Recovery Services 자격 증명 모음을 사용하여 Azure Backup에 대한 보고서를 구성하고 Power BI를 사용하여 이러한 보고서에 액세스하는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-104">This article talks about steps to configure reports for Azure Backup using Recovery Services vault, and  to access these reports using Power BI.</span></span> <span data-ttu-id="480b9-105">이러한 단계를 수행한 후 Power BI로 직접 이동하여 모든 보고서를 확인하고, 보고서를 사용자 지정 및 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-105">After performing these steps, you can directly go to Power BI to view all the reports, customize and create reports.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="480b9-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="480b9-106">Supported scenarios</span></span>
1. <span data-ttu-id="480b9-107">Azure Backup 보고서는 Azure Recovery Services 에이전트를 사용한 클라우드로 파일/폴더 백업 및 Azure 가상 컴퓨터 백업에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-107">Azure Backup reports are supported for Azure virtual machine backup and file/folder backup to cloud using Azure Recovery Services Agent.</span></span>
2. <span data-ttu-id="480b9-108">Azure SQL, DPM 및 Azure Backup Server에 대한 보고서는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-108">Reports for Azure SQL, DPM and Azure Backup Server are not supported at this time.</span></span>
3. <span data-ttu-id="480b9-109">각 자격 증명 모음에 대해 동일한 저장소 계정이 구성된 경우 여러 자격 증명 모음과 구독의 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-109">You can view reports across vaults and across subscriptions, if same storage account is configured for each of the vaults.</span></span> <span data-ttu-id="480b9-110">선택한 저장소 계정이 Recovery Services 자격 증명 모음과 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-110">Storage account selected should be in the same region as recovery services vault.</span></span>
4. <span data-ttu-id="480b9-111">Power BI에서 보고서에 대해 예약된 새로 고침 빈도는 24시간입니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-111">The frequency of scheduled refresh for the reports is 24 hours in Power BI.</span></span> <span data-ttu-id="480b9-112">Power BI에서 보고서의 임시 새로 고침을 수행할 수도 있으며, 이 경우 고객 저장소 계정의 최신 데이터가 보고서 렌더링에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-112">You can also perform an ad-hoc refresh of the reports in Power BI, in which case latest data in customer storage account is used for rendering reports.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="480b9-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="480b9-113">Prerequisites</span></span>
1. <span data-ttu-id="480b9-114">[Azure 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account)을 만들어 보고서에 대해 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-114">Create an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to configure it for reports.</span></span> <span data-ttu-id="480b9-115">이 저장소 계정은 보고서 관련 데이터를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-115">This storage account is used for storing reports related data.</span></span>
2. <span data-ttu-id="480b9-116">[Power BI 계정을 만들어](https://powerbi.microsoft.com/landing/signin/) Power BI 포털에서 보고서를 확인, 사용자 지정 및 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-116">[Create a Power BI account](https://powerbi.microsoft.com/landing/signin/) to view, customize, and create your own reports using Power BI portal.</span></span>
3. <span data-ttu-id="480b9-117">아직 등록되지 않은 경우 리소스 공급자 **Microsoft.insights**를 저장소 계정 구독 및 Recovery Services 자격 증명 모음 구독에 등록하여 보고 데이터가 저장소 계정으로 흐르도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-117">Register the resource provider **Microsoft.insights** if not registered already, with the subscription of storage account and also with the subscription of Recovery Services vault to enable reporting data to flow to the storage account.</span></span> <span data-ttu-id="480b9-118">동일한 작업을 수행하려면 Azure Portal > 구독 > 리소스 공급자로 이동한 다음 이 공급자를 선택해서 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-118">To do the same, you must go to Azure portal > Subscription > Resource providers and check for this provider to register it.</span></span> 

## <a name="configure-storage-account-for-reports"></a><span data-ttu-id="480b9-119">보고서에 대한 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="480b9-119">Configure storage account for reports</span></span>
<span data-ttu-id="480b9-120">Azure Portal을 사용하여 Recovery Services 자격 증명 모음에 대한 저장소 계정을 구성하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="480b9-120">Use the following steps to configure the storage account for recovery services vault using Azure portal.</span></span> <span data-ttu-id="480b9-121">이는 일회성 구성이며 저장소 계정이 구성되면 Power BI로 직접 이동하여 콘텐츠 팩을 확인하고 보고서를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-121">This is a one-time configuration and once storage account is configured, you can go to Power BI directly to view content pack and leverage reports.</span></span>
1. <span data-ttu-id="480b9-122">이미 Recovery Services 자격 증명 모음이 열려 있으면 다음 단계로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-122">If you already have a Recovery Services vault open, proceed to next step.</span></span> <span data-ttu-id="480b9-123">복구 서비스 자격 증명 모음이 열려 있지 않지만 Azure 포털에 있는 경우 허브 메뉴에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-123">If you do not have a Recovery Services vault open, but are in the Azure portal, on the Hub menu, click **Browse**.</span></span>

   * <span data-ttu-id="480b9-124">리소스 목록에서 **복구 서비스**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-124">In the list of resources, type **Recovery Services**.</span></span>
   * <span data-ttu-id="480b9-125">입력을 시작하면 입력한 내용을 바탕으로 목록이 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-125">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="480b9-126">**복구 서비스 자격 증명 모음**이 표시되면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-126">When you see **Recovery Services vaults**, click it.</span></span>

      ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     <span data-ttu-id="480b9-128">복구 서비스 자격 증명 모음의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-128">The list of Recovery Services vaults appears.</span></span> <span data-ttu-id="480b9-129">복구 서비스 자격 증명 모음의 목록에서 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-129">From the list of Recovery Services vaults, select a vault.</span></span>

     <span data-ttu-id="480b9-130">선택한 자격 증명 모음 대시보드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-130">The selected vault dashboard opens.</span></span>
2. <span data-ttu-id="480b9-131">자격 증명 모음 아래에 나타나는 항목 목록에서 모니터링 및 보고서 섹션 아래의 **백업 보고서**를 클릭하여 보고서에 대한 저장소 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-131">From the list of items that appears under vault, click **Backup Reports** under Monitoring and Reports section to configure the storage account for reports.</span></span>

      ![백업 보고서 메뉴 항목 선택 2단계](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. <span data-ttu-id="480b9-133">백업 보고서 블레이드에서 **구성** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-133">On the Backup Reports blade, click **Configure** button.</span></span> <span data-ttu-id="480b9-134">고객 저장소 계정에 데이터를 푸시하는 데 사용되는 Azure Application Insights 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-134">This opens the Azure Application Insights blade which is used for pushing data to customer storage account.</span></span>

      ![저장소 계정 구성 3단계](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. <span data-ttu-id="480b9-136">상태 토글 단추를 **켜기**로 설정하고 **저장소 계정에 보관** 확인란을 선택하여 보고 데이터가 저장소 계정으로 흐르기 시작하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-136">Set the Status toggle button to **On** and select **Archive to a Storage Account** check box so that reporting data can start flowing in to the storage account.</span></span>

      ![진단 사용 4단계](./media/backup-azure-configure-reports/set-status-on.png)
5. <span data-ttu-id="480b9-138">저장소 계정 선택을 클릭하고 목록에서 보고 데이터를 저장하는 데 사용할 저장소 계정을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-138">Click Storage Account picker and select the storage account from the list for storing reporting data and click **OK**.</span></span>

      ![저장소 계정 선택 5단계](./media/backup-azure-configure-reports/select-storage-account.png)
6. <span data-ttu-id="480b9-140">**AzureBackupReport** 확인란을 선택하고 슬라이더를 이동하여 이 보고 데이터의 보존 기간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-140">Select **AzureBackupReport** check box and also move the slider to select retention period for this reporting data.</span></span> <span data-ttu-id="480b9-141">저장소 계정의 보고 데이터는 이 슬라이더를 사용하여 선택한 기간 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-141">Reporting data in the storage account is kept for the period selected using this slider.</span></span>

      ![저장소 계정 선택 6단계](./media/backup-azure-configure-reports/save-configuration.png)
7. <span data-ttu-id="480b9-143">모든 변경 내용을 검토하고 위 그림에 표시된, 맨 위의 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-143">Review all the changes and click **Save** button on top, as shown in the figure above.</span></span> <span data-ttu-id="480b9-144">이 작업을 수행하면 모든 변경 내용이 저장되며, 이제 보고 데이터를 저장하는 데 사용할 저장소 계정이 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-144">This action ensures that all your changes are saved and storage account is now configured for storing reporting data.</span></span>

> [!NOTE]
> <span data-ttu-id="480b9-145">저장소 계정을 저장하여 보고서를 구성한 후에는 초기 데이터 푸시가 완료될 때까지 **24시간 동안 대기**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-145">Once you configure reports by saving storage account, you should **wait for 24 hours** for initial data push to complete.</span></span> <span data-ttu-id="480b9-146">이 시간 이후에만 Power BI에서 Azure Backup 콘텐츠 팩을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-146">You should import Azure Backup content pack in Power BI only after that time.</span></span> <span data-ttu-id="480b9-147">자세한 내용은 [FAQ 섹션](#frequently-asked-questions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="480b9-147">Refer [FAQ section](#frequently-asked-questions) for futher details.</span></span> 
>
>

## <a name="view-reports-in-power-bi"></a><span data-ttu-id="480b9-148">Power BI에서 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="480b9-148">View reports in Power BI</span></span> 
<span data-ttu-id="480b9-149">Recovery Services 자격 증명 모음을 사용하여 보고서에 대한 저장소 계정을 구성한 후 보고 데이터가 흐름을 시작하기까지 약 24시간 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-149">After configuring storage account for reports using recovery services vault, it takes around 24 hours for reporting data to start flowing in.</span></span> <span data-ttu-id="480b9-150">저장소 계정을 설정하고 24시간 후에 Power BI에서 보고서를 보려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="480b9-150">After 24 hours of setting up storage account, use the following steps to view reports in Power BI:</span></span>
1. <span data-ttu-id="480b9-151">Power BI에 [로그인](https://powerbi.microsoft.com/landing/signin/)합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-151">[Sign in](https://powerbi.microsoft.com/landing/signin/) to Power BI.</span></span>
2. <span data-ttu-id="480b9-152">**데이터 가져오기**를 클릭한 다음 콘텐츠 팩 라이브러리의 **서비스**에서 가져오기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-152">Click **Get Data** and click Get under **Services** in Content Pack Library.</span></span> <span data-ttu-id="480b9-153">[콘텐츠 팩에 액세스하려면 Power BI 설명서](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/)에 있는 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="480b9-153">Use steps mentioned in [Power BI documentation to access content pack](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/).</span></span>

     ![콘텐츠 팩 가져오기](./media/backup-azure-configure-reports/content-pack-import.png)
3. <span data-ttu-id="480b9-155">검색 창에서 **Azure Backup**을 입력하고 **지금 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-155">Type **Azure Backup** in Search bar and click **Get it now**.</span></span>

      ![콘텐츠 팩 가져오기](./media/backup-azure-configure-reports/content-pack-get.png)
4. <span data-ttu-id="480b9-157">위의 5단계에서 구성한 저장소 계정 이름을 입력하고 **다음** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-157">Enter the storage account name configured in step 5 above and click **Next** button.</span></span>

    ![저장소 계정 이름 입력](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. <span data-ttu-id="480b9-159">이 저장소 계정에 대한 저장소 계정 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-159">Enter the storage account key for this storage account.</span></span> <span data-ttu-id="480b9-160">Azure Portal에서 저장소 계정으로 이동하면 [저장소 액세스 키를 확인하고 복사](../storage/common/storage-create-storage-account.md#manage-your-storage-account)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-160">You can [view and copy storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account) by navigating to your storage account in Azure portal.</span></span> 

     ![저장소 계정 입력](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. <span data-ttu-id="480b9-162">**로그인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-162">Click **Sign in** button.</span></span> <span data-ttu-id="480b9-163">로그인에 성공하면 **데이터를 가져오는 중** 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-163">After sign-in is successful, you get **Importing data** notification.</span></span>

    ![콘텐츠 팩 가져오기](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    <span data-ttu-id="480b9-165">일정 시간 후에 가져오기가 완료되면 **성공** 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-165">After some time, you get **Success** notification after the import is complete.</span></span> <span data-ttu-id="480b9-166">저장소 계정에 많은 데이터가 있는 경우 콘텐츠 팩을 가져오는 데 시간이 좀 더 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-166">It might take little longer to import the content pack, if there is a lot of data in the storage account.</span></span>
    
    ![콘텐츠 팩 가져오기 성공](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. <span data-ttu-id="480b9-168">데이터를 성공적으로 가져왔으면 **Azure Backup** 콘텐츠 팩이 탐색 창의 **앱**에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-168">Once data is imported successfully, **Azure Backup** content pack is visible in **Apps** in the navigation pane.</span></span> <span data-ttu-id="480b9-169">이제 목록에 Azure Backup 대시보드, 보고서 및 데이터 집합이 나타나고 새로 가져온 보고서에는 노란색 별이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-169">The list now shows Azure Backup dashboard, reports, and dataset with a yellow star indicating newly imported reports.</span></span> 

     ![Azure Backup 콘텐츠 팩](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. <span data-ttu-id="480b9-171">대시보드에서 **Azure Backup**을 클릭합니다. 일련의 고정 키 보고서가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-171">Click **Azure Backup** under Dashboards, which shows a set of pinned key reports.</span></span>

      ![Azure Backup 대시보드](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. <span data-ttu-id="480b9-173">전체 보고서 집합을 보려면 대시보드에서 아무 보고서나 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-173">To view the complete set of reports, click any report in the dashboard.</span></span>

      ![Azure Backup 작업 상태](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. <span data-ttu-id="480b9-175">보고서의 각 탭을 클릭하여 해당 영역의 보고서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-175">Click each tab in the reports to view reports in that area.</span></span>

      ![Azure Backup 보고서 탭](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a><span data-ttu-id="480b9-177">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="480b9-177">Frequently asked questions</span></span>
1. <span data-ttu-id="480b9-178">**보고 데이터가 저장소 계정으로 흐름기 시작했는지 확인하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="480b9-178">**How do I check if reporting data has started flowing in to storage account?**</span></span>
    
    <span data-ttu-id="480b9-179">구성된 저장소 계정으로 이동한 다음 컨테이너를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-179">You can go to the storage account configured and select containers.</span></span> <span data-ttu-id="480b9-180">컨테이너에 insights-logs-azurebackupreport에 대한 항목이 있으면 보고 데이터가 흐르기 시작한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-180">If the container has an entry for insights-logs-azurebackupreport, it indicates that reporting data has started flowing in.</span></span>

2. <span data-ttu-id="480b9-181">**Power BI에서 Azure Backup 콘텐츠 팩 및 저장소 계정으로 데이터 푸시가 수행되는 빈도는 어느 정도인가요?**</span><span class="sxs-lookup"><span data-stu-id="480b9-181">**What is the frequency of data push to storage account and Azure Backup content pack in Power BI?**</span></span>

   <span data-ttu-id="480b9-182">0일 사용자의 경우 저장소 계정에 데이터를 푸시하는 데 약 24시간 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-182">For Day 0 users, it would take around 24 hours to push data to storage account.</span></span> <span data-ttu-id="480b9-183">이 초기 푸시가 완료된 후에는 아래 그림에 표시된 빈도로 데이터가 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-183">Once this initial push is compelete, data is refreshed with the following frequency shown in the figure below.</span></span> 
      * <span data-ttu-id="480b9-184">**작업, 경고, 백업 항목, 자격 증명 모음, 보호된 서버 및 정책**과 관련된 데이터는 기록 시 고객 저장소 계정에 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-184">Data related to **Jobs, Alerts, Backup Items, Vaults, Protected Servers and Policies** is pushed to customer storage account as and when it is logged.</span></span>
      * <span data-ttu-id="480b9-185">**저장소**와 관련된 데이터는 24시간마다 고객 저장소 계정에 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-185">Data related to **Storage** is pushed to customer storage account every 24 hours.</span></span>
   
    ![Azure Backup 보고서 데이터 푸시 빈도](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  <span data-ttu-id="480b9-187">Power BI에는 [하루에 한 번 예약된 새로 고침](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-187">Power BI has a [scheduled refresh once a day](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed).</span></span> <span data-ttu-id="480b9-188">Power BI에서 콘텐츠 팩에 대한 데이터를 수동으로 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-188">You can perform a manual refresh of the data in Power BI for the content pack.</span></span>

3. <span data-ttu-id="480b9-189">**보고서를 유지할 수 있는 기간은 어느 정도인가요?**</span><span class="sxs-lookup"><span data-stu-id="480b9-189">**How long can I retain the reports?**</span></span> 

   <span data-ttu-id="480b9-190">저장소 계정을 구성하는 동안 저장소 계정의 보고 데이터 보존 기간을 선택할 수 있습니다(위의 보고서에 대한 저장소 계정 구성 섹션에서 6단계 사용).</span><span class="sxs-lookup"><span data-stu-id="480b9-190">While configuring storage account, you can select retention period of reporting data in the storage account (using step 6 in Configure storage account for reports section above).</span></span> <span data-ttu-id="480b9-191">뿐만 아니라 [Excel에서 보고서를 분석](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/)하고 요구에 따라 더 오랜 보존 기간 동안 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-191">Besides that, you can [Analyze reports in excel](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/) and save them for a longer retention period, as per your needs.</span></span> 

4. <span data-ttu-id="480b9-192">**저장소 계정을 구성하면 보고서에서 내 데이터를 모두 볼 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="480b9-192">**Will I see all my data in reports after configuring the storage account?**</span></span>

   <span data-ttu-id="480b9-193">**"저장소 계정을 구성"**한 후 생성된 모든 데이터는 저장소 계정에 푸시되며 보고서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-193">All the data generated after **"configuring storage account"** will be pushed to the storage account and will be available in reports.</span></span> <span data-ttu-id="480b9-194">그러나 **진행 중인 작업은 보고를 위해 푸시되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="480b9-194">However, **In Progress Jobs are not pushed** for Reporting.</span></span> <span data-ttu-id="480b9-195">작업이 완료되거나 실패하면 보고서에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-195">Once the job completes or fails, it is sent to reports.</span></span>

5. <span data-ttu-id="480b9-196">**보고서를 보는 데 사용할 저장소 계정을 이미 구성한 경우 다른 저장소 계정을 사용하도록 구성을 변경할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="480b9-196">**If I have already configured the storage account to view reports, can I change the configuration to use another storage account?**</span></span> 

   <span data-ttu-id="480b9-197">예, 다른 저장소 계정을 가리키도록 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-197">Yes, you can change the configuration to point to a different storage account.</span></span> <span data-ttu-id="480b9-198">Azure Backup 콘텐츠 팩에 연결하는 동안 새로 구성된 저장소 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-198">You should use the newly configured storage account while connecting to Azure Backup content pack.</span></span> <span data-ttu-id="480b9-199">또한 다른 저장소 계정이 구성된 후 새 데이터는 이 저장소 계정으로 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-199">Also, once a different storage account is configured, new data would flow in this storage account.</span></span> <span data-ttu-id="480b9-200">하지만 구성을 변경하기 전의 오래된 데이터는 계속해서 이전 저장소 계정에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-200">But older data (before changing the configuration) would still remain in the older storage account.</span></span>

6. <span data-ttu-id="480b9-201">**여러 자격 증명 모음 및 구독의 보고서를 볼 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="480b9-201">**Can I view reports across vaults and across subscriptions?**</span></span> 

   <span data-ttu-id="480b9-202">예, 다양한 자격 증명 모음에 동일한 저장소 계정을 구성하여 자격 증명 모음 간 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-202">Yes, you can configure the same storage account across various vaults to view cross-vault reports.</span></span> <span data-ttu-id="480b9-203">여러 구독의 자격 증명 모음에 대해 동일한 저장소 계정을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-203">Also, you can configure the same storage account for vaults across subscriptions.</span></span> <span data-ttu-id="480b9-204">그런 다음 Power BI에서 Azure Backup 콘텐츠 팩에 연결하는 동안 이 저장소 계정을 사용하여 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-204">You can then use this storage account while connecting to Azure Backup content pack in Power BI to view the reports.</span></span> <span data-ttu-id="480b9-205">그러나 선택한 저장소 계정이 Recovery Services 자격 증명 모음과 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-205">However, the storage account selected should be in the same region as recovery services vault.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="480b9-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="480b9-206">Next steps</span></span>
<span data-ttu-id="480b9-207">이제 저장소 계정을 구성하고 Azure Backup 콘텐츠 팩을 가져왔으므로 다음 단계는 이러한 보고서를 사용자 지정하고 보고 데이터 모델을 사용하여 보고서를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="480b9-207">Now that you have configured the storage account and imported Azure Backup content pack, the next step is to customize these reports and use reporting data model to create reports.</span></span> <span data-ttu-id="480b9-208">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="480b9-208">Refer the following articles for more details.</span></span>

* [<span data-ttu-id="480b9-209">Azure Backup 보고 데이터 모델 사용</span><span class="sxs-lookup"><span data-stu-id="480b9-209">Using Azure Backup reporting data model</span></span>](backup-azure-reports-data-model.md)
* [<span data-ttu-id="480b9-210">Power BI에서 보고서 필터링</span><span class="sxs-lookup"><span data-stu-id="480b9-210">Filtering reports in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [<span data-ttu-id="480b9-211">Power BI에서 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="480b9-211">Creating reports in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

