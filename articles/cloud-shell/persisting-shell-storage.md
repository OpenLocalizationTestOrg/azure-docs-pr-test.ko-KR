---
title: "Azure 클라우드 셸에서 (미리 보기) aaaPersist 파일 | Microsoft Docs"
description: "Azure Cloud Shell에서 파일을 유지하는 방법의 연습입니다."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="5bdee-103">Azure Cloud Shell에서 파일 유지</span><span class="sxs-lookup"><span data-stu-id="5bdee-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="5bdee-104">클라우드 셸에서는 세션 전반에 걸쳐 Azure 파일 저장소 toopersist 파일 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-104">Cloud Shell takes advantage of Azure File storage toopersist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="5bdee-105">`clouddrive` 파일 공유 설정</span><span class="sxs-lookup"><span data-stu-id="5bdee-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="5bdee-106">처음 시작 시 클라우드 셸 묻는 메시지를 기존 또는 새 파일 공유를 통해 파일을 toopersist 세션 tooassociate 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-106">On initial start, Cloud Shell prompts you tooassociate a new or existing file share toopersist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="5bdee-107">새 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="5bdee-107">Create new storage</span></span>

<span data-ttu-id="5bdee-108">기본 설정을 사용 하 고만 구독을 선택 하는 경우 클라우드 셸 가장 tooyou 가까이 있는 hello 지원 영역에 사용자 대신 세 개의 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in hello supported region that's nearest tooyou:</span></span>
* <span data-ttu-id="5bdee-109">리소스 그룹: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="5bdee-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="5bdee-110">저장소 계정: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="5bdee-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="5bdee-111">파일 공유: `cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="5bdee-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![hello 구독 설정](media/basic-storage.png)

<span data-ttu-id="5bdee-113">hello 파일 공유로 탑재할 `clouddrive` 에 프로그램 `$Home` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-113">hello file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="5bdee-114">hello 파일 공유는도 자동으로 및에 대해 만들어지는 5GB 이미지를 업데이트 하 고 계속 되 면 사용 되는 toostore 프로그램 `$Home` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-114">hello file share is also used toostore a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="5bdee-115">이 일회성 작업 이므로 이후의 세션 hello 파일 공유를 자동으로 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-115">This is a one-time action, and hello file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="5bdee-116">기존 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="5bdee-116">Use existing resources</span></span>

<span data-ttu-id="5bdee-117">고급 옵션 hello를 사용 하 여 기존 리소스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-117">By using hello advanced option, you can associate existing resources.</span></span> <span data-ttu-id="5bdee-118">Hello 저장소 설정 프롬프트가 나타나면 선택 **고급 설정 표시** tooview 추가 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-118">When hello storage setup prompt appears, select **Show advanced settings** tooview additional options.</span></span> <span data-ttu-id="5bdee-119">기존 파일 공유 5GB 사용자 이미지 toopersist 수신 프로그램 `$Home` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-119">Existing file shares receive a 5-GB user image toopersist your `$Home` directory.</span></span> <span data-ttu-id="5bdee-120">로컬 중복 및 지리적 중복 저장소 계정의 및 클라우드 셸 영역에 대 한 hello 드롭 다운 메뉴 필터링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-120">hello drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![hello 리소스 그룹 설정](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="5bdee-122">Azure 리소스 정책으로 리소스 만들기 제한</span><span class="sxs-lookup"><span data-stu-id="5bdee-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="5bdee-123">Cloud Shell에서 생성된 저장소 계정에 `ms-resource-usage:azure-cloud-shell` 태그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="5bdee-124">클라우드 셸에서 저장소 계정을 만들지 못하도록 toodisallow 사용자 만듭니다는 [태그에 대 한 Azure 리소스 정책](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) 이 특정 태그에 의해 트리거되는입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-124">If you want toodisallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="5bdee-125">Cloud Shell 작동 방식</span><span class="sxs-lookup"><span data-stu-id="5bdee-125">How Cloud Shell works</span></span>
<span data-ttu-id="5bdee-126">클라우드 셸 모두 hello 다음 메서드를 통해 파일을 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-126">Cloud Shell persists files through both of hello following methods:</span></span>
* <span data-ttu-id="5bdee-127">디스크 이미지를 만들어 프로그램 `$Home` hello 디렉터리 내에서 모든 디렉터리 toopersist 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-127">Creating a disk image of your `$Home` directory toopersist all contents within hello directory.</span></span> <span data-ttu-id="5bdee-128">hello 디스크 이미지 사용자 지정 된 파일 공유에 저장 된 `acc_<User>.img` 에서 `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, 변경 내용을 자동으로 동기화 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-128">hello disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="5bdee-129">직접 파일 공유의 상호 작용을 위해 `$Home` 디렉터리에서 지정된 파일 공유를 `clouddrive`로 마운트합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="5bdee-130">`/Home/<User>/clouddrive`너무 매핑된`fileshare.storage.windows.net/fileshare`합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-130">`/Home/<User>/clouddrive` is mapped too`fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="5bdee-131">SSH 키와 같이 `$Home` 디렉터리의 모든 파일은 마운트된 파일 공유에 저장된 사용자 디스크 이미지에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="5bdee-132">`$Home` 디렉터리 및 마운트된 파일 공유에서 정보를 유지하는 경우 모범 사례를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-hello-clouddrive-command"></a><span data-ttu-id="5bdee-133">사용 하 여 hello `clouddrive` 명령</span><span class="sxs-lookup"><span data-stu-id="5bdee-133">Use hello `clouddrive` command</span></span>
<span data-ttu-id="5bdee-134">클라우드 셸을 사용 하 여 호출 하는 명령을 실행할 수 있습니다 `clouddrive`, 어떤 있습니다 toomanually 업데이트 hello 파일 공유는 탑재 된 tooCloud 셸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you toomanually update hello file share that's mounted tooCloud Shell.</span></span>
<span data-ttu-id="5bdee-135">![Hello "clouddrive" 명령을 실행합니다.](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="5bdee-135">![Running hello "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="5bdee-136">새 `clouddrive` 마운트</span><span class="sxs-lookup"><span data-stu-id="5bdee-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="5bdee-137">수동 마운트를 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="5bdee-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="5bdee-138">Hello를 사용 하 여 클라우드 셸와 관련 된 hello 파일 공유를 업데이트할 수 있습니다 `clouddrive mount` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-138">You can update hello file share that's associated with Cloud Shell by using hello `clouddrive mount` command.</span></span>

<span data-ttu-id="5bdee-139">기존 파일 공유를 탑재 하는 경우 hello 저장소 계정은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-139">If you mount an existing file share, hello storage accounts must be:</span></span>
* <span data-ttu-id="5bdee-140">로컬 중복 저장소 또는 지역 중복 저장소 toosupport 파일을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-140">Locally-redundant storage or geo-redundant storage toosupport file shares.</span></span>
* <span data-ttu-id="5bdee-141">할당된 지역에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-141">Located in your assigned region.</span></span> <span data-ttu-id="5bdee-142">온 보 딩을 hello 영역 할당 된 경우 hello 리소스 그룹 이름에 나열 된 toois `cloud-shell-storage-<region>`합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-142">When you are onboarding, hello region you are assigned toois listed in hello resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="5bdee-143">지원되는 저장소 지역</span><span class="sxs-lookup"><span data-stu-id="5bdee-143">Supported storage regions</span></span>
<span data-ttu-id="5bdee-144">hello Azure 파일에에서 있어야 hello 동일 하도록 탑재 하는 hello 클라우드 셸 컴퓨터와 지역의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-144">hello Azure files must reside in hello same region as hello Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="5bdee-145">클라우드 셸 클러스터는 현재 hello 다음 영역에에서 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-145">Cloud Shell clusters currently exist in hello following regions:</span></span>
|<span data-ttu-id="5bdee-146">영역</span><span class="sxs-lookup"><span data-stu-id="5bdee-146">Area</span></span>|<span data-ttu-id="5bdee-147">지역</span><span class="sxs-lookup"><span data-stu-id="5bdee-147">Region</span></span>|
|---|---|
|<span data-ttu-id="5bdee-148">아메리카</span><span class="sxs-lookup"><span data-stu-id="5bdee-148">Americas</span></span>|<span data-ttu-id="5bdee-149">미국 동부, 미국 중남부, 미국 서부</span><span class="sxs-lookup"><span data-stu-id="5bdee-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="5bdee-150">유럽</span><span class="sxs-lookup"><span data-stu-id="5bdee-150">Europe</span></span>|<span data-ttu-id="5bdee-151">북유럽, 서유럽</span><span class="sxs-lookup"><span data-stu-id="5bdee-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="5bdee-152">아시아 태평양</span><span class="sxs-lookup"><span data-stu-id="5bdee-152">Asia Pacific</span></span>|<span data-ttu-id="5bdee-153">인도 중부, 동남 아시아</span><span class="sxs-lookup"><span data-stu-id="5bdee-153">India Central, Southeast Asia</span></span>|

### <a name="hello-clouddrive-mount-command"></a><span data-ttu-id="5bdee-154">hello `clouddrive mount` 명령</span><span class="sxs-lookup"><span data-stu-id="5bdee-154">hello `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="5bdee-155">새 사용자 이미지에 대해 만든 새 파일 공유를 탑재 하는 경우 프로그램 `$Home` 디렉터리 때문에 이전 `$Home` hello 이전 파일 공유에 유지 되는 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in hello previous file share.</span></span>

