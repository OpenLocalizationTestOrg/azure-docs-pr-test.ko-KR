---
title: "aaaAzure Analysis Services 데이터베이스 백업 및 복원 | Microsoft Docs"
description: "설명 방법을 toobackup 및 복원 Azure Analysis Services 데이터베이스입니다."
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
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="644e0-103">백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="644e0-103">Backup and restore</span></span>

<span data-ttu-id="644e0-104">온-프레미스 Analysis Services의 경우와 동일 hello 많은 Azure Analysis Services의 테이블 형식 모델 데이터베이스를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-104">Backing up tabular model databases in Azure Analysis Services is much hello same as for on-premises Analysis Services.</span></span> <span data-ttu-id="644e0-105">hello 주요 차이점은 백업 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-105">hello primary difference is where you store your backup files.</span></span> <span data-ttu-id="644e0-106">백업 파일을 tooa 컨테이너에 저장 된 [Azure 저장소 계정](../storage/common/storage-create-storage-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-106">Backup files must be saved tooa container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="644e0-107">이미 있는 저장소 계정과 컨테이너를 사용하거나 서버에 대한 저장소 설정을 구성할 때 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="644e0-108">저장소 계정을 만들면 새로운 유료 서비스가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="644e0-109">toolearn 더 참조 [Azure 저장소 가격](https://azure.microsoft.com/pricing/details/storage/blobs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-109">toolearn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="644e0-110">백업은 abf 확장명으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="644e0-111">메모리 내 테이블 형식 모델의 경우 모델 데이터와 메타데이터가 모두 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="644e0-112">DirectQuery 테이블 형식 모델의 경우 모델 메타데이터만 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="644e0-113">백업 압축 및 암호화, 선택한 hello 옵션에 따라 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-113">Backups can be compressed and encrypted, depending on hello options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="644e0-114">저장소 설정 구성</span><span class="sxs-lookup"><span data-stu-id="644e0-114">Configure storage settings</span></span>
<span data-ttu-id="644e0-115">를 백업 하기 전에 서버에 대 한 tooconfigure 저장소 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-115">Before backing up, you need tooconfigure storage settings for your server.</span></span>


### <a name="tooconfigure-storage-settings"></a><span data-ttu-id="644e0-116">tooconfigure 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="644e0-116">tooconfigure storage settings</span></span>
1.  <span data-ttu-id="644e0-117">Azure Portal > **설정**에서 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![설정의 백업](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="644e0-119">**사용**을 클릭한 다음 **저장소 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![사용](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="644e0-121">저장소 계정을 선택하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="644e0-122">컨테이너를 선택하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-122">Select a container or create a new one.</span></span>

    ![컨테이너 선택](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="644e0-124">백업 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-124">Save your backup settings.</span></span>

    ![백업 설정 저장](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="644e0-126">백업</span><span class="sxs-lookup"><span data-stu-id="644e0-126">Backup</span></span>

### <a name="toobackup-by-using-ssms"></a><span data-ttu-id="644e0-127">SSMS를 사용 하 여 toobackup</span><span class="sxs-lookup"><span data-stu-id="644e0-127">toobackup by using SSMS</span></span>

1. <span data-ttu-id="644e0-128">SSMS에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="644e0-129">**데이터베이스 백업** > **백업 파일**에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="644e0-130">Hello에 **파일 저장** 대화 상자에서 hello 폴더 경로 확인 하 고 hello 백업 파일에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-130">In hello **Save file as** dialog, verify hello folder path, and then type a name for hello backup file.</span></span> 

4. <span data-ttu-id="644e0-131">Hello에 **Backup Database** 대화 상자에서 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-131">In hello **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="644e0-132">**파일 덮어쓰기** -hello의이 옵션 toooverwrite 백업 파일을 선택 합니다. 이름이 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-132">**Allow file overwrite** - Select this option toooverwrite backup files of hello same name.</span></span> <span data-ttu-id="644e0-133">이 옵션을 선택 하지 않으면 저장 하는 hello 파일 가질 수 없습니다 이름과 같은 이름을 hello에에서 이미 있는 hello 동일한 파일로 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-133">If this option is not selected, hello file you are saving cannot have hello same name as a file that already exists in hello same location.</span></span>

    <span data-ttu-id="644e0-134">**압축 적용** -이 옵션 toocompress hello 백업 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-134">**Apply compression** - Select this option toocompress hello backup file.</span></span> <span data-ttu-id="644e0-135">백업 파일을 압축하면 디스크 공간은 절약되지만 CPU 사용률이 약간 더 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="644e0-136">**백업 파일을 암호화** -이 옵션 tooencrypt hello 백업 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-136">**Encrypt backup file** - Select this option tooencrypt hello backup file.</span></span> <span data-ttu-id="644e0-137">이 옵션에는 사용자가 제공한 암호 toosecure hello 백업 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-137">This option requires a user-supplied password toosecure hello backup file.</span></span> <span data-ttu-id="644e0-138">hello 암호 복원 작업 이외의 다른 도구를 hello 백업 데이터의 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-138">hello password prevents reading of hello backup data any other means than a restore operation.</span></span> <span data-ttu-id="644e0-139">Tooencrypt 백업을 선택 하면 hello 암호를 안전한 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-139">If you choose tooencrypt backups, store hello password in a safe location.</span></span>

5. <span data-ttu-id="644e0-140">클릭 **확인** toocreate hello 백업 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-140">Click **OK** toocreate and save hello backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="644e0-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="644e0-141">PowerShell</span></span>
<span data-ttu-id="644e0-142">[Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="644e0-143">복원</span><span class="sxs-lookup"><span data-stu-id="644e0-143">Restore</span></span>
<span data-ttu-id="644e0-144">를 복원할 때는 백업 파일이 서버에 구성 된 hello 저장소 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-144">When restoring, your backup file must be in hello storage account you've configured for your server.</span></span> <span data-ttu-id="644e0-145">Toomove는 온-프레미스 위치 tooyour 저장소 계정에서 백업 파일을 필요한 경우 사용 [Microsoft Azure 저장소 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) 또는 hello [AzCopy](../storage/common/storage-use-azcopy.md) 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-145">If you need toomove a backup file from an on-premises location tooyour storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or hello [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="644e0-146">Hello 모델의 역할에서 모든 hello에 대 한 도메인 사용자가 제거 하 고 추가할 해야 온-프레미스 서버에서 복원 하는 경우 Azure Active Directory 사용자로 toohello 역할을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-146">If you're restoring from an on-premises server, you must remove all hello domain users from hello model's roles and add them back toohello roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="toorestore-by-using-ssms"></a><span data-ttu-id="644e0-147">SSMS를 사용 하 여 toorestore</span><span class="sxs-lookup"><span data-stu-id="644e0-147">toorestore by using SSMS</span></span>

1. <span data-ttu-id="644e0-148">SSMS에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="644e0-149">Hello에 **Backup Database** 대화에 **백업 파일**, 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-149">In hello **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="644e0-150">Hello에 **데이터베이스 파일 찾기** 대화 상자에서 원하는 toorestore 선택 hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-150">In hello **Locate Database Files** dialog, select hello file you want toorestore.</span></span>

4. <span data-ttu-id="644e0-151">**데이터베이스 복원**선택, hello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-151">In **Restore database**, select hello database.</span></span>

5. <span data-ttu-id="644e0-152">옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-152">Specify options.</span></span> <span data-ttu-id="644e0-153">보안 옵션을 백업할 때 사용한 hello 백업 옵션 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-153">Security options must match hello backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="644e0-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="644e0-154">PowerShell</span></span>

<span data-ttu-id="644e0-155">[Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="644e0-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="644e0-156">관련 정보</span><span class="sxs-lookup"><span data-stu-id="644e0-156">Related information</span></span>

[<span data-ttu-id="644e0-157">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="644e0-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="644e0-158">[고가용성](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="644e0-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="644e0-159">Azure Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="644e0-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
