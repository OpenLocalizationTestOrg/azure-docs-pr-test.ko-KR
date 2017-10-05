---
title: "Azure Analysis Services 데이터베이스 백업 및 복원 | Microsoft Docs"
description: "Azure Analysis Services 데이터베이스를 백업하고 복원하는 방법에 대해 설명합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: bffa481a498b130ef1f2388a5ba856da5d164ee0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="1ff04-103">백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="1ff04-103">Backup and restore</span></span>

<span data-ttu-id="1ff04-104">Azure Analysis Services에서 테이블 형식 모델 데이터베이스를 백업하는 것은 온-프레미스 Analysis Services의 경우와 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-104">Backing up tabular model databases in Azure Analysis Services is much the same as for on-premises Analysis Services.</span></span> <span data-ttu-id="1ff04-105">주요 차이점은 백업 파일을 저장하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-105">The primary difference is where you store your backup files.</span></span> <span data-ttu-id="1ff04-106">백업 파일은 [Azure Storage 계정](../storage/common/storage-create-storage-account.md)의 컨테이너에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-106">Backup files must be saved to a container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="1ff04-107">이미 있는 저장소 계정과 컨테이너를 사용하거나 서버에 대한 저장소 설정을 구성할 때 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="1ff04-108">저장소 계정을 만들면 새로운 유료 서비스가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="1ff04-109">자세한 내용은 [Azure Storage 가격](https://azure.microsoft.com/pricing/details/storage/blobs/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff04-109">To learn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="1ff04-110">백업은 abf 확장명으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="1ff04-111">메모리 내 테이블 형식 모델의 경우 모델 데이터와 메타데이터가 모두 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="1ff04-112">DirectQuery 테이블 형식 모델의 경우 모델 메타데이터만 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="1ff04-113">백업은 선택한 옵션에 따라 압축하고 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-113">Backups can be compressed and encrypted, depending on the options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="1ff04-114">저장소 설정 구성</span><span class="sxs-lookup"><span data-stu-id="1ff04-114">Configure storage settings</span></span>
<span data-ttu-id="1ff04-115">백업하기 전에 서버에 대해 저장소 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-115">Before backing up, you need to configure storage settings for your server.</span></span>