<span data-ttu-id="5bdee-156">Hello 실행 `clouddrive mount` 명령 hello 매개 변수 뒤에:</span><span class="sxs-lookup"><span data-stu-id="5bdee-156">Run hello `clouddrive mount` command with hello following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="5bdee-157">자세한 내용은 실행 tooview `clouddrive mount -h`여기 표시 된 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="5bdee-157">tooview more details, run `clouddrive mount -h`, as shown here:</span></span>

![실행 중인 hello ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="5bdee-159">`clouddrive` 마운트 해제</span><span class="sxs-lookup"><span data-stu-id="5bdee-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="5bdee-160">파일 공유는 탑재 된 tooCloud 셸 언제 든 지 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-160">You can unmount a file share that's mounted tooCloud Shell at any time.</span></span> <span data-ttu-id="5bdee-161">파일 공유를 탑재 됩니다 증명된 toomount 새 파일 공유 이전 tooyour 다음 세션.</span><span class="sxs-lookup"><span data-stu-id="5bdee-161">Once your file share is unmounted, you will be prompted toomount a new file share prior tooyour next session.</span></span>

<span data-ttu-id="5bdee-162">클라우드 셸에서 tooremove 파일을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-162">tooremove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="5bdee-163">`clouddrive unmount`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="5bdee-164">승인 하 고 hello 메시지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-164">Acknowledge and confirm hello prompts.</span></span>

<span data-ttu-id="5bdee-165">파일 공유는 수동으로 삭제 하지 않는 한 tooexist를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-165">Your file share will continue tooexist unless you delete it manually.</span></span> <span data-ttu-id="5bdee-166">Cloud Shell은 후속 세션에서 이 파일 공유를 더 이상 검색하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="5bdee-167">자세한 내용은 실행 tooview `clouddrive unmount -h`여기 표시 된 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="5bdee-167">tooview more details, run `clouddrive unmount -h`, as shown here:</span></span>

![실행 중인 hello ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="5bdee-169">이 명령을 실행하면 리소스가 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="5bdee-170">셸 영구적으로 삭제 됩니다 tooCloud 매핑된 리소스 그룹, 저장소 계정 또는 파일 공유를 수동으로 삭제 하면 `$Home` 이미지 디렉터리 및 파일 공유에서 다른 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-170">Manually deleting a resource group, storage account, or file share that is mapped tooCloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="5bdee-171">이 작업은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="5bdee-172">`clouddrive` 파일 공유 나열</span><span class="sxs-lookup"><span data-stu-id="5bdee-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="5bdee-173">사용할 파일 공유로 탑재 됩니다 toodiscover `clouddrive`, hello 다음 실행 `df` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-173">toodiscover which file share is mounted as `clouddrive`, run hello following `df` command.</span></span> 

<span data-ttu-id="5bdee-174">hello 파일 경로 tooclouddrive hello URL에서 공유 하는 저장소 계정 이름 및 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-174">hello file path tooclouddrive shows your storage account name and file share in hello URL.</span></span> <span data-ttu-id="5bdee-175">예를 들어 `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="5bdee-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a><span data-ttu-id="5bdee-176">로컬 파일 tooCloud 셸 전송</span><span class="sxs-lookup"><span data-stu-id="5bdee-176">Transfer local files tooCloud Shell</span></span>
<span data-ttu-id="5bdee-177">hello `clouddrive` hello Azure 포털 저장소 블레이드와 디렉터리 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-177">hello `clouddrive` directory syncs with hello Azure portal storage blade.</span></span> <span data-ttu-id="5bdee-178">이 블레이드 tootransfer 로컬 파일 tooor 파일 공유에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-178">Use this blade tootransfer local files tooor from your file share.</span></span> <span data-ttu-id="5bdee-179">클라우드 셸 내에서 파일을 업데이트 hello 블레이드를 새로 고칠 때 hello 파일 저장소 GUI에에서 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-179">Updating files from within Cloud Shell is reflected in hello file storage GUI when you refresh hello blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="5bdee-180">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="5bdee-180">Download files</span></span>

![로컬 파일 목록](media/download.png)
1. <span data-ttu-id="5bdee-182">Azure 포털 hello toohello 탑재 된 파일 공유를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-182">In hello Azure portal, go toohello mounted file share.</span></span>
2. <span data-ttu-id="5bdee-183">Hello 대상 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-183">Select hello target file.</span></span>
3. <span data-ttu-id="5bdee-184">선택 hello **다운로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-184">Select hello **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="5bdee-185">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="5bdee-185">Upload files</span></span>

![로컬 파일 toobe 업로드](media/upload.png)
1. <span data-ttu-id="5bdee-187">Tooyour 탑재 된 파일 공유를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-187">Go tooyour mounted file share.</span></span>
2. <span data-ttu-id="5bdee-188">선택 hello **업로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-188">Select hello **Upload** button.</span></span>
3. <span data-ttu-id="5bdee-189">Hello 파일 또는 tooupload 원하는 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-189">Select hello file or files that you want tooupload.</span></span>
4. <span data-ttu-id="5bdee-190">Hello 업로드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-190">Confirm hello upload.</span></span>

<span data-ttu-id="5bdee-191">이제 표시 hello 파일에 액세스할 수 있는 프로그램 `clouddrive` 클라우드 셸에서 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5bdee-191">You should now see hello files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bdee-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5bdee-192">Next steps</span></span>
[<span data-ttu-id="5bdee-193">Cloud Shell 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="5bdee-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="5bdee-194">
[Azure File Storage에 대해 알아보기](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="5bdee-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="5bdee-195">
[저장소 태그에 대해 알아보기](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="5bdee-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
