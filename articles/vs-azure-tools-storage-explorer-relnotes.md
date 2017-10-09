---
title: "aaaMicrosoft Azure 저장소 탐색기 (미리 보기) 릴리스 정보 | Microsoft Docs"
description: "Microsoft Azure Storage 탐색기(미리 보기) 릴리스 정보"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="18d85-103">Microsoft Azure Storage 탐색기(미리 보기) 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="18d85-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="18d85-104">이전 버전에 대 한 릴리스 정보 뿐만 아니라 Azure 저장소 탐색기 0.8.16에 대 한 정보 (Preview) 릴리스 hello 릴리스가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-104">This article contains hello release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="18d85-105">[Microsoft Azure 저장소 탐색기 (미리 보기)](./vs-azure-tools-storage-manage-with-storage-explorer.md) 는 Windows, macOS 등 및 Linux에서 데이터를 Azure 저장소 사용 tooeasily 작업 수 있도록 하는 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="18d85-106">버전 0.8.16(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="18d85-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="18d85-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="18d85-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="18d85-108">Azure Storage 탐색기 0.8.16(미리 보기) 다운로드</span><span class="sxs-lookup"><span data-stu-id="18d85-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="18d85-109">Windows용 Azure Storage 탐색기 0.8.16(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="18d85-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="18d85-110">Mac용 Azure Storage 탐색기 0.8.16(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="18d85-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="18d85-111">Linux용 Azure Storage 탐색기 0.8.16(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="18d85-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="18d85-112">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-112">New</span></span>
* <span data-ttu-id="18d85-113">Blob을 열 때 저장소 탐색기 묻는 메시지가 나타납니다 tooupload hello 다운로드 한 파일 변경이 감지 된 경우</span><span class="sxs-lookup"><span data-stu-id="18d85-113">When you open a blob, Storage Explorer will prompt you tooupload hello downloaded file if a change is detected</span></span>
* <span data-ttu-id="18d85-114">향상된 Azure Stack 로그인 환경</span><span class="sxs-lookup"><span data-stu-id="18d85-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="18d85-115">Hello에 너무 작은 업로드/다운로드의 향상 된 hello 성능을 파일 같은 시간</span><span class="sxs-lookup"><span data-stu-id="18d85-115">Improved hello performance of uploading/downloading many small files at hello same time</span></span>


### <a name="fixes"></a><span data-ttu-id="18d85-116">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-116">Fixes</span></span>
* <span data-ttu-id="18d85-117">일부 blob 유형에 대 한 선택 너무 "자동 대체" 업로드 충돌 하는 동안 하면 경우에 따라 발생 hello 업로드를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-117">For some blob types, choosing too"replace" during an upload conflict would sometimes result in hello upload being restarted.</span></span> 
* <span data-ttu-id="18d85-118">버전 0.8.15에서 업로드는 경우에 따라 99%에서 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="18d85-119">아직 존재 하지 않는 tooupload tooa 디렉터리를 선택 하는 경우 파일 tooa 파일 공유를 업로드, 하는 경우 업로드가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-119">When uploading files tooa file share, if you chose tooupload tooa directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="18d85-120">저장소 탐색기가 공유 액세스 서명 및 테이블 쿼리에 대한 타임스탬프를 잘못 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="18d85-121">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-121">Known Issues</span></span>
* <span data-ttu-id="18d85-122">현재 이름 및 키 연결 문자열을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="18d85-123">Hello 다음 릴리스에서 수정 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-123">It will be fixed in hello next release.</span></span> <span data-ttu-id="18d85-124">그때까지는 이름 및 키로 연결 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="18d85-125">Tooopen 잘못 된 Windows 파일 이름으로 파일을 시도 하면 hello 다운로드 한 파일 없음 오류 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-125">If you try tooopen a file with an invalid Windows file name, hello download will result in a file not found error.</span></span>
* <span data-ttu-id="18d85-126">작업에 "취소"를 클릭 한 후 해당 작업 toocancel 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-126">After clicking "Cancel" on a task, it may take a while for that task toocancel.</span></span> <span data-ttu-id="18d85-127">Hello Azure 저장소 노드 라이브러리의 제한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-127">This is a limitation of hello Azure Storage Node library.</span></span>
* <span data-ttu-id="18d85-128">Blob 업로드를 완료 한 후 hello 업로드 중에서 어느 hello 탭 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-128">After completing a blob upload, hello tab which initiated hello upload is refreshed.</span></span> <span data-ttu-id="18d85-129">이전 동작에서 변경 된 내용 이므로 toobe toohello 루트에 있는 hello 컨테이너의 다시 이동 해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-129">This is a change from previous behavior, and will also cause you toobe taken back toohello root of hello container you are in.</span></span>
* <span data-ttu-id="18d85-130">잘못 된 PIN/스마트 카드 인증서 hello 다음 toorestart 순서 toohave 저장소 탐색기에에서 필요 합니다를 선택 하는 경우 기억해 해당 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-130">If you choose hello wrong PIN/Smartcard certificate, then you will need toorestart in order toohave Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="18d85-131">hello 계정 설정 패널 tooreenter 자격 증명 toofilter 구독 해야 하는 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-131">hello account settings panel may show that you need tooreenter credentials toofilter subscriptions.</span></span>
* <span data-ttu-id="18d85-132">blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="18d85-133">Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="18d85-134">Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="18d85-135">Ubuntu 14.04에 사용자를 위해 GCC toodate 중일 tooensure 해야-hello를 실행 하 여이 작업을 수행할 수 있습니다 명령 하 고 다음 컴퓨터를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-135">For users on Ubuntu 14.04, you will need tooensure GCC is up toodate - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="18d85-136">Ubuntu 17.04에 사용자를 위해 tooinstall GConf 해야-이렇게 하 여 hello 명령, 다음 컴퓨터를 다시 시작 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-136">For users on Ubuntu 17.04, you will need tooinstall GConf - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="18d85-137">버전 0.8.14(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="18d85-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="18d85-138">06/22/2017</span><span class="sxs-lookup"><span data-stu-id="18d85-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="18d85-139">Azure Storage 탐색기 0.8.14(미리 보기) 다운로드</span><span class="sxs-lookup"><span data-stu-id="18d85-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="18d85-140">Windows용 Azure Storage 탐색기 0.8.14(미리 보기) 다운로드</span><span class="sxs-lookup"><span data-stu-id="18d85-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="18d85-141">Mac용 Azure Storage 탐색기 0.8.14(미리 보기) 다운로드</span><span class="sxs-lookup"><span data-stu-id="18d85-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="18d85-142">Linux용 Azure Storage 탐색기 0.8.14(미리 보기) 다운로드</span><span class="sxs-lookup"><span data-stu-id="18d85-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="18d85-143">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-143">New</span></span>

* <span data-ttu-id="18d85-144">순서 tootake 활용 한 몇 가지 중요 한 보안 업데이트에서에서 업데이트 된 전자 버전 too1.7.2</span><span class="sxs-lookup"><span data-stu-id="18d85-144">Updated Electron version too1.7.2 in order tootake advantage of several critical security updates</span></span>
* <span data-ttu-id="18d85-145">이제 빠르게 액세스할 수 있습니다 hello 온라인 문제 해결 가이드 hello 도움말 메뉴에서</span><span class="sxs-lookup"><span data-stu-id="18d85-145">You can now quickly access hello online troubleshooting guide from hello help menu</span></span>
* <span data-ttu-id="18d85-146">Storage 탐색기 문제 해결 [가이드][2]</span><span class="sxs-lookup"><span data-stu-id="18d85-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="18d85-147">[지침] [ 3] tooan 스택 Azure 구독 연결</span><span class="sxs-lookup"><span data-stu-id="18d85-147">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="18d85-148">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-148">Known Issues</span></span>

* <span data-ttu-id="18d85-149">Hello 삭제 폴더 확인 대화 상자에서 단추 linux hello 마우스 클릭 하 여 등록 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-149">Buttons on hello delete folder confirmation dialog don't register with hello mouse clicks on Linux.</span></span> <span data-ttu-id="18d85-150">Toouse hello Enter 키를이 문제를 해결</span><span class="sxs-lookup"><span data-stu-id="18d85-150">Workaround is toouse hello Enter key</span></span>
* <span data-ttu-id="18d85-151">잘못 된 PIN/스마트 카드 인증서 hello 다음 toorestart 순서 toohave 저장소 탐색기에에서 필요 합니다를 선택 하면 잊은 hello 의사 결정</span><span class="sxs-lookup"><span data-stu-id="18d85-151">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="18d85-152">Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-152">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="18d85-153">hello 계정 설정 패널 순서 toofilter 구독에 자격 증명 tooreenter 해야 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-153">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="18d85-154">blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="18d85-155">Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="18d85-156">Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="18d85-157">Ubuntu 14.04 설치 요구 gcc 버전 업데이트 또는 업그레이드 – 단계 tooupgrade 아래에</span><span class="sxs-lookup"><span data-stu-id="18d85-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="18d85-158">이전 릴리스</span><span class="sxs-lookup"><span data-stu-id="18d85-158">Previous releases</span></span>

* [<span data-ttu-id="18d85-159">버전 0.8.13</span><span class="sxs-lookup"><span data-stu-id="18d85-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="18d85-160">버전 0.8.12/0.8.11/0.8.10</span><span class="sxs-lookup"><span data-stu-id="18d85-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="18d85-161">버전 0.8.9/0.8.8</span><span class="sxs-lookup"><span data-stu-id="18d85-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="18d85-162">버전 0.8.7</span><span class="sxs-lookup"><span data-stu-id="18d85-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="18d85-163">버전 0.8.6</span><span class="sxs-lookup"><span data-stu-id="18d85-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="18d85-164">버전 0.8.5</span><span class="sxs-lookup"><span data-stu-id="18d85-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="18d85-165">버전 0.8.4</span><span class="sxs-lookup"><span data-stu-id="18d85-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="18d85-166">버전 0.8.3</span><span class="sxs-lookup"><span data-stu-id="18d85-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="18d85-167">버전 0.8.2</span><span class="sxs-lookup"><span data-stu-id="18d85-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="18d85-168">버전 0.8.0</span><span class="sxs-lookup"><span data-stu-id="18d85-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="18d85-169">버전 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="18d85-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="18d85-170">버전 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="18d85-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="18d85-171">버전 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="18d85-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="18d85-172">버전 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="18d85-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="18d85-173">버전 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="18d85-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="18d85-174">버전 0.8.13</span><span class="sxs-lookup"><span data-stu-id="18d85-174">Version 0.8.13</span></span>
<span data-ttu-id="18d85-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="18d85-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="18d85-176">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-176">New</span></span>

* <span data-ttu-id="18d85-177">Storage 탐색기 문제 해결 [가이드][2]</span><span class="sxs-lookup"><span data-stu-id="18d85-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="18d85-178">[지침] [ 3] tooan 스택 Azure 구독 연결</span><span class="sxs-lookup"><span data-stu-id="18d85-178">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-179">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-179">Fixes</span></span>

* <span data-ttu-id="18d85-180">수정됨: 파일 업로드 시의 높은 메모리 부족 오류 발생 가능성이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="18d85-181">수정됨: 이제 PIN/스마트 카드를 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="18d85-182">수정됨: 이제 포털에서 열기가 Azure 중국, Azure 독일, Azure 미국 정부 및 Azure Stack에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="18d85-183">고정: 폴더 tooa blob 컨테이너를 업로드 하는 동안 "작업이 잘못 되었습니다." 오류가 경우가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-183">Fixed: While uploading a folder tooa blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="18d85-184">수정됨: 스냅숏을 관리하는 동안 모두 선택 기능이 사용할 수 없도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="18d85-185">고정: hello 기본 blob의 hello 메타 데이터 가져오기 덮어써질 스냅숏과 hello 속성을 검토 한 후</span><span class="sxs-lookup"><span data-stu-id="18d85-185">Fixed: hello metadata of hello base blob might get overwritten after viewing hello properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="18d85-186">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-186">Known Issues</span></span>

* <span data-ttu-id="18d85-187">잘못 된 PIN/스마트 카드 인증서 hello 다음 toorestart 순서 toohave 저장소 탐색기에에서 필요 합니다를 선택 하면 잊은 hello 의사 결정</span><span class="sxs-lookup"><span data-stu-id="18d85-187">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="18d85-188">확대 또는 축소, 동안 hello 확대/축소 수준을 일시적으로 다시 설정 toohello 기본 수준</span><span class="sxs-lookup"><span data-stu-id="18d85-188">While zoomed in or out, hello zoom level may momentarily reset toohello default level</span></span>
* <span data-ttu-id="18d85-189">Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-189">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="18d85-190">hello 계정 설정 패널 순서 toofilter 구독에 자격 증명 tooreenter 해야 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-190">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="18d85-191">blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="18d85-192">Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="18d85-193">Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="18d85-194">Ubuntu 14.04 설치 요구 gcc 버전 업데이트 또는 업그레이드 – 단계 tooupgrade 아래에</span><span class="sxs-lookup"><span data-stu-id="18d85-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="18d85-195">버전 0.8.12/0.8.11/0.8.10</span><span class="sxs-lookup"><span data-stu-id="18d85-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="18d85-196">04/07/2017</span><span class="sxs-lookup"><span data-stu-id="18d85-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="18d85-197">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-197">New</span></span>

* <span data-ttu-id="18d85-198">저장소 탐색기 자동으로 닫힙니다 hello 업데이트 알림에서 업데이트를 설치 하는 경우</span><span class="sxs-lookup"><span data-stu-id="18d85-198">Storage Explorer will now automatically close when you install an update from hello update notification</span></span>
* <span data-ttu-id="18d85-199">현재 위치 빠른 액세스 기능이 자주 액세스하는 리소스 사용을 위한 향상된 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="18d85-200">Hello Blob 컨테이너 편집기에 표시 임대 된 blob에 속해 있는 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="18d85-200">In hello Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="18d85-201">이제 hello 왼쪽 패널 축소</span><span class="sxs-lookup"><span data-stu-id="18d85-201">You can now collapse hello left side panel</span></span>
* <span data-ttu-id="18d85-202">검색 지금 실행 hello에서 동일한 시간 다운로드로</span><span class="sxs-lookup"><span data-stu-id="18d85-202">Discovery now runs at hello same time as download</span></span>
* <span data-ttu-id="18d85-203">리소스 또는 선택의 Blob 컨테이너, 파일 공유 및 테이블 편집기 toosee hello 크기 hello에 통계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-203">Use Statistics in hello Blob Container, File Share, and Table editors toosee hello size of your resource or selection</span></span>
* <span data-ttu-id="18d85-204">이제 로그인 tooAzure Active Directory (AAD) Azure 스택 계정을 기반으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-204">You can now sign-in tooAzure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="18d85-205">이제 업로드 보관 32 개 MB tooPremium 저장소 계정 파일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-205">You can now upload archive files over 32MB tooPremium storage accounts</span></span>
* <span data-ttu-id="18d85-206">손쉬운 사용 옵션 지원이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-206">Improved accessibility support</span></span>
* <span data-ttu-id="18d85-207">신뢰할 수 있는 base64 이제 추가할 수 있습니다 이동 tooEdit-X.509 SSL 인증서로 인코딩하지&gt; SSL 인증서-&gt; 인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="18d85-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going tooEdit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-208">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-208">Fixes</span></span>

* <span data-ttu-id="18d85-209">고정: 계정의 자격 증명을 새로 고친 후 hello 트리 보기는 경우에 따라 자동으로 새로 고쳐지지 않습니다</span><span class="sxs-lookup"><span data-stu-id="18d85-209">Fixed: after refreshing an account's credentials, hello tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="18d85-210">수정됨: 에뮬레이터 큐 및 테이블에 대해 SAS를 생성하면 잘못된 URL이 생성되는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="18d85-211">수정됨: 이제 프록시가 사용하도록 설정된 상태에서 Premium Storage 계정을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="18d85-212">고정: hello 적용 단추 hello 계정 관리 페이지에는 1 또는 0 계정을 선택한 경우 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-212">Fixed: hello apply button on hello accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="18d85-213">수정됨: 충돌을 해결해야 하는 Blob 업로드가 실패할 수 있는 현상이 버전 0.8.11에서 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="18d85-214">수정됨: 버전 0.8.11에서 피드백 전송이 중단되는 현상이 버전 0.8.12에서 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="18d85-215">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-215">Known Issues</span></span>

* <span data-ttu-id="18d85-216">Too0.8.10를 업그레이드 한 후 해야 toorefresh 모든 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-216">After upgrading too0.8.10, you will need toorefresh all of your credentials.</span></span>
* <span data-ttu-id="18d85-217">확대 또는 축소, 동안 hello 확대/축소 수준을 toohello 기본 수준 다시 설정 일시적으로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-217">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="18d85-218">Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-218">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>
* <span data-ttu-id="18d85-219">hello 계정 설정 패널 순서 toofilter 구독에 자격 증명 tooreenter 해야 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-219">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions.</span></span>
* <span data-ttu-id="18d85-220">blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="18d85-221">Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="18d85-222">Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="18d85-223">Ubuntu 14.04 설치 요구 gcc 버전 업데이트 또는 업그레이드 – 단계 tooupgrade 아래에</span><span class="sxs-lookup"><span data-stu-id="18d85-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="18d85-224">버전 0.8.9/0.8.8</span><span class="sxs-lookup"><span data-stu-id="18d85-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="18d85-225">02/23/2017</span><span class="sxs-lookup"><span data-stu-id="18d85-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="18d85-226">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-226">New</span></span>

* <span data-ttu-id="18d85-227">저장소 탐색기 0.8.9 hello 업데이트에 대 한 최신 버전을 자동으로 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-227">Storage Explorer 0.8.9 will automatically download hello latest version for updates.</span></span>
* <span data-ttu-id="18d85-228">핫픽스: 포털을 사용 하 여 SAS URI tooattach 저장소 계정을 결과 오류가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-228">Hotfix: using a portal generated SAS URI tooattach a storage account would result in an error.</span></span>
* <span data-ttu-id="18d85-229">이제 Blob 스냅숏을 만들고 관리하고 수준을 올릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="18d85-230">이제 tooAzure 중국, Azure 독일 및 Azure 미국 정부 계정을에 서명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-230">You can now sign in tooAzure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="18d85-231">이제 hello 확대/축소 수준을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-231">You can now change hello zoom level.</span></span> <span data-ttu-id="18d85-232">축소 및 확대/축소 다시 설정에서 보기 메뉴 tooZoom hello에에서 hello 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-232">Use hello options in hello View menu tooZoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="18d85-233">이제 Blob 및 파일의 사용자 메타데이터에서 유니코드 문자가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="18d85-234">내게 필요한 옵션이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-234">Accessibility improvements.</span></span>
* <span data-ttu-id="18d85-235">hello 업데이트 알림에서 hello 다음 버전의 릴리스 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-235">hello next version's release notes can be viewed from hello update notification.</span></span> <span data-ttu-id="18d85-236">Hello hello 도움말 메뉴에서 현재 릴리스 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-236">You can also view hello current release notes from hello Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-237">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-237">Fixes</span></span>

* <span data-ttu-id="18d85-238">고정: hello 버전 번호는 이제 올바르게 표시 Windows에서 제어판의</span><span class="sxs-lookup"><span data-stu-id="18d85-238">Fixed: hello version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="18d85-239">고정: 검색은 더 이상 제한 too50, 000 노드</span><span class="sxs-lookup"><span data-stu-id="18d85-239">Fixed: search is no longer limited too50,000 nodes</span></span>
* <span data-ttu-id="18d85-240">고정: 업로드 tooa 파일 공유 된 영원히 hello 대상 디렉터리가 아직 없는 경우</span><span class="sxs-lookup"><span data-stu-id="18d85-240">Fixed: upload tooa file share spun forever if hello destination directory did not already exist</span></span>
* <span data-ttu-id="18d85-241">수정됨: 오랫동안 실행되는 업로드와 다운로드의 안정성이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="18d85-242">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-242">Known Issues</span></span>

* <span data-ttu-id="18d85-243">확대 또는 축소, 동안 hello 확대/축소 수준을 toohello 기본 수준 다시 설정 일시적으로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-243">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="18d85-244">빠른 액세스는 구독 기반 항목에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="18d85-245">로컬 리소스 또는 키나 SAS 토큰을 통해 연결된 리소스는 이번 릴리스에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="18d85-246">빠르게 액세스할 수는 몇 초 toonavigate toohello 대상 리소스에 있는 리소스의 수에 따라 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-246">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="18d85-247">Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-247">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>

<span data-ttu-id="18d85-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="18d85-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="18d85-249">버전 0.8.7</span><span class="sxs-lookup"><span data-stu-id="18d85-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="18d85-250">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-250">New</span></span>

* <span data-ttu-id="18d85-251">업데이트를 시작 하는 hello에서 tooresolve 충돌 다운로드 하거나 세션 hello 활동 창에서 복사 방법을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-251">You can choose how tooresolve conflicts at hello beginning of an update, download or copy session in hello Activities window</span></span>
* <span data-ttu-id="18d85-252">Hello 저장소 리소스의 탭 toosee hello 전체 경로 위로 마우스를 가져가고합니다</span><span class="sxs-lookup"><span data-stu-id="18d85-252">Hover over a tab toosee hello full path of hello storage resource</span></span>
* <span data-ttu-id="18d85-253">Hello 왼쪽 탐색 창에서 해당 위치와 동기화 하는 탭을 클릭할 때</span><span class="sxs-lookup"><span data-stu-id="18d85-253">When you click on a tab, it synchronizes with its location in hello left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-254">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-254">Fixes</span></span>

* <span data-ttu-id="18d85-255">수정됨: 이제 Mac에서도 Storage 탐색기를 신뢰할 수 있는 앱으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="18d85-256">수정됨: Ubuntu 14.04가 다시 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="18d85-257">고정: 때로는 hello 계정을 추가 구독을 로드할 때 UI 깜박이</span><span class="sxs-lookup"><span data-stu-id="18d85-257">Fixed: Sometimes hello add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="18d85-258">고정: 경우에 따라 모든 저장소 리소스 hello 왼쪽 탐색 창에 나열 된</span><span class="sxs-lookup"><span data-stu-id="18d85-258">Fixed: Sometimes not all storage resources were listed in hello left side navigation pane</span></span>
* <span data-ttu-id="18d85-259">고정: hello 작업 창 경우가 표시 빈 동작</span><span class="sxs-lookup"><span data-stu-id="18d85-259">Fixed: hello action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="18d85-260">고정: hello 창 크기 hello 마지막 닫힌 세션에서 이제 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-260">Fixed: hello window size from hello last closed session is now retained</span></span>
* <span data-ttu-id="18d85-261">고정: hello에 대 한 여러 탭을 열 수 hello 상황에 맞는 메뉴를 사용 하 여 동일한 리소스</span><span class="sxs-lookup"><span data-stu-id="18d85-261">Fixed: You can open multiple tabs for hello same resource using hello context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="18d85-262">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-262">Known Issues</span></span>

* <span data-ttu-id="18d85-263">빠른 액세스는 구독 기반 항목에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="18d85-264">로컬 리소스 또는 키나 SAS 토큰을 통해 연결된 리소스는 이번 릴리스에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="18d85-265">빠르게 액세스할 수는 몇 초 toonavigate toohello 대상 리소스에 있는 리소스의 수에 따라 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-265">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="18d85-266">Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-266">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="18d85-267">검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하되거나 처리되지 않은 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="18d85-268">MacOS 등에서 hello 저장소 탐색기를 사용 하 여 처음으로 hello에 대 한 사용자의 권한 tooaccess 키 집합을 요청 하는 여러 개의 프롬프트가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-268">For hello first time using hello Storage Explorer on macOS, you might see multiple prompts asking for user's permission tooaccess keychain.</span></span> <span data-ttu-id="18d85-269">항상 허용 되도록 선택 hello 프롬프트 다시 나타나지 않습니다 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-269">We suggest you select Always Allow so hello prompt won't show up again</span></span>

<span data-ttu-id="18d85-270">11/18/2016</span><span class="sxs-lookup"><span data-stu-id="18d85-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="18d85-271">버전 0.8.6</span><span class="sxs-lookup"><span data-stu-id="18d85-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="18d85-272">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-272">New</span></span>

* <span data-ttu-id="18d85-273">이제 쉽게 탐색을 위한 pin 가장 자주 사용 되는 서비스 toohello 빠르게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-273">You can now pin most frequently used services toohello Quick Access for easy navigation</span></span>
* <span data-ttu-id="18d85-274">이제 다른 탭에 있는 여러 편집기를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="18d85-275">단일 tooopen 임시 탭;를 클릭 합니다. tooopen 영구 탭을 두 번 클릭 합니다. 클릭할 수도 있습니다 hello 임시 탭 toomake에 해당 영구 탭</span><span class="sxs-lookup"><span data-stu-id="18d85-275">Single click tooopen a temporary tab; double click tooopen a permanent tab. You can also click on hello temporary tab toomake it a permanent tab</span></span>
* <span data-ttu-id="18d85-276">특히 빠른 컴퓨터에서 큰 파일에 대해 업로드 및 다운로드를 수행할 때 성능 및 안정성이 크게 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="18d85-277">이제 blob 컨테이너에 빈 "가상" 폴더를 만들 수 있음</span><span class="sxs-lookup"><span data-stu-id="18d85-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="18d85-278">새롭게 향상된 하위 문자열 검색에 범위 지정 검색 기능이 다시 도입되었으므로 이제 검색 시에 다음의 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="18d85-279">전역 검색-hello 검색 텍스트 상자에 검색 용어 입력</span><span class="sxs-lookup"><span data-stu-id="18d85-279">Global search - just enter a search term into hello search textbox</span></span>
    * <span data-ttu-id="18d85-280">범위 지정된 검색-hello 돋보기 아이콘 다음 tooa 노드를 클릭 한 다음 hello 경로 검색 용어 toohello 끝에 추가 또는 마우스 오른쪽 단추로 클릭 한 검색에서 "여기" 선택</span><span class="sxs-lookup"><span data-stu-id="18d85-280">Scoped search - click hello magnifying glass icon next tooa node, then add a search term toohello end of hello path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="18d85-281">밝게(기본값), 어둡게, 고대비 검정 및 고대비 흰색 등의 다양한 테마를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="18d85-282">TooEdit-이동&gt; 테마 toochange 테마 설정 기본 설정</span><span class="sxs-lookup"><span data-stu-id="18d85-282">Go tooEdit -&gt; Themes toochange your theming preference</span></span>
* <span data-ttu-id="18d85-283">Blob 및 파일 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="18d85-284">이제 인코딩된 큐 메시지(Base64)와 인코딩되지 않은 큐 메시지가 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="18d85-285">이제 Linux에서는 64비트 OS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="18d85-286">이번 릴리스에서는 64비트 Ubuntu 16.04.1 LTS만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="18d85-287">로고가 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-288">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-288">Fixes</span></span>

* <span data-ttu-id="18d85-289">수정됨: 화면 중단 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="18d85-290">수정됨: 향상된 보안</span><span class="sxs-lookup"><span data-stu-id="18d85-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="18d85-291">수정됨: 가끔씩 연결된 계정이 중복으로 표시되는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="18d85-292">수정됨: Blob의 콘텐츠 형식이 정의되어 있지 않으면 예외가 발생할 수 있는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="18d85-293">고정: 빈 테이블에 대 한 쿼리 패널 열기 hello 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-293">Fixed: Opening hello Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="18d85-294">수정됨: 검색의 버그가 확인 및 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="18d85-295">고정: "부하 추가 정보"를 클릭 하면 50 too100에서 로드 하는 리소스의 hello 수 증가</span><span class="sxs-lookup"><span data-stu-id="18d85-295">Fixed: Increased hello number of resources loaded from 50 too100 when clicking "Load More"</span></span>
* <span data-ttu-id="18d85-296">수정됨: 이제는 첫 실행 시 계정에 로그인하면 기본적으로 해당 계정의 모든 구독이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="18d85-297">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-297">Known Issues</span></span>

* <span data-ttu-id="18d85-298">Ubuntu 14.04에서이 버전의 hello 저장소 탐색기를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-298">This release of hello Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="18d85-299">tooopen 동일한 리소스에 계속 하지 마십시오 클릭 hello에 대 한 여러 탭 hello 동일한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-299">tooopen multiple tabs for hello same resource, do not continuously click on hello same resource.</span></span> <span data-ttu-id="18d85-300">다른 리소스 클릭 하 고 이전 단계로 이동 하 고 원래 리소스 tooopen hello 다시 클릭 다른 탭에서</span><span class="sxs-lookup"><span data-stu-id="18d85-300">Click on another resource and then go back and then click on hello original resource tooopen it again in another tab</span></span> 
* <span data-ttu-id="18d85-301">빠른 액세스는 구독 기반 항목에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="18d85-302">로컬 리소스 또는 키나 SAS 토큰을 통해 연결된 리소스는 이번 릴리스에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="18d85-303">빠르게 액세스할 수는 몇 초 toonavigate toohello 대상 리소스에 있는 리소스의 수에 따라 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-303">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="18d85-304">Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-304">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="18d85-305">검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하되거나 처리되지 않은 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="18d85-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="18d85-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="18d85-307">버전 0.8.5</span><span class="sxs-lookup"><span data-stu-id="18d85-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="18d85-308">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-308">New</span></span>

* <span data-ttu-id="18d85-309">사용 하 여 포털에서 생성 된 SAS 키 tooattach tooStorage 이제 계정 및 리소스</span><span class="sxs-lookup"><span data-stu-id="18d85-309">Can now use Portal-generated SAS keys tooattach tooStorage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-310">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-310">Fixes</span></span>

* <span data-ttu-id="18d85-311">경우에 따라 검색 하는 동안 경합 상태는 확장할 수 없는 노드 toobecome를 발생 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-311">Fixed: race condition during search sometimes caused nodes toobecome non-expandable</span></span>
* <span data-ttu-id="18d85-312">고정: "HTTP 사용" 경우 작동 하지 않음 tooStorage 계정의 계정 이름과 키를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="18d85-312">Fixed: "Use HTTP" doesn't work when connecting tooStorage Accounts with account name and key</span></span>
* <span data-ttu-id="18d85-313">수정됨: SAS 키(구체적으로는 Portal에서 생성된 키)에서 "후행 슬래시" 오류가 반환되는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="18d85-314">수정됨: 테이블 가져오기 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="18d85-315">가끔씩 파티션 키와 행 키가 서로 바뀌는 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="18d85-316">파티션 키를 "null" 없습니다 tooread</span><span class="sxs-lookup"><span data-stu-id="18d85-316">Unable tooread "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="18d85-317">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-317">Known Issues</span></span>

* <span data-ttu-id="18d85-318">검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="18d85-319">시도 tooexpand 파일에서는 오류를 표시 하므로 azure 스택 파일을 현재 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-319">Azure Stack doesn't currently support Files, so trying tooexpand Files will show an error</span></span>

<span data-ttu-id="18d85-320">09/12/2016</span><span class="sxs-lookup"><span data-stu-id="18d85-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="18d85-321">버전 0.8.4</span><span class="sxs-lookup"><span data-stu-id="18d85-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="18d85-322">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-322">New</span></span>

* <span data-ttu-id="18d85-323">직접 링크 toostorage 계정, 컨테이너, 큐, 테이블, 생성 또는 공유 하기 위한 쉽고 파일 공유 액세스 tooyour 리소스-Windows 및 Mac OS 지원</span><span class="sxs-lookup"><span data-stu-id="18d85-323">Generate direct links toostorage accounts, containers, queues, tables, or file shares for sharing and easy access tooyour resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="18d85-324">Blob 컨테이너, 테이블, 큐, 파일 공유 또는 hello 검색 상자에서 저장소 계정에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="18d85-324">Search for your blob containers, tables, queues, file shares, or storage accounts from hello search box</span></span>
* <span data-ttu-id="18d85-325">이제 절 hello 테이블 쿼리 작성기에서를 그룹 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-325">You can now group clauses in hello table query builder</span></span>
* <span data-ttu-id="18d85-326">SAS에 연결된 계정 및 컨테이너 내에서 Blob 컨테이너, 파일 공유, 테이블, Blob, Blob 폴더, 파일 및 디렉터리 복사/붙여넣기 및 이름 바꾸기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="18d85-327">이제 Blob 컨테이너와 파일 공유의 이름 바꾸기 및 복사 시에 속성과 메타데이터가 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-328">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-328">Fixes</span></span>

* <span data-ttu-id="18d85-329">수정됨: 부울 또는 이진 속성을 포함하는 테이블 엔터티를 편집할 수 없는 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="18d85-330">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-330">Known Issues</span></span>

* <span data-ttu-id="18d85-331">검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="18d85-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="18d85-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="18d85-333">버전 0.8.3</span><span class="sxs-lookup"><span data-stu-id="18d85-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="18d85-334">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-334">New</span></span>

* <span data-ttu-id="18d85-335">컨테이너, 테이블, 파일 공유의 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="18d85-336">쿼리 작성기 환경이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-336">Improved Query builder experience</span></span>
* <span data-ttu-id="18d85-337">기능 toosave 및 부하 쿼리</span><span class="sxs-lookup"><span data-stu-id="18d85-337">Ability toosave and load queries</span></span>
* <span data-ttu-id="18d85-338">직접 링크 toostorage 계정 또는 컨테이너, 큐, 테이블 또는 파일 공유를 공유 하 고 쉽게 리소스에 액세스 (Windows 전용-macOS 지원 출시 예정!)</span><span class="sxs-lookup"><span data-stu-id="18d85-338">Direct links toostorage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="18d85-339">기능 toomanage CORS 규칙을 구성 하 고</span><span class="sxs-lookup"><span data-stu-id="18d85-339">Ability toomanage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-340">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-340">Fixes</span></span>

* <span data-ttu-id="18d85-341">수정됨: Microsoft 계정을 8-12시간마다 다시 인증해야 하는 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="18d85-342">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-342">Known Issues</span></span>

* <span data-ttu-id="18d85-343">경우에 따라 hello UI 수 중지 된 것 처럼-이 문제를 해결 하는 사용 하면 hello 창 최대화</span><span class="sxs-lookup"><span data-stu-id="18d85-343">Sometimes hello UI might appear frozen - maximizing hello window helps resolve this issue</span></span>
* <span data-ttu-id="18d85-344">macOS 설치 시 관리자 권한이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="18d85-345">계정 설정 패널 순서 toofilter 구독에 자격 증명 tooreenter 해야 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-345">Account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="18d85-346">파일 공유 이름 바꾸기, blob 컨테이너 및 테이블 메타 데이터 또는 파일 공유 할당량, 공용 액세스 수준 액세스 정책 등 hello 컨테이너의 다른 속성을 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on hello container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="18d85-347">blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="18d85-348">Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="18d85-349">SAS에 연결된 계정 내에서는 리소스 복사 또는 이름 바꾸기가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="18d85-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="18d85-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="18d85-351">버전 0.8.2</span><span class="sxs-lookup"><span data-stu-id="18d85-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="18d85-352">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-352">New</span></span>

* <span data-ttu-id="18d85-353">Storage 계정이 구독별로 그룹화됩니다. 키 또는 SAS를 통해 연결된 개발 Storage 및 리소스는 (로컬 및 연결됨) 노드 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="18d85-354">"Azure 계정 설정" 패널에서 계정을 로그오프할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="18d85-355">프록시 설정을 tooenable 구성 및 로그인 관리</span><span class="sxs-lookup"><span data-stu-id="18d85-355">Configure proxy settings tooenable and manage sign-in</span></span>
* <span data-ttu-id="18d85-356">Blob 임대를 작성/중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-356">Create and break blob leases</span></span>
* <span data-ttu-id="18d85-357">클릭 한 번으로 Blob 컨테이너, 큐, 테이블 및 파일을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-358">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-358">Fixes</span></span>

* <span data-ttu-id="18d85-359">수정됨: .NET 또는 Java 라이브러리와 함께 삽입된 큐 메시지가 Base64에서 올바르게 디코드되지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="18d85-360">수정됨: $metrics 테이블이 Blob Storage 계정에 대해 표시되지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="18d85-361">수정됨: 로컬(개발) 저장소에 대해 테이블 노드가 작동하지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="18d85-362">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-362">Known Issues</span></span>

* <span data-ttu-id="18d85-363">macOS 설치 시 관리자 권한이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="18d85-364">06/15/2016</span><span class="sxs-lookup"><span data-stu-id="18d85-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="18d85-365">버전 0.8.0</span><span class="sxs-lookup"><span data-stu-id="18d85-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="18d85-366">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-366">New</span></span>

* <span data-ttu-id="18d85-367">파일 공유 지원: 파일 및 디렉터리 보기/업로드/다운로드/복사, SAS URI 만들기 및 연결이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="18d85-368">TooStorage SAS Uri 또는 계정 키와 연결 하기 위한 사용자 환경 개선</span><span class="sxs-lookup"><span data-stu-id="18d85-368">Improved user experience for connecting tooStorage with SAS URIs or account keys</span></span>
* <span data-ttu-id="18d85-369">테이블 쿼리 결과를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-369">Export table query results</span></span>
* <span data-ttu-id="18d85-370">테이블 열 다시 정렬 및 사용자 지정이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-370">Table column reordering and customization</span></span>
* <span data-ttu-id="18d85-371">메트릭이 사용하도록 설정된 Storage 계정의 $logs Blob 컨테이너와 $metrics 테이블을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="18d85-372">내보내기 및 가져오기 동작이 개선되어 이제 속성 값 형식이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-373">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-373">Fixes</span></span>

* <span data-ttu-id="18d85-374">수정됨: 큰 Blob를 업로드하거나 다운로드하면 업로드/다운로드가 완전히 진행되지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="18d85-375">고정: 편집, 추가 또는 숫자 문자열 값 ("1")가 있는 엔터티를 가져오는 변환 toodouble</span><span class="sxs-lookup"><span data-stu-id="18d85-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it toodouble</span></span>
* <span data-ttu-id="18d85-376">Hello 로컬 개발 환경에서 문제가 해결된 됨 없습니다 tooexpand hello 테이블 노드</span><span class="sxs-lookup"><span data-stu-id="18d85-376">Fixed: Unable tooexpand hello table node in hello local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="18d85-377">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-377">Known Issues</span></span>

* <span data-ttu-id="18d85-378">$metrics 테이블이 Blob Storage 계정에 대해 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="18d85-379">Base64 인코딩을 사용 하 여 hello 메시지를 인코딩하도록 경우 프로그래밍 방식으로 추가 하는 큐 메시지 제대로 표시 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-379">Queue messages added programmatically may not be displayed correctly if hello messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="18d85-380">05/17/2016</span><span class="sxs-lookup"><span data-stu-id="18d85-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="18d85-381">버전 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="18d85-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="18d85-382">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-382">New</span></span>

* <span data-ttu-id="18d85-383">앱 작동 중단 시의 오류가 보다 효율적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-384">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-384">Fixes</span></span>

* <span data-ttu-id="18d85-385">로그인 자격 증명이 필요할 때 정보 표시줄 메시지가 가끔씩 표시되지 않는 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="18d85-386">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-386">Known Issues</span></span>

* <span data-ttu-id="18d85-387">테이블: 추가, 편집 또는 모호 하 게 숫자 값을 "1" 또는 "1.0"와 같은 속성을 가진 엔터티를 가져오는 및 사용자 시도 toosend hello로 `Edm.String`, hello 값 hello 클라이언트는 Edm.Double로 API 통해 다시 나올지</span><span class="sxs-lookup"><span data-stu-id="18d85-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>

<span data-ttu-id="18d85-388">03/31/2016</span><span class="sxs-lookup"><span data-stu-id="18d85-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="18d85-389">버전 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="18d85-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="18d85-390">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-390">New</span></span>

* <span data-ttu-id="18d85-391">테이블 지원: 엔터티 보기/쿼리/내보내기/가져오기 및 CRUD 작업이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="18d85-392">큐 지원: 메시지 보기, 추가, 큐에서 제거가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="18d85-393">Storage 계정에 대해 SAS URI를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="18d85-394">SAS Uri를 사용 하 여 tooStorage 계정 연결</span><span class="sxs-lookup"><span data-stu-id="18d85-394">Connecting tooStorage Accounts with SAS URIs</span></span>
* <span data-ttu-id="18d85-395">향후 업데이트 tooStorage 탐색기에 대 한 업데이트 알림</span><span class="sxs-lookup"><span data-stu-id="18d85-395">Update notifications for future updates tooStorage Explorer</span></span>
* <span data-ttu-id="18d85-396">디자인이 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-397">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-397">Fixes</span></span>

* <span data-ttu-id="18d85-398">성능과 안정성이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="18d85-399">알려진 문제 &amp; 완화 방법</span><span class="sxs-lookup"><span data-stu-id="18d85-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="18d85-400">큰 Blob 파일 다운로드가 제대로 작동하지 않습니다. 이 문제를 해결하는 방법이 제공될 때까지는 AzCopy를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="18d85-401">계정 자격 증명을 검색할 않았거나 hello 홈 폴더를 찾을 수 없거나에 쓸 수 없는 경우 캐시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-401">Account credentials will not be retrieved nor cached if hello home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="18d85-402">Hello 사용자가 toosend 및 우리는 추가, 편집 또는 모호 하 게 숫자 값을 "1" 또는 "1.0"와 같은 속성을 가진 엔터티를 가져오는 경우로 `Edm.String`, hello 값 hello 클라이언트는 Edm.Double로 API 통해 다시 나올지</span><span class="sxs-lookup"><span data-stu-id="18d85-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>
* <span data-ttu-id="18d85-403">여러 줄로 된 레코드를 사용 하 여 CSV 파일을 가져올 때 hello 데이터 수 되었다고 해 가져오거나 스크램블</span><span class="sxs-lookup"><span data-stu-id="18d85-403">When importing CSV files with multiline records, hello data may get chopped or scrambled</span></span>

<span data-ttu-id="18d85-404">02/03/2016</span><span class="sxs-lookup"><span data-stu-id="18d85-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="18d85-405">버전 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="18d85-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-406">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-406">Fixes</span></span>

* <span data-ttu-id="18d85-407">Blob 업로드, 다운로드 및 복사 시의 전반적인 성능이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="18d85-408">01/14/2016</span><span class="sxs-lookup"><span data-stu-id="18d85-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="18d85-409">버전 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="18d85-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="18d85-410">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-410">New</span></span>

* <span data-ttu-id="18d85-411">Linux 지원 (패리티 기능 tooOSX)</span><span class="sxs-lookup"><span data-stu-id="18d85-411">Linux support (parity features tooOSX)</span></span>
* <span data-ttu-id="18d85-412">SAS(공유 액세스 서명) 키를 사용하여 Blob 컨테이너를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="18d85-413">Azure 중국의 Storage 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="18d85-414">사용자 지정 끝점이 있는 Storage 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="18d85-415">열고 hello 내용을 텍스트와 그림 blob를 보려면</span><span class="sxs-lookup"><span data-stu-id="18d85-415">Open and view hello contents text and picture blobs</span></span>
* <span data-ttu-id="18d85-416">blob 속성 및 메타데이터 보기 및 편집</span><span class="sxs-lookup"><span data-stu-id="18d85-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="18d85-417">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="18d85-417">Fixes</span></span>

* <span data-ttu-id="18d85-418">고정: 업로드 또는 다운로드 많은 수의 blob (500 이상) 될 수 있습니다 하는 경우가 발생할 hello 앱 toohave 흰색 화면</span><span class="sxs-lookup"><span data-stu-id="18d85-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause hello app toohave a white screen</span></span> 
* <span data-ttu-id="18d85-419">고정된: blob 컨테이너 공용 액세스 수준의 설정할 때 hello 새 값 업데이트 되지 않습니다 hello 컨테이너에서 hello 포커스를 다시 설정 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-419">Fixed: when setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container.</span></span> <span data-ttu-id="18d85-420">또한 hello 대화 상자에서 항상 기본값 너무 "public"에 액세스 하 고 hello 실제 현재 값이 아닌 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-420">Also, hello dialog always defaults too"No public access", and not hello actual current value.</span></span>
* <span data-ttu-id="18d85-421">전반적인 키보드/손쉬운 사용 및 UI 지원이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="18d85-422">이동 경로 기록 텍스트가 길면 공백이 추가되어 줄이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="18d85-423">SAS 대화 상자에서 입력 유효성 검사가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="18d85-424">사용자의 자격 증명이 만료 하는 경우에 toobe 사용 가능한 로컬 저장소에 계속</span><span class="sxs-lookup"><span data-stu-id="18d85-424">Local storage continues toobe available even if user credentials have expired</span></span>
* <span data-ttu-id="18d85-425">Hello 오른쪽에 hello blob 탐색기 닫혀 열린된 blob 컨테이너를 삭제 하면</span><span class="sxs-lookup"><span data-stu-id="18d85-425">When an opened blob container is deleted, hello blob explorer on hello right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="18d85-426">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-426">Known Issues</span></span>

* <span data-ttu-id="18d85-427">Gcc 버전 업데이트 또는 업그레이드 – 단계 tooupgrade Linux 설치 요구 사항 아래에</span><span class="sxs-lookup"><span data-stu-id="18d85-427">Linux install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="18d85-428">11/18/2015</span><span class="sxs-lookup"><span data-stu-id="18d85-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="18d85-429">버전 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="18d85-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="18d85-430">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="18d85-430">New</span></span>

* <span data-ttu-id="18d85-431">macOS 및 Windows 버전이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="18d85-432">저장소 계정에서 tooview sign-조직 계정, Microsoft 계정, 2FA, 등을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-432">Sign in tooview your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="18d85-433">로컬 개발 저장소가 제공됩니다(Storage 에뮬레이터 사용, Windows 전용).</span><span class="sxs-lookup"><span data-stu-id="18d85-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="18d85-434">Azure Resource Manager 및 클래식 리소스가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="18d85-435">Blob, 큐 또는 테이블을 만들고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="18d85-436">특정 Blob, 큐 또는 테이블을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="18d85-437">Blob 컨테이너의 내용을 hello 탐색</span><span class="sxs-lookup"><span data-stu-id="18d85-437">Explore hello contents of blob containers</span></span>
* <span data-ttu-id="18d85-438">디렉터리를 보고 디렉터리 간을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-438">View and navigate through directories</span></span>
* <span data-ttu-id="18d85-439">Blob와 폴더를 업로드, 다운로드 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="18d85-440">blob 속성 및 메타데이터 보기 및 편집</span><span class="sxs-lookup"><span data-stu-id="18d85-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="18d85-441">SAS 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-441">Generate SAS keys</span></span>
* <span data-ttu-id="18d85-442">SAP(저장된 액세스 정책)를 관리하고 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="18d85-443">접두사별로 blob 검색</span><span class="sxs-lookup"><span data-stu-id="18d85-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="18d85-444">' N 파일 tooupload drop 끌거나 다운로드</span><span class="sxs-lookup"><span data-stu-id="18d85-444">Drag 'n drop files tooupload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="18d85-445">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18d85-445">Known Issues</span></span>

* <span data-ttu-id="18d85-446">Blob 컨테이너 공용 액세스 수준의 설정할 때 hello 컨테이너에서 hello 포커스를 다시 설정 하기 전에 hello 새 값 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-446">When setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container</span></span>
* <span data-ttu-id="18d85-447">Hello 실제 현재 값이 아닌 hello 기본적으로 "공용 액세스 권한이" hello 대화 tooset hello 공용 액세스 수준의 열 때 항상 표시</span><span class="sxs-lookup"><span data-stu-id="18d85-447">When you open hello dialog tooset hello public access level, it always shows "No public access" as hello default, and not hello actual current value</span></span>
* <span data-ttu-id="18d85-448">다운로드한 Blob 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="18d85-449">이 경우에 따라 "중단"에서 진행 중인 활동 로그 항목 상태 때 오류가 발생 하 고 hello 오류가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and hello error is not displayed</span></span>
* <span data-ttu-id="18d85-450">경우에 따라 중단을 일으키거나 turns 완전히 흰색 tooupload 하려고 할 때 또는 다 수의 blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="18d85-450">Sometimes crashes or turns completely white when trying tooupload or download a large number of blobs</span></span>
* <span data-ttu-id="18d85-451">가끔씩 복사 작업을 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="18d85-452">(테이블/blob/큐) 컨테이너를 만드는 동안 잘못 된 이름을 입력 하 고 toocreate 진행 하는 경우 서로 다른 컨테이너 형식에서 다른 설정할 수 없습니다 포커스 hello 새 형식</span><span class="sxs-lookup"><span data-stu-id="18d85-452">During creating a container (blob/queue/table), if you input an invalid name and proceed toocreate another under a different container type you cannot set focus on hello new type</span></span>
* <span data-ttu-id="18d85-453">새 폴더를 만들거나 폴더 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18d85-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md