### <a name="to-configure-storage-settings"></a><span data-ttu-id="1ff04-116">저장소 설정을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="1ff04-116">To configure storage settings</span></span>
1.  <span data-ttu-id="1ff04-117">Azure Portal > **설정**에서 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![설정의 백업](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="1ff04-119">**사용**을 클릭한 다음 **저장소 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![사용](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="1ff04-121">저장소 계정을 선택하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="1ff04-122">컨테이너를 선택하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-122">Select a container or create a new one.</span></span>

    ![컨테이너 선택](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="1ff04-124">백업 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-124">Save your backup settings.</span></span>

    ![백업 설정 저장](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="1ff04-126">백업</span><span class="sxs-lookup"><span data-stu-id="1ff04-126">Backup</span></span>

### <a name="to-backup-by-using-ssms"></a><span data-ttu-id="1ff04-127">SSMS를 사용하여 백업하려면</span><span class="sxs-lookup"><span data-stu-id="1ff04-127">To backup by using SSMS</span></span>

1. <span data-ttu-id="1ff04-128">SSMS에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="1ff04-129">**데이터베이스 백업** > **백업 파일**에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="1ff04-130">**다른 이름으로 파일 저장** 대화 상자에서 폴더 경로 확인한 다음 백업 파일의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-130">In the **Save file as** dialog, verify the folder path, and then type a name for the backup file.</span></span> 

4. <span data-ttu-id="1ff04-131">**데이터베이스 백업** 대화 상자에서 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-131">In the **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="1ff04-132">**파일 덮어쓰기 허용** - 이름이 같은 백업 파일을 덮어쓰려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-132">**Allow file overwrite** - Select this option to overwrite backup files of the same name.</span></span> <span data-ttu-id="1ff04-133">이 옵션을 선택하지 않으면 저장하려는 파일에 동일한 위치에 이미 있는 파일과 같은 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-133">If this option is not selected, the file you are saving cannot have the same name as a file that already exists in the same location.</span></span>

    <span data-ttu-id="1ff04-134">**압축 적용** - 백업 파일을 압축하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-134">**Apply compression** - Select this option to compress the backup file.</span></span> <span data-ttu-id="1ff04-135">백업 파일을 압축하면 디스크 공간은 절약되지만 CPU 사용률이 약간 더 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="1ff04-136">**백업 파일 암호화** - 백업 파일을 암호화하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-136">**Encrypt backup file** - Select this option to encrypt the backup file.</span></span> <span data-ttu-id="1ff04-137">이 옵션에서 백업 파일을 보호하려면 사용자가 제공한 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-137">This option requires a user-supplied password to secure the backup file.</span></span> <span data-ttu-id="1ff04-138">암호는 복원 작업 이외의 다른 방법으로 백업 데이터를 읽을 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-138">The password prevents reading of the backup data any other means than a restore operation.</span></span> <span data-ttu-id="1ff04-139">백업을 암호화하도록 선택한 경우 암호를 안전한 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-139">If you choose to encrypt backups, store the password in a safe location.</span></span>

5. <span data-ttu-id="1ff04-140">**확인**을 클릭하여 백업 파일을 만들고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-140">Click **OK** to create and save the backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="1ff04-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ff04-141">PowerShell</span></span>
<span data-ttu-id="1ff04-142">[Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="1ff04-143">복원</span><span class="sxs-lookup"><span data-stu-id="1ff04-143">Restore</span></span>
<span data-ttu-id="1ff04-144">복원할 때 백업 파일은 서버용으로 구성한 저장소 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-144">When restoring, your backup file must be in the storage account you've configured for your server.</span></span> <span data-ttu-id="1ff04-145">온-프레미스 위치에서 저장소 계정으로 백업 파일을 이동해야 하는 경우 [Microsoft Azure Storage 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) 또는 [AzCopy](../storage/common/storage-use-azcopy.md) 명령줄 유틸리티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-145">If you need to move a backup file from an on-premises location to your storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or the [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="1ff04-146">온-프레미스 서버에서 저장하는 경우 모델 역할에서 모든 도메인 사용자를 제거한 후 Azure Active Directory 사용자로 역할에 다시 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-146">If you're restoring from an on-premises server, you must remove all the domain users from the model's roles and add them back to the roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="to-restore-by-using-ssms"></a><span data-ttu-id="1ff04-147">SSMS를 사용하여 복원하려면</span><span class="sxs-lookup"><span data-stu-id="1ff04-147">To restore by using SSMS</span></span>

1. <span data-ttu-id="1ff04-148">SSMS에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="1ff04-149">**데이터베이스 백업** 대화 상자의 **백업 파일**에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-149">In the **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="1ff04-150">**데이터베이스 파일 찾기** 대화 상자에서 복원하려는 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-150">In the **Locate Database Files** dialog, select the file you want to restore.</span></span>

4. <span data-ttu-id="1ff04-151">**데이터베이스 복원**에서 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-151">In **Restore database**, select the database.</span></span>

5. <span data-ttu-id="1ff04-152">옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-152">Specify options.</span></span> <span data-ttu-id="1ff04-153">보안 옵션은 백업할 때 사용한 백업 옵션과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-153">Security options must match the backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="1ff04-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ff04-154">PowerShell</span></span>

<span data-ttu-id="1ff04-155">[Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff04-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="1ff04-156">관련 정보</span><span class="sxs-lookup"><span data-stu-id="1ff04-156">Related information</span></span>

[<span data-ttu-id="1ff04-157">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="1ff04-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="1ff04-158">[고가용성](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="1ff04-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="1ff04-159">Azure Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="1ff04-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
