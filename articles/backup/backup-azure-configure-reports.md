---
title: "Azure 백업에 대 한 aaaConfigure 보고서"
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
ms.openlocfilehash: 503a240b36ea999e0fea434b6a50d26ddf7677bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-backup-reports"></a><span data-ttu-id="562f1-103">Azure Backup 보고서 구성</span><span class="sxs-lookup"><span data-stu-id="562f1-103">Configure Azure Backup reports</span></span>
<span data-ttu-id="562f1-104">이 문서 발언 단계 tooconfigure 보고서에 대 한 복구 서비스 자격 증명 모음 및 tooaccess를 사용 하 여 Azure 백업에 대 한 Power BI를 사용 하 여 이러한 보고서.</span><span class="sxs-lookup"><span data-stu-id="562f1-104">This article talks about steps tooconfigure reports for Azure Backup using Recovery Services vault, and  tooaccess these reports using Power BI.</span></span> <span data-ttu-id="562f1-105">다음이 단계를 수행한 후 있습니다 수 직접 tooPower BI tooview 모든 hello 보고서를 이동, 사용자 지정 보고서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-105">After performing these steps, you can directly go tooPower BI tooview all hello reports, customize and create reports.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="562f1-106">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="562f1-106">Supported scenarios</span></span>
1. <span data-ttu-id="562f1-107">Azure 백업 보고서는 Azure 가상 컴퓨터 백업 및 파일/폴더 백업 toocloud Azure 복구 서비스 에이전트를 사용 하 여에 대 한 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-107">Azure Backup reports are supported for Azure virtual machine backup and file/folder backup toocloud using Azure Recovery Services Agent.</span></span>
2. <span data-ttu-id="562f1-108">Azure SQL, DPM 및 Azure Backup Server에 대한 보고서는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-108">Reports for Azure SQL, DPM and Azure Backup Server are not supported at this time.</span></span>
3. <span data-ttu-id="562f1-109">볼 수 있습니다 보고서 및 구독, 자격 증명 모음에서 동일한 저장소 계정이 각 hello 자격 증명 모음에 대해 구성 된 경우.</span><span class="sxs-lookup"><span data-stu-id="562f1-109">You can view reports across vaults and across subscriptions, if same storage account is configured for each of hello vaults.</span></span> <span data-ttu-id="562f1-110">선택한 저장소 계정 hello에 있어야 합니다. 동일한 지역 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-110">Storage account selected should be in hello same region as recovery services vault.</span></span>
4. <span data-ttu-id="562f1-111">hello 보고서에 대 한 예정 된 새로 고침 빈도 hello에는 Power BI에서 24 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-111">hello frequency of scheduled refresh for hello reports is 24 hours in Power BI.</span></span> <span data-ttu-id="562f1-112">Power bi에서 보고서를 렌더링 하기 위한 고객 저장소 계정에서 최신 데이터를 사례을 사용 하는 hello 보고서의 임시 새로 고침을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-112">You can also perform an ad-hoc refresh of hello reports in Power BI, in which case latest data in customer storage account is used for rendering reports.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="562f1-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="562f1-113">Prerequisites</span></span>
1. <span data-ttu-id="562f1-114">만들기는 [Azure 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooconfigure에 대해 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-114">Create an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooconfigure it for reports.</span></span> <span data-ttu-id="562f1-115">이 저장소 계정은 보고서 관련 데이터를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-115">This storage account is used for storing reports related data.</span></span>
2. <span data-ttu-id="562f1-116">[Power BI 계정을 만듭니다](https://powerbi.microsoft.com/landing/signin/) tooview, 사용자 지정 하 고 Power BI 포털을 사용 하 여 보고서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-116">[Create a Power BI account](https://powerbi.microsoft.com/landing/signin/) tooview, customize, and create your own reports using Power BI portal.</span></span>
3. <span data-ttu-id="562f1-117">Hello 리소스 공급자 등록이 **Microsoft.insights** 등록 되어 있지 이미 저장소 계정의 hello 구독 및 복구 서비스의 hello 구독과 자격 증명 모음에 tooenable tooflow toohello 데이터를 보고 합니다. 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-117">Register hello resource provider **Microsoft.insights** if not registered already, with hello subscription of storage account and also with hello subscription of Recovery Services vault tooenable reporting data tooflow toohello storage account.</span></span> <span data-ttu-id="562f1-118">동일한 toodo hello, tooAzure 포털 야 합니다. > 구독 > 리소스 공급자와 공급자 tooregister이에 대 한 확인 것입니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-118">toodo hello same, you must go tooAzure portal > Subscription > Resource providers and check for this provider tooregister it.</span></span> 

## <a name="configure-storage-account-for-reports"></a><span data-ttu-id="562f1-119">보고서에 대한 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="562f1-119">Configure storage account for reports</span></span>
<span data-ttu-id="562f1-120">Azure 포털을 사용 하 여 복구 서비스 자격 증명 모음에 대 한 단계 tooconfigure hello 저장소 계정을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-120">Use hello following steps tooconfigure hello storage account for recovery services vault using Azure portal.</span></span> <span data-ttu-id="562f1-121">이것은 일회성 구성 하 고 저장소 계정이 구성 되 면 보고서 tooview 콘텐츠 팩 및 활용 하 여 직접 tooPower BI 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-121">This is a one-time configuration and once storage account is configured, you can go tooPower BI directly tooview content pack and leverage reports.</span></span>
1. <span data-ttu-id="562f1-122">복구 서비스 자격 증명 모음 열고 이미 있는 경우 toonext 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-122">If you already have a Recovery Services vault open, proceed toonext step.</span></span> <span data-ttu-id="562f1-123">복구 서비스 자격 증명 모음 열기를 갖지 않는 hello hello 허브 메뉴에서 Azure 포털에 있지만 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-123">If you do not have a Recovery Services vault open, but are in hello Azure portal, on hello Hub menu, click **Browse**.</span></span>

   * <span data-ttu-id="562f1-124">Hello 리소스 목록에 입력 **복구 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-124">In hello list of resources, type **Recovery Services**.</span></span>
   * <span data-ttu-id="562f1-125">입력을 시작할 때 hello 사용자 입력에 따라 필터를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-125">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="562f1-126">**복구 서비스 자격 증명 모음**이 표시되면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-126">When you see **Recovery Services vaults**, click it.</span></span>

      ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     <span data-ttu-id="562f1-128">복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-128">hello list of Recovery Services vaults appears.</span></span> <span data-ttu-id="562f1-129">복구 서비스 자격 증명 모음 hello 목록에서 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-129">From hello list of Recovery Services vaults, select a vault.</span></span>

     <span data-ttu-id="562f1-130">hello 선택한 자격 증명 모음 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-130">hello selected vault dashboard opens.</span></span>
2. <span data-ttu-id="562f1-131">Hello 목록에서 항목의 자격 증명 모음 아래에 나타나는 클릭 **백업 보고서** 모니터링 및 보고서 섹션 tooconfigure hello 저장소 계정에서 보고서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-131">From hello list of items that appears under vault, click **Backup Reports** under Monitoring and Reports section tooconfigure hello storage account for reports.</span></span>

      ![백업 보고서 메뉴 항목 선택 2단계](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. <span data-ttu-id="562f1-133">Hello 백업 보고서 블레이드에서 클릭 **구성** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-133">On hello Backup Reports blade, click **Configure** button.</span></span> <span data-ttu-id="562f1-134">Toocustomer 저장소 계정의 데이터를 밀어 넣는 데 사용 되는 hello Azure Application Insights 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-134">This opens hello Azure Application Insights blade which is used for pushing data toocustomer storage account.</span></span>

      ![저장소 계정 구성 3단계](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. <span data-ttu-id="562f1-136">너무 hello 상태 토글 단추가 설정**에** 선택 **보관 저장소 계정 tooa** 확인란을 선택 하 여 데이터 흐름 toohello 저장소 계정에 시작할 수를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-136">Set hello Status toggle button too**On** and select **Archive tooa Storage Account** check box so that reporting data can start flowing in toohello storage account.</span></span>

      ![진단 사용 4단계](./media/backup-azure-configure-reports/set-status-on.png)
5. <span data-ttu-id="562f1-138">저장소 계정 선택 및 보고 데이터와 클릭을 저장 하는 것에 대 한 hello 목록에서 선택 hello 저장소 계정을 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-138">Click Storage Account picker and select hello storage account from hello list for storing reporting data and click **OK**.</span></span>

      ![저장소 계정 선택 5단계](./media/backup-azure-configure-reports/select-storage-account.png)
6. <span data-ttu-id="562f1-140">선택 **AzureBackupReport** 확인란을 선택 하 고도 hello 슬라이더 tooselect 보존 기간이에 대 한 이동 데이터를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-140">Select **AzureBackupReport** check box and also move hello slider tooselect retention period for this reporting data.</span></span> <span data-ttu-id="562f1-141">Hello 저장소 계정의 데이터를에서 보고이 슬라이더를 사용 하 여 선택 하는 hello 기간 동안 보관 됩니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-141">Reporting data in hello storage account is kept for hello period selected using this slider.</span></span>

      ![저장소 계정 선택 6단계](./media/backup-azure-configure-reports/save-configuration.png)
7. <span data-ttu-id="562f1-143">모든 hello 변경 내용을 검토 하 고 클릭 **저장** 위의 hello 그림에 나와 있는 것 처럼 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-143">Review all hello changes and click **Save** button on top, as shown in hello figure above.</span></span> <span data-ttu-id="562f1-144">이 작업을 수행하면 모든 변경 내용이 저장되며, 이제 보고 데이터를 저장하는 데 사용할 저장소 계정이 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-144">This action ensures that all your changes are saved and storage account is now configured for storing reporting data.</span></span>

> [!NOTE]
> <span data-ttu-id="562f1-145">저장소 계정을 저장 하 여 보고서를 구성 하 고 나면 해야 **24 시간 동안 대기** 푸시 toocomplete 초기 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-145">Once you configure reports by saving storage account, you should **wait for 24 hours** for initial data push toocomplete.</span></span> <span data-ttu-id="562f1-146">이 시간 이후에만 Power BI에서 Azure Backup 콘텐츠 팩을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-146">You should import Azure Backup content pack in Power BI only after that time.</span></span> <span data-ttu-id="562f1-147">자세한 내용은 [FAQ 섹션](#frequently-asked-questions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="562f1-147">Refer [FAQ section](#frequently-asked-questions) for futher details.</span></span> 
>
>

## <a name="view-reports-in-power-bi"></a><span data-ttu-id="562f1-148">Power BI에서 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="562f1-148">View reports in Power BI</span></span> 
<span data-ttu-id="562f1-149">복구 서비스 자격 증명 모음을 사용 하 여 보고서에 대 한 저장소 계정을 구성 하는 후에 약 24 시간 정도의 흐름에 데이터 toostart 보고용 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-149">After configuring storage account for reports using recovery services vault, it takes around 24 hours for reporting data toostart flowing in.</span></span> <span data-ttu-id="562f1-150">저장소 계정 설정의 24 시간 후 사용 하 여 hello 다음 Power BI의 보고서 tooview 단계:</span><span class="sxs-lookup"><span data-stu-id="562f1-150">After 24 hours of setting up storage account, use hello following steps tooview reports in Power BI:</span></span>
1. <span data-ttu-id="562f1-151">[로그인](https://powerbi.microsoft.com/landing/signin/) tooPower BI 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-151">[Sign in](https://powerbi.microsoft.com/landing/signin/) tooPower BI.</span></span>
2. <span data-ttu-id="562f1-152">**데이터 가져오기**를 클릭한 다음 콘텐츠 팩 라이브러리의 **서비스**에서 가져오기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-152">Click **Get Data** and click Get under **Services** in Content Pack Library.</span></span> <span data-ttu-id="562f1-153">언급 한 단계를 사용 하 여 [설명서 tooaccess Power BI 콘텐츠 팩](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/)합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-153">Use steps mentioned in [Power BI documentation tooaccess content pack](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/).</span></span>

     ![콘텐츠 팩 가져오기](./media/backup-azure-configure-reports/content-pack-import.png)
3. <span data-ttu-id="562f1-155">검색 창에서 **Azure Backup**을 입력하고 **지금 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-155">Type **Azure Backup** in Search bar and click **Get it now**.</span></span>

      ![콘텐츠 팩 가져오기](./media/backup-azure-configure-reports/content-pack-get.png)
4. <span data-ttu-id="562f1-157">위의 5 단계에서 구성 된 hello 저장소 계정 이름을 입력 하 고 클릭 **다음** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-157">Enter hello storage account name configured in step 5 above and click **Next** button.</span></span>

    ![저장소 계정 이름 입력](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. <span data-ttu-id="562f1-159">이 저장소 계정에 대 한 hello 저장소 계정 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-159">Enter hello storage account key for this storage account.</span></span> <span data-ttu-id="562f1-160">있습니다 수 [표시 및 저장소 액세스 키를 복사](../storage/common/storage-create-storage-account.md#manage-your-storage-account) Azure 포털에서 저장소 계정의 tooyour 이동 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-160">You can [view and copy storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account) by navigating tooyour storage account in Azure portal.</span></span> 

     ![저장소 계정 입력](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. <span data-ttu-id="562f1-162">**로그인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-162">Click **Sign in** button.</span></span> <span data-ttu-id="562f1-163">로그인에 성공하면 **데이터를 가져오는 중** 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-163">After sign-in is successful, you get **Importing data** notification.</span></span>

    ![콘텐츠 팩 가져오기](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    <span data-ttu-id="562f1-165">가져올 일정 시간이 지난 후 **성공** hello 가져오기가 완료 된 후에 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-165">After some time, you get **Success** notification after hello import is complete.</span></span> <span data-ttu-id="562f1-166">Hello 저장소 계정에는 데이터의 많은 있는 경우 거의 긴 tooimport hello 콘텐츠 팩을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-166">It might take little longer tooimport hello content pack, if there is a lot of data in hello storage account.</span></span>
    
    ![콘텐츠 팩 가져오기 성공](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. <span data-ttu-id="562f1-168">데이터를 성공적으로 가져온 후 **Azure 백업** 콘텐츠 팩을 볼 수 있으면 **앱** hello 탐색 창에서.</span><span class="sxs-lookup"><span data-stu-id="562f1-168">Once data is imported successfully, **Azure Backup** content pack is visible in **Apps** in hello navigation pane.</span></span> <span data-ttu-id="562f1-169">hello 목록 새로 가져온된 보고서 나타내는 노란색 별이 있는 Azure 백업 대시보드, 보고서 및 데이터 집합을 이제 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-169">hello list now shows Azure Backup dashboard, reports, and dataset with a yellow star indicating newly imported reports.</span></span> 

     ![Azure Backup 콘텐츠 팩](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. <span data-ttu-id="562f1-171">대시보드에서 **Azure Backup**을 클릭합니다. 일련의 고정 키 보고서가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-171">Click **Azure Backup** under Dashboards, which shows a set of pinned key reports.</span></span>

      ![Azure Backup 대시보드](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. <span data-ttu-id="562f1-173">tooview hello 전체 보고서를 집합 hello 대시보드에서 임의의 보고서를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-173">tooview hello complete set of reports, click any report in hello dashboard.</span></span>

      ![Azure Backup 작업 상태](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. <span data-ttu-id="562f1-175">해당 영역의 hello 보고서 tooview 보고서의 각 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-175">Click each tab in hello reports tooview reports in that area.</span></span>

      ![Azure Backup 보고서 탭](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a><span data-ttu-id="562f1-177">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="562f1-177">Frequently asked questions</span></span>
1. <span data-ttu-id="562f1-178">**보고 데이터 흐름 toostorage 계정에 시작 된 경우 확인 방법**</span><span class="sxs-lookup"><span data-stu-id="562f1-178">**How do I check if reporting data has started flowing in toostorage account?**</span></span>
    
    <span data-ttu-id="562f1-179">Toohello 저장소를 이동할 수 있습니다 계정 구성 및 선택 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-179">You can go toohello storage account configured and select containers.</span></span> <span data-ttu-id="562f1-180">Hello 컨테이너 insights-로그-azurebackupreport에 대 한 항목이 있으면, 보고 데이터가 시작 되었음을 흐름 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-180">If hello container has an entry for insights-logs-azurebackupreport, it indicates that reporting data has started flowing in.</span></span>

2. <span data-ttu-id="562f1-181">**데이터 푸시 toostorage 계정 및 Azure 백업에서 Power BI 콘텐츠 팩의 hello 주파수 이란?**</span><span class="sxs-lookup"><span data-stu-id="562f1-181">**What is hello frequency of data push toostorage account and Azure Backup content pack in Power BI?**</span></span>

   <span data-ttu-id="562f1-182">Day 0 사용자에 대 한 약 24 시간 동안 toopush 데이터 toostorage 계정을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-182">For Day 0 users, it would take around 24 hours toopush data toostorage account.</span></span> <span data-ttu-id="562f1-183">이 초기 푸시 compelete 되 면 아래 hello 그림에 표시 된 빈도 따라 hello로 데이터가 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-183">Once this initial push is compelete, data is refreshed with hello following frequency shown in hello figure below.</span></span> 
      * <span data-ttu-id="562f1-184">데이터가 너무 관련**작업, 경고, 백업 항목, 자격 증명 모음, 보호 된 서버 및 정책** 으로 toocustomer 저장소 계정 및 기록 되는 경우 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-184">Data related too**Jobs, Alerts, Backup Items, Vaults, Protected Servers and Policies** is pushed toocustomer storage account as and when it is logged.</span></span>
      * <span data-ttu-id="562f1-185">데이터가 너무 관련**저장소** 24 시간 마다 toocustomer 저장소 계정 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-185">Data related too**Storage** is pushed toocustomer storage account every 24 hours.</span></span>
   
    ![Azure Backup 보고서 데이터 푸시 빈도](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  <span data-ttu-id="562f1-187">Power BI에는 [하루에 한 번 예약된 새로 고침](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-187">Power BI has a [scheduled refresh once a day](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed).</span></span> <span data-ttu-id="562f1-188">Power BI에서 콘텐츠 팩 hello에 대 한 hello 데이터 수동 새로 고침을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-188">You can perform a manual refresh of hello data in Power BI for hello content pack.</span></span>

3. <span data-ttu-id="562f1-189">**Hello 보고서를 유지할 수는 기간**</span><span class="sxs-lookup"><span data-stu-id="562f1-189">**How long can I retain hello reports?**</span></span> 

   <span data-ttu-id="562f1-190">저장소 계정, 구성 하는 동안 hello 저장소 계정 (위의 보고서 섹션에 대 한 구성 저장소 계정에서 6 단계를 사용)에서 보고 데이터의 보존 기간을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-190">While configuring storage account, you can select retention period of reporting data in hello storage account (using step 6 in Configure storage account for reports section above).</span></span> <span data-ttu-id="562f1-191">뿐만 아니라 [Excel에서 보고서를 분석](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/)하고 요구에 따라 더 오랜 보존 기간 동안 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-191">Besides that, you can [Analyze reports in excel](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/) and save them for a longer retention period, as per your needs.</span></span> 

4. <span data-ttu-id="562f1-192">**Hello 저장소 계정을 구성한 후 보고서의 내 모든 데이터를 볼 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="562f1-192">**Will I see all my data in reports after configuring hello storage account?**</span></span>

   <span data-ttu-id="562f1-193">모든 이후 생성 된 데이터를 hello **"저장소 계정 구성"** toohello 저장소 계정 밀어넣습니다 및 보고서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-193">All hello data generated after **"configuring storage account"** will be pushed toohello storage account and will be available in reports.</span></span> <span data-ttu-id="562f1-194">그러나 **진행 중인 작업은 보고를 위해 푸시되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="562f1-194">However, **In Progress Jobs are not pushed** for Reporting.</span></span> <span data-ttu-id="562f1-195">Hello 작업 완료 또는 실패를 일단 tooreports를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-195">Once hello job completes or fails, it is sent tooreports.</span></span>

5. <span data-ttu-id="562f1-196">**이미 hello 저장소 계정 tooview 보고서를 구성 하려면 경우 변경 hello 구성 toouse 다른 저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="562f1-196">**If I have already configured hello storage account tooview reports, can I change hello configuration toouse another storage account?**</span></span> 

   <span data-ttu-id="562f1-197">예, hello 구성 toopoint tooa 다른 저장소 계정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-197">Yes, you can change hello configuration toopoint tooa different storage account.</span></span> <span data-ttu-id="562f1-198">TooAzure 백업에 대 한 콘텐츠 팩을 연결 하는 동안 hello 새로 구성 된 저장소 계정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-198">You should use hello newly configured storage account while connecting tooAzure Backup content pack.</span></span> <span data-ttu-id="562f1-199">또한 다른 저장소 계정이 구성된 후 새 데이터는 이 저장소 계정으로 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-199">Also, once a different storage account is configured, new data would flow in this storage account.</span></span> <span data-ttu-id="562f1-200">하지만 hello 구성 변경) (이전 오래 된 데이터는 여전히 hello 이전 저장소 계정에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-200">But older data (before changing hello configuration) would still remain in hello older storage account.</span></span>

6. <span data-ttu-id="562f1-201">**여러 자격 증명 모음 및 구독의 보고서를 볼 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="562f1-201">**Can I view reports across vaults and across subscriptions?**</span></span> 

   <span data-ttu-id="562f1-202">예, hello를 구성할 수 있습니다 동일한 저장소 계정에서 다양 한 tooview 크로스-자격 증명 모음 보고서 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-202">Yes, you can configure hello same storage account across various vaults tooview cross-vault reports.</span></span> <span data-ttu-id="562f1-203">구성할 수는 또한 구독에서 동일한 저장소 계정 자격 증명 모음에 대 한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-203">Also, you can configure hello same storage account for vaults across subscriptions.</span></span> <span data-ttu-id="562f1-204">다음 백업 tooAzure tooview hello Power BI 보고서의 콘텐츠 팩을 연결 하는 동안이 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-204">You can then use this storage account while connecting tooAzure Backup content pack in Power BI tooview hello reports.</span></span> <span data-ttu-id="562f1-205">하지만 Hello에 hello 저장소 계정을 선택 해야 동일한 지역 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-205">However, hello storage account selected should be in hello same region as recovery services vault.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="562f1-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="562f1-206">Next steps</span></span>
<span data-ttu-id="562f1-207">이제 hello 저장소 계정 및 Azure 백업 콘텐츠 팩을 가져온된, hello 다음 단계를 사용 하도록 구성한입니다 toocustomize 이러한 보고서 및 데이터 모델 toocreate 보고서를 보고 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="562f1-207">Now that you have configured hello storage account and imported Azure Backup content pack, hello next step is toocustomize these reports and use reporting data model toocreate reports.</span></span> <span data-ttu-id="562f1-208">Hello 문서에 대 한 자세한 내용은 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="562f1-208">Refer hello following articles for more details.</span></span>

* [<span data-ttu-id="562f1-209">Azure Backup 보고 데이터 모델 사용</span><span class="sxs-lookup"><span data-stu-id="562f1-209">Using Azure Backup reporting data model</span></span>](backup-azure-reports-data-model.md)
* [<span data-ttu-id="562f1-210">Power BI에서 보고서 필터링</span><span class="sxs-lookup"><span data-stu-id="562f1-210">Filtering reports in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [<span data-ttu-id="562f1-211">Power BI에서 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="562f1-211">Creating reports in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

