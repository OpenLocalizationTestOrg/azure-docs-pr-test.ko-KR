---
title: "Azure Cloud Shell에서 파일 유지(미리 보기) | Microsoft Docs"
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
ms.openlocfilehash: 61a8bfcf3704f361432400771d8fcc8b81927b53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="bad25-103">Azure Cloud Shell에서 파일 유지</span><span class="sxs-lookup"><span data-stu-id="bad25-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="bad25-104">Cloud Shell은 Azure 파일 저장소를 활용하여 세션 간에 파일을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-104">Cloud Shell takes advantage of Azure File storage to persist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="bad25-105">`clouddrive` 파일 공유 설정</span><span class="sxs-lookup"><span data-stu-id="bad25-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="bad25-106">처음 시작 시 Cloud Shell은 세션 간에 파일을 유지하기 위해 새 또는 기존 파일 공유를 연결하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-106">On initial start, Cloud Shell prompts you to associate a new or existing file share to persist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="bad25-107">새 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="bad25-107">Create new storage</span></span>

<span data-ttu-id="bad25-108">기본 설정을 사용하고 구독만 선택하면 Cloud Shell은 가장 가까운 지원되는 지역에서 사용자를 대신에 3개 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in the supported region that's nearest to you:</span></span>
* <span data-ttu-id="bad25-109">리소스 그룹: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="bad25-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="bad25-110">저장소 계정: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="bad25-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="bad25-111">파일 공유: `cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="bad25-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![구독 설정](media/basic-storage.png)

<span data-ttu-id="bad25-113">파일 공유는 `$Home` 디렉터리에서 `clouddrive`로 마운트됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-113">The file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="bad25-114">또한 이 파일 공유를 사용하여 만들어진 5GB 이미지를 저장하고 `$Home` 디렉터리를 자동으로 업데이트하고 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-114">The file share is also used to store a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="bad25-115">이것은 일회성 작업이며 파일 공유는 후속 세션에서 자동으로 마운트됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-115">This is a one-time action, and the file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="bad25-116">기존 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="bad25-116">Use existing resources</span></span>

<span data-ttu-id="bad25-117">고급 옵션을 사용하여 기존 리소스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-117">By using the advanced option, you can associate existing resources.</span></span> <span data-ttu-id="bad25-118">저장소 설정 프롬프트가 나타나면 **고급 옵션 표시**를 선택하여 추가 옵션을 봅니다. </span><span class="sxs-lookup"><span data-stu-id="bad25-118">When the storage setup prompt appears, select **Show advanced settings** to view additional options.</span></span> <span data-ttu-id="bad25-119">기존 파일 공유는 `$Home` 디렉터리를 유지하기 위한 5GB 사용자 이미지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-119">Existing file shares receive a 5-GB user image to persist your `$Home` directory.</span></span> <span data-ttu-id="bad25-120">Cloud Shell 지역, 로컬 중복 및 지역 중복 저장소 계정에 대해 드롭다운 메뉴가 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-120">The drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![리소스 그룹 설정](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="bad25-122">Azure 리소스 정책으로 리소스 만들기 제한</span><span class="sxs-lookup"><span data-stu-id="bad25-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="bad25-123">Cloud Shell에서 생성된 저장소 계정에 `ms-resource-usage:azure-cloud-shell` 태그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="bad25-124">사용자가 Cloud Shell에서 저장소 계정을 만드는 것을 허용하지 않으려면 이 특정 태그로 트리거되는 [태그에 대한 Azure 리소스 정책](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-124">If you want to disallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="bad25-125">Cloud Shell 작동 방식</span><span class="sxs-lookup"><span data-stu-id="bad25-125">How Cloud Shell works</span></span>
<span data-ttu-id="bad25-126">Cloud Shell은 다음 방법 모두를 통해 파일을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-126">Cloud Shell persists files through both of the following methods:</span></span>
* <span data-ttu-id="bad25-127">`$Home` 디렉터리 내에 모든 콘텐츠를 유지하기 위해 해당 디렉터리의 디스크 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-127">Creating a disk image of your `$Home` directory to persist all contents within the directory.</span></span> <span data-ttu-id="bad25-128">디스크 이미지는 `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`에서 `acc_<User>.img`로 지정된 파일 공유에 저장되고 변경 내용을 자동으로 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-128">The disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="bad25-129">직접 파일 공유의 상호 작용을 위해 `$Home` 디렉터리에서 지정된 파일 공유를 `clouddrive`로 마운트합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="bad25-130">`/Home/<User>/clouddrive`은 `fileshare.storage.windows.net/fileshare`에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-130">`/Home/<User>/clouddrive` is mapped to `fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="bad25-131">SSH 키와 같이 `$Home` 디렉터리의 모든 파일은 마운트된 파일 공유에 저장된 사용자 디스크 이미지에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="bad25-132">`$Home` 디렉터리 및 마운트된 파일 공유에서 정보를 유지하는 경우 모범 사례를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-the-clouddrive-command"></a><span data-ttu-id="bad25-133">`clouddrive` 명령 사용</span><span class="sxs-lookup"><span data-stu-id="bad25-133">Use the `clouddrive` command</span></span>
<span data-ttu-id="bad25-134">Cloud Shell에서 `clouddrive` 명령을 실행하여 Cloud Shell에 마운트된 파일 공유를 수동으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you to manually update the file share that's mounted to Cloud Shell.</span></span>
<span data-ttu-id="bad25-135">![clouddrive 명령 실행](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="bad25-135">![Running the "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="bad25-136">새 `clouddrive` 마운트</span><span class="sxs-lookup"><span data-stu-id="bad25-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="bad25-137">수동 마운트를 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="bad25-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="bad25-138">`clouddrive mount` 명령을 사용하여 Cloud Shell과 연결된 파일 공유를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-138">You can update the file share that's associated with Cloud Shell by using the `clouddrive mount` command.</span></span>

<span data-ttu-id="bad25-139">기존 파일 공유를 마운트할 경우 저장소 계정은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-139">If you mount an existing file share, the storage accounts must be:</span></span>
* <span data-ttu-id="bad25-140">파일 공유를 지원하는 로컬 중복 저장소 또는 지역 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="bad25-140">Locally-redundant storage or geo-redundant storage to support file shares.</span></span>
* <span data-ttu-id="bad25-141">할당된 지역에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-141">Located in your assigned region.</span></span> <span data-ttu-id="bad25-142">시작할 때 사용자가 할당된 지역이 리소스 그룹 이름 `cloud-shell-storage-<region>`에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-142">When you are onboarding, the region you are assigned to is listed in the resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="bad25-143">지원되는 저장소 지역</span><span class="sxs-lookup"><span data-stu-id="bad25-143">Supported storage regions</span></span>
<span data-ttu-id="bad25-144">Azure 파일은 사용자가 마운트되는 대상 Cloud Shell 컴퓨터와 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-144">The Azure files must reside in the same region as the Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="bad25-145">Cloud Shell 클러스터는 현재 다음 지역에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-145">Cloud Shell clusters currently exist in the following regions:</span></span>
|<span data-ttu-id="bad25-146">영역</span><span class="sxs-lookup"><span data-stu-id="bad25-146">Area</span></span>|<span data-ttu-id="bad25-147">지역</span><span class="sxs-lookup"><span data-stu-id="bad25-147">Region</span></span>|
|---|---|
|<span data-ttu-id="bad25-148">아메리카</span><span class="sxs-lookup"><span data-stu-id="bad25-148">Americas</span></span>|<span data-ttu-id="bad25-149">미국 동부, 미국 중남부, 미국 서부</span><span class="sxs-lookup"><span data-stu-id="bad25-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="bad25-150">유럽</span><span class="sxs-lookup"><span data-stu-id="bad25-150">Europe</span></span>|<span data-ttu-id="bad25-151">북유럽, 서유럽</span><span class="sxs-lookup"><span data-stu-id="bad25-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="bad25-152">아시아 태평양</span><span class="sxs-lookup"><span data-stu-id="bad25-152">Asia Pacific</span></span>|<span data-ttu-id="bad25-153">인도 중부, 동남 아시아</span><span class="sxs-lookup"><span data-stu-id="bad25-153">India Central, Southeast Asia</span></span>|

### <a name="the-clouddrive-mount-command"></a><span data-ttu-id="bad25-154">`clouddrive mount` 명령</span><span class="sxs-lookup"><span data-stu-id="bad25-154">The `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="bad25-155">새 파일 공유를 마운트하는 경우 이전 `$Home` 이미지가 이전 파일 공유에 보관되는 것처럼 `$Home` 디렉터리에 대해 새 사용자 이미지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in the previous file share.</span></span>

<span data-ttu-id="bad25-156">다음 매개 변수를 사용하여 `clouddrive mount` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-156">Run the `clouddrive mount` command with the following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="bad25-157">자세한 세부 정보를 보려면 아래와 같이 `clouddrive mount -h`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-157">To view more details, run `clouddrive mount -h`, as shown here:</span></span>

![‘clouddrive mount’ 명령 실행](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="bad25-159">`clouddrive` 마운트 해제</span><span class="sxs-lookup"><span data-stu-id="bad25-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="bad25-160">언제든지 Cloud Shell에 마운트된 파일 공유의 마운트를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-160">You can unmount a file share that's mounted to Cloud Shell at any time.</span></span> <span data-ttu-id="bad25-161">파일 공유가 분리되면 다음 세션을 진행하기 전에 새 파일 공유를 탑재하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-161">Once your file share is unmounted, you will be prompted to mount a new file share prior to your next session.</span></span>

<span data-ttu-id="bad25-162">Cloud Shell에서 파일 공유를 제거하려면</span><span class="sxs-lookup"><span data-stu-id="bad25-162">To remove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="bad25-163">`clouddrive unmount`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="bad25-164">프롬프트를 승인 및 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-164">Acknowledge and confirm the prompts.</span></span>

<span data-ttu-id="bad25-165">파일 공유는 수동으로 삭제하지 않은 한 계속 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-165">Your file share will continue to exist unless you delete it manually.</span></span> <span data-ttu-id="bad25-166">Cloud Shell은 후속 세션에서 이 파일 공유를 더 이상 검색하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="bad25-167">자세한 세부 정보를 보려면 아래와 같이 `clouddrive unmount -h`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-167">To view more details, run `clouddrive unmount -h`, as shown here:</span></span>

![‘clouddrive unmount’ 명령 실행](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="bad25-169">이 명령을 실행하면 리소스가 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="bad25-170">Cloud Shell에 매핑된 리소스 그룹, 저장소 계정 또는 파일 공유를 수동으로 삭제하면 `$Home` 디렉터리 디스크 이미지 및 파일 공유의 다른 모든 파일이 영구적으로 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-170">Manually deleting a resource group, storage account, or file share that is mapped to Cloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="bad25-171">이 작업은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="bad25-172">`clouddrive` 파일 공유 나열</span><span class="sxs-lookup"><span data-stu-id="bad25-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="bad25-173">`clouddrive`로 마운트된 파일 공유를 확인하려면 다음 `df` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-173">To discover which file share is mounted as `clouddrive`, run the following `df` command.</span></span> 

<span data-ttu-id="bad25-174">clouddrive에 대한 파일 경로는 URL에서 저장소 계정 이름 및 파일 공유를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-174">The file path to clouddrive shows your storage account name and file share in the URL.</span></span> <span data-ttu-id="bad25-175">예를 들어 `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="bad25-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

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

## <a name="transfer-local-files-to-cloud-shell"></a><span data-ttu-id="bad25-176">Cloud Shell에 로컬 파일 전송</span><span class="sxs-lookup"><span data-stu-id="bad25-176">Transfer local files to Cloud Shell</span></span>
<span data-ttu-id="bad25-177">`clouddrive` 디렉터리가 Azure Portal 저장소 블레이드에 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-177">The `clouddrive` directory syncs with the Azure portal storage blade.</span></span> <span data-ttu-id="bad25-178">이 블레이드를 사용하여 파일 공유 간에 로컬 파일을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-178">Use this blade to transfer local files to or from your file share.</span></span> <span data-ttu-id="bad25-179">Cloud Shell 내의 파일을 업데이트하면 블레이드를 새로 고칠 때 파일 저장소 GUI에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-179">Updating files from within Cloud Shell is reflected in the file storage GUI when you refresh the blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="bad25-180">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="bad25-180">Download files</span></span>

![로컬 파일 목록](media/download.png)
1. <span data-ttu-id="bad25-182">Azure Portal에서 마운트된 파일 공유로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-182">In the Azure portal, go to the mounted file share.</span></span>
2. <span data-ttu-id="bad25-183">대상 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-183">Select the target file.</span></span>
3. <span data-ttu-id="bad25-184">**다운로드** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-184">Select the **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="bad25-185">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="bad25-185">Upload files</span></span>

![업로드할 로컬 파일](media/upload.png)
1. <span data-ttu-id="bad25-187">마운트된 파일 공유로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-187">Go to your mounted file share.</span></span>
2. <span data-ttu-id="bad25-188">**업데이트** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-188">Select the **Upload** button.</span></span>
3. <span data-ttu-id="bad25-189">업로드할 파일을 하나 이상 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-189">Select the file or files that you want to upload.</span></span>
4. <span data-ttu-id="bad25-190">업로드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-190">Confirm the upload.</span></span>

<span data-ttu-id="bad25-191">이제 Cloud Shell의 `clouddrive` 디렉터리에서 액세스할 수 있는 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad25-191">You should now see the files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bad25-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bad25-192">Next steps</span></span>
[<span data-ttu-id="bad25-193">Cloud Shell 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="bad25-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="bad25-194">
[Azure File Storage에 대해 알아보기](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="bad25-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="bad25-195">
[저장소 태그에 대해 알아보기](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="bad25-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
