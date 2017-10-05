---
title: "Microsoft Azure Storage 탐색기(미리 보기) 릴리스 정보 | Microsoft 문서"
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
ms.openlocfilehash: 63a24f6b153390533bba0888fd1051508c65bf6e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="c4296-103">Microsoft Azure Storage 탐색기(미리 보기) 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="c4296-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="c4296-104">이 문서에서는 Azure Storage 탐색기 0.8.16(미리 보기) 릴리스의 릴리스 정보와 이전 버전의 릴리스 정보를 모두 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-104">This article contains the release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="c4296-105">[Microsoft Azure Storage 탐색기(미리 보기)](./vs-azure-tools-storage-manage-with-storage-explorer.md)는 Windows, macOS 및 Linux에서 Azure Storage 데이터를 손쉽게 사용할 수 있는 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="c4296-106">버전 0.8.16(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="c4296-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="c4296-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="c4296-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="c4296-108">Azure Storage 탐색기 0.8.16(미리 보기) 다운로드</span><span class="sxs-lookup"><span data-stu-id="c4296-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="c4296-109">Windows용 Azure Storage 탐색기 0.8.16(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="c4296-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="c4296-110">Mac용 Azure Storage 탐색기 0.8.16(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="c4296-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="c4296-111">Linux용 Azure Storage 탐색기 0.8.16(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="c4296-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="c4296-112">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-112">New</span></span>
* <span data-ttu-id="c4296-113">Blob을 열 때 저장소 탐색기는 변경 내용이 감지될 경우 다운로드한 파일을 업로드할지 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-113">When you open a blob, Storage Explorer will prompt you to upload the downloaded file if a change is detected</span></span>
* <span data-ttu-id="c4296-114">향상된 Azure Stack 로그인 환경</span><span class="sxs-lookup"><span data-stu-id="c4296-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="c4296-115">여러 개의 작은 파일을 동시에 업로드/다운로드하는 성능 개선</span><span class="sxs-lookup"><span data-stu-id="c4296-115">Improved the performance of uploading/downloading many small files at the same time</span></span>


### <a name="fixes"></a><span data-ttu-id="c4296-116">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-116">Fixes</span></span>
* <span data-ttu-id="c4296-117">일부 blob 형식의 경우 업로드 중에 "바꾸기"를 선택하면 충돌이 발생해서 업로드가 다시 시작될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-117">For some blob types, choosing to "replace" during an upload conflict would sometimes result in the upload being restarted.</span></span> 
* <span data-ttu-id="c4296-118">버전 0.8.15에서 업로드는 경우에 따라 99%에서 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="c4296-119">파일을 파일 공유에 업로드할 때 아직 존재하지 않는 디렉터리로 업로드하도록 선택하면 업로드가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-119">When uploading files to a file share, if you chose to upload to a directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="c4296-120">저장소 탐색기가 공유 액세스 서명 및 테이블 쿼리에 대한 타임스탬프를 잘못 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="c4296-121">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-121">Known Issues</span></span>
* <span data-ttu-id="c4296-122">현재 이름 및 키 연결 문자열을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="c4296-123">이 문제는 다음 릴리스에서 해결될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-123">It will be fixed in the next release.</span></span> <span data-ttu-id="c4296-124">그때까지는 이름 및 키로 연결 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="c4296-125">잘못된 Windows 파일 이름을 갖는 파일을 열려고 하면 다운로드 시 파일을 찾을 수 없음 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-125">If you try to open a file with an invalid Windows file name, the download will result in a file not found error.</span></span>
* <span data-ttu-id="c4296-126">작업에서 "취소"를 클릭한 후 해당 작업이 취소될 때까지 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-126">After clicking "Cancel" on a task, it may take a while for that task to cancel.</span></span> <span data-ttu-id="c4296-127">이것은 Azure Storage 노드 라이브러리의 제한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-127">This is a limitation of the Azure Storage Node library.</span></span>
* <span data-ttu-id="c4296-128">Blob 업로드를 완료한 후 업로드를 시작한 탭이 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-128">After completing a blob upload, the tab which initiated the upload is refreshed.</span></span> <span data-ttu-id="c4296-129">이러한 현상은 이전과 다르게 변경된 동작이며, 해당 동작으로 인해 현재 표시되어 있는 컨테이너의 루트로 다시 이동하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-129">This is a change from previous behavior, and will also cause you to be taken back to the root of the container you are in.</span></span>
* <span data-ttu-id="c4296-130">잘못된 PIN/스마트 카드 인증서를 선택하는 경우 해당 선택을 취소하려면 저장소 탐색기를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-130">If you choose the wrong PIN/Smartcard certificate, then you will need to restart in order to have Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="c4296-131">계정 설정 패널에 구독을 필터링하기 위해 자격 증명을 다시 입력하라고 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-131">The account settings panel may show that you need to reenter credentials to filter subscriptions.</span></span>
* <span data-ttu-id="c4296-132">blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="c4296-133">Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="c4296-134">Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="c4296-135">Ubuntu 14.04 사용자의 경우 GCC가 최신 상태인지 확인해야 합니다. 이를 위해 다음 명령을 실행한 후 컴퓨터를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-135">For users on Ubuntu 14.04, you will need to ensure GCC is up to date - this can be done by running the following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="c4296-136">Ubuntu 17.04 사용자의 경우에는 GConf를 설치해야 합니다. 이렇게 하려면 다음 명령을 실행한 후 컴퓨터를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-136">For users on Ubuntu 17.04, you will need to install GConf - this can be done by running the following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="c4296-137">버전 0.8.14(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="c4296-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="c4296-138">06/22/2017</span><span class="sxs-lookup"><span data-stu-id="c4296-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="c4296-139">Azure Storage 탐색기 0.8.14(미리 보기) 다운로드</span><span class="sxs-lookup"><span data-stu-id="c4296-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="c4296-140">Windows용 Azure Storage 탐색기 0.8.14(미리 보기) 다운로드</span><span class="sxs-lookup"><span data-stu-id="c4296-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="c4296-141">Mac용 Azure Storage 탐색기 0.8.14(미리 보기) 다운로드</span><span class="sxs-lookup"><span data-stu-id="c4296-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="c4296-142">Linux용 Azure Storage 탐색기 0.8.14(미리 보기) 다운로드</span><span class="sxs-lookup"><span data-stu-id="c4296-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="c4296-143">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-143">New</span></span>

* <span data-ttu-id="c4296-144">여러 중요 보안 업데이트를 활용하기 위해 Electron 버전이 1.7.2로 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-144">Updated Electron version to 1.7.2 in order to take advantage of several critical security updates</span></span>
* <span data-ttu-id="c4296-145">이제 도움말 메뉴에서 온라인 문제 해결 가이드에 빠르게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-145">You can now quickly access the online troubleshooting guide from the help menu</span></span>
* <span data-ttu-id="c4296-146">Storage 탐색기 문제 해결 [가이드][2]</span><span class="sxs-lookup"><span data-stu-id="c4296-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="c4296-147">Azure Stack 구독 연결 관련 [지침][3]</span><span class="sxs-lookup"><span data-stu-id="c4296-147">[Instructions][3] on connecting to an Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="c4296-148">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-148">Known Issues</span></span>

* <span data-ttu-id="c4296-149">Linux에서 마우스를 클릭해도 폴더 삭제 확인 대화 상자의 단추가 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-149">Buttons on the delete folder confirmation dialog don't register with the mouse clicks on Linux.</span></span> <span data-ttu-id="c4296-150">이 문제를 해결하려면 Enter 키를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="c4296-150">Workaround is to use the Enter key</span></span>
* <span data-ttu-id="c4296-151">잘못된 PIN/스마트 카드 인증서를 선택하는 경우 해당 선택을 취소하려면 Storage 탐색기를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-151">If you choose the wrong PIN/Smartcard certificate then you will need to restart in order to have Storage Explorer forget the decision</span></span>
* <span data-ttu-id="c4296-152">4개 이상의 Blob 또는 파일 그룹을 동시에 업로드하면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-152">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="c4296-153">계정 설정 패널에 구독을 필터링하려면 자격 증명을 다시 입력하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-153">The account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="c4296-154">blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="c4296-155">Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="c4296-156">Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="c4296-157">Ubuntu 14.04 설치 시에는 gcc 버전을 업데이트하거나 업그레이드해야 합니다. 업그레이드 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="c4296-158">이전 릴리스</span><span class="sxs-lookup"><span data-stu-id="c4296-158">Previous releases</span></span>

* [<span data-ttu-id="c4296-159">버전 0.8.13</span><span class="sxs-lookup"><span data-stu-id="c4296-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="c4296-160">버전 0.8.12/0.8.11/0.8.10</span><span class="sxs-lookup"><span data-stu-id="c4296-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="c4296-161">버전 0.8.9/0.8.8</span><span class="sxs-lookup"><span data-stu-id="c4296-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="c4296-162">버전 0.8.7</span><span class="sxs-lookup"><span data-stu-id="c4296-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="c4296-163">버전 0.8.6</span><span class="sxs-lookup"><span data-stu-id="c4296-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="c4296-164">버전 0.8.5</span><span class="sxs-lookup"><span data-stu-id="c4296-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="c4296-165">버전 0.8.4</span><span class="sxs-lookup"><span data-stu-id="c4296-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="c4296-166">버전 0.8.3</span><span class="sxs-lookup"><span data-stu-id="c4296-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="c4296-167">버전 0.8.2</span><span class="sxs-lookup"><span data-stu-id="c4296-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="c4296-168">버전 0.8.0</span><span class="sxs-lookup"><span data-stu-id="c4296-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="c4296-169">버전 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="c4296-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="c4296-170">버전 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="c4296-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="c4296-171">버전 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="c4296-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="c4296-172">버전 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="c4296-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="c4296-173">버전 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="c4296-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="c4296-174">버전 0.8.13</span><span class="sxs-lookup"><span data-stu-id="c4296-174">Version 0.8.13</span></span>
<span data-ttu-id="c4296-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="c4296-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="c4296-176">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-176">New</span></span>

* <span data-ttu-id="c4296-177">Storage 탐색기 문제 해결 [가이드][2]</span><span class="sxs-lookup"><span data-stu-id="c4296-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="c4296-178">Azure Stack 구독 연결 관련 [지침][3]</span><span class="sxs-lookup"><span data-stu-id="c4296-178">[Instructions][3] on connecting to an Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-179">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-179">Fixes</span></span>

* <span data-ttu-id="c4296-180">수정됨: 파일 업로드 시의 높은 메모리 부족 오류 발생 가능성이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="c4296-181">수정됨: 이제 PIN/스마트 카드를 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="c4296-182">수정됨: 이제 포털에서 열기가 Azure 중국, Azure 독일, Azure 미국 정부 및 Azure Stack에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="c4296-183">수정됨: Blob 컨테이너에 폴더를 업로드하는 중에 가끔씩 "잘못된 작업입니다."라는 오류가 발생하는 현상이 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-183">Fixed: While uploading a folder to a blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="c4296-184">수정됨: 스냅숏을 관리하는 동안 모두 선택 기능이 사용할 수 없도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="c4296-185">수정됨: 기본 Blob의 메타데이터 스냅숏 속성을 확인하고 나면 해당 메타데이터가 덮어쓰여질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-185">Fixed: The metadata of the base blob might get overwritten after viewing the properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4296-186">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-186">Known Issues</span></span>

* <span data-ttu-id="c4296-187">잘못된 PIN/스마트 카드 인증서를 선택하는 경우 해당 선택을 취소하려면 Storage 탐색기를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-187">If you choose the wrong PIN/Smartcard certificate then you will need to restart in order to have Storage Explorer forget the decision</span></span>
* <span data-ttu-id="c4296-188">확대하거나 축소하는 동안 확대/축소 수준이 잠시 동안 기본 수준으로 다시 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-188">While zoomed in or out, the zoom level may momentarily reset to the default level</span></span>
* <span data-ttu-id="c4296-189">4개 이상의 Blob 또는 파일 그룹을 동시에 업로드하면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-189">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="c4296-190">계정 설정 패널에 구독을 필터링하려면 자격 증명을 다시 입력하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-190">The account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="c4296-191">blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="c4296-192">Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="c4296-193">Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="c4296-194">Ubuntu 14.04 설치 시에는 gcc 버전을 업데이트하거나 업그레이드해야 합니다. 업그레이드 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="c4296-195">버전 0.8.12/0.8.11/0.8.10</span><span class="sxs-lookup"><span data-stu-id="c4296-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="c4296-196">04/07/2017</span><span class="sxs-lookup"><span data-stu-id="c4296-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="c4296-197">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-197">New</span></span>

* <span data-ttu-id="c4296-198">이제 업데이트 알림에서 업데이트를 설치할 때 Storage 탐색기가 자동으로 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-198">Storage Explorer will now automatically close when you install an update from the update notification</span></span>
* <span data-ttu-id="c4296-199">현재 위치 빠른 액세스 기능이 자주 액세스하는 리소스 사용을 위한 향상된 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="c4296-200">이제 Blob 컨테이너 편집기에서 임대한 Blob가 속하는 가상 컴퓨터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-200">In the Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="c4296-201">이제 왼쪽 가로 패널을 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-201">You can now collapse the left side panel</span></span>
* <span data-ttu-id="c4296-202">이제 검색이 다운로드와 동시에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-202">Discovery now runs at the same time as download</span></span>
* <span data-ttu-id="c4296-203">Blob 컨테이너, 파일 공유 및 테이블 편집기에서 통계를 사용하여 리소스 또는 선택 항목의 크기를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-203">Use Statistics in the Blob Container, File Share, and Table editors to see the size of your resource or selection</span></span>
* <span data-ttu-id="c4296-204">이제 Azure Stack 계정을 기준으로 AAD(Azure Active Directory)에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-204">You can now sign-in to Azure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="c4296-205">이제 Premium Storage 계정에 32MB가 넘는 보관 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-205">You can now upload archive files over 32MB to Premium storage accounts</span></span>
* <span data-ttu-id="c4296-206">손쉬운 사용 옵션 지원이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-206">Improved accessibility support</span></span>
* <span data-ttu-id="c4296-207">이제 편집 -&gt; SSL 인증서 -&gt; 인증서 가져오기로 이동하여 신뢰할 수 있는 Base64 인코딩 X.509 SSL 인증서를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going to Edit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-208">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-208">Fixes</span></span>

* <span data-ttu-id="c4296-209">수정됨: 계정의 자격 증명을 새로 고친 후 트리 뷰가 가끔씩 자동으로 새로 고쳐지지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-209">Fixed: after refreshing an account's credentials, the tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="c4296-210">수정됨: 에뮬레이터 큐 및 테이블에 대해 SAS를 생성하면 잘못된 URL이 생성되는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="c4296-211">수정됨: 이제 프록시가 사용하도록 설정된 상태에서 Premium Storage 계정을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="c4296-212">수정됨: 계정을 1개 또는 0개를 선택하면 계정 관리 페이지의 적용 단추가 작동하지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-212">Fixed: the apply button on the accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="c4296-213">수정됨: 충돌을 해결해야 하는 Blob 업로드가 실패할 수 있는 현상이 버전 0.8.11에서 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="c4296-214">수정됨: 버전 0.8.11에서 피드백 전송이 중단되는 현상이 버전 0.8.12에서 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="c4296-215">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-215">Known Issues</span></span>

* <span data-ttu-id="c4296-216">0.8.10으로 업그레이드한 후에는 모든 자격 증명을 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-216">After upgrading to 0.8.10, you will need to refresh all of your credentials.</span></span>
* <span data-ttu-id="c4296-217">확대하거나 축소하는 동안 확대/축소 수준이 잠시 동안 기본 수준으로 다시 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-217">While zoomed in or out, the zoom level may momentarily reset to the default level.</span></span>
* <span data-ttu-id="c4296-218">4개 이상의 Blob 또는 파일 그룹을 동시에 업로드하면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-218">Having more than 3 groups of blobs or files uploading at the same time may cause errors.</span></span>
* <span data-ttu-id="c4296-219">계정 설정 패널에 구독을 필터링하려면 자격 증명을 다시 입력하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-219">The account settings panel may show that you need to reenter credentials in order to filter subscriptions.</span></span>
* <span data-ttu-id="c4296-220">blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="c4296-221">Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="c4296-222">Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="c4296-223">Ubuntu 14.04 설치 시에는 gcc 버전을 업데이트하거나 업그레이드해야 합니다. 업그레이드 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="c4296-224">버전 0.8.9/0.8.8</span><span class="sxs-lookup"><span data-stu-id="c4296-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="c4296-225">02/23/2017</span><span class="sxs-lookup"><span data-stu-id="c4296-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="c4296-226">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-226">New</span></span>

* <span data-ttu-id="c4296-227">Storage 탐색기 0.8.9는 업데이트를 위해 최신 버전을 자동으로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-227">Storage Explorer 0.8.9 will automatically download the latest version for updates.</span></span>
* <span data-ttu-id="c4296-228">핫픽스: 포털에서 생성한 SAS URI를 사용하여 Storage 계정을 연결하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-228">Hotfix: using a portal generated SAS URI to attach a storage account would result in an error.</span></span>
* <span data-ttu-id="c4296-229">이제 Blob 스냅숏을 만들고 관리하고 수준을 올릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="c4296-230">이제 Azure 중국, Azure 독일 및 Azure 미국 정부 계정에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-230">You can now sign in to Azure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="c4296-231">이제 확대/축소 수준을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-231">You can now change the zoom level.</span></span> <span data-ttu-id="c4296-232">보기 메뉴의 옵션을 사용하여 확대, 축소 및 확대/축소 다시 설정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-232">Use the options in the View menu to Zoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="c4296-233">이제 Blob 및 파일의 사용자 메타데이터에서 유니코드 문자가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="c4296-234">내게 필요한 옵션이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-234">Accessibility improvements.</span></span>
* <span data-ttu-id="c4296-235">업데이트 알림에서 다음 버전의 릴리스 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-235">The next version's release notes can be viewed from the update notification.</span></span> <span data-ttu-id="c4296-236">또한 도움말 메뉴에서 현재 릴리스 정보를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-236">You can also view the current release notes from the Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-237">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-237">Fixes</span></span>

* <span data-ttu-id="c4296-238">수정됨: 이제 Windows의 제어판에서 버전 번호가 올바르게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-238">Fixed: the version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="c4296-239">수정됨: 검색 가능한 노드 수가 더 이상 50,000개로 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-239">Fixed: search is no longer limited to 50,000 nodes</span></span>
* <span data-ttu-id="c4296-240">수정됨: 대상 디렉터리가 없으면 파일 공유로의 업로드가 무한 반복되는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-240">Fixed: upload to a file share spun forever if the destination directory did not already exist</span></span>
* <span data-ttu-id="c4296-241">수정됨: 오랫동안 실행되는 업로드와 다운로드의 안정성이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4296-242">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-242">Known Issues</span></span>

* <span data-ttu-id="c4296-243">확대하거나 축소하는 동안 확대/축소 수준이 잠시 동안 기본 수준으로 다시 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-243">While zoomed in or out, the zoom level may momentarily reset to the default level.</span></span>
* <span data-ttu-id="c4296-244">빠른 액세스는 구독 기반 항목에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="c4296-245">로컬 리소스 또는 키나 SAS 토큰을 통해 연결된 리소스는 이번 릴리스에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="c4296-246">보유하고 있는 리소스 수에 따라 빠른 액세스 기능으로 대상 리소스에 액세스하는 데 몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-246">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="c4296-247">4개 이상의 Blob 또는 파일 그룹을 동시에 업로드하면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-247">Having more than 3 groups of blobs or files uploading at the same time may cause errors.</span></span>

<span data-ttu-id="c4296-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="c4296-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="c4296-249">버전 0.8.7</span><span class="sxs-lookup"><span data-stu-id="c4296-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="c4296-250">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-250">New</span></span>

* <span data-ttu-id="c4296-251">이제 활동 창에서 업데이트, 다운로드 또는 복사 세션을 시작할 때 발생하는 충돌을 해결하는 방법을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-251">You can choose how to resolve conflicts at the beginning of an update, download or copy session in the Activities window</span></span>
* <span data-ttu-id="c4296-252">Storage 리소스의 전체 경로를 보려면 탭 위로 마우스를 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-252">Hover over a tab to see the full path of the storage resource</span></span>
* <span data-ttu-id="c4296-253">탭을 클릭하면 왼쪽 탐색 창의 해당 위치와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-253">When you click on a tab, it synchronizes with its location in the left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-254">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-254">Fixes</span></span>

* <span data-ttu-id="c4296-255">수정됨: 이제 Mac에서도 Storage 탐색기를 신뢰할 수 있는 앱으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="c4296-256">수정됨: Ubuntu 14.04가 다시 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="c4296-257">수정됨: 구독을 로드할 때 계정 추가 UI가 가끔씩 깜박이는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-257">Fixed: Sometimes the add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="c4296-258">수정됨: 가끔씩 왼쪽 탐색 창에 일부 Storage 리소스가 나열되지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-258">Fixed: Sometimes not all storage resources were listed in the left side navigation pane</span></span>
* <span data-ttu-id="c4296-259">수정됨: 작업 창에 가끔씩 빈 작업이 표시되는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-259">Fixed: The action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="c4296-260">수정됨: 이제 마지막에 닫은 세션의 창 크기가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-260">Fixed: The window size from the last closed session is now retained</span></span>
* <span data-ttu-id="c4296-261">수정됨: 상황에 맞는 메뉴를 사용하는 동일한 리소스에 대해 여러 탭을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-261">Fixed: You can open multiple tabs for the same resource using the context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4296-262">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-262">Known Issues</span></span>

* <span data-ttu-id="c4296-263">빠른 액세스는 구독 기반 항목에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="c4296-264">로컬 리소스 또는 키나 SAS 토큰을 통해 연결된 리소스는 이번 릴리스에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="c4296-265">보유하고 있는 리소스 수에 따라 빠른 액세스 기능으로 대상 리소스로 이동하는 데 몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-265">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="c4296-266">4개 이상의 Blob 또는 파일 그룹을 동시에 업로드하면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-266">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="c4296-267">검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하되거나 처리되지 않은 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="c4296-268">Mac OS에서 Storage 탐색기를 처음 사용할 때 사용자의 키 집합 액세스 권한을 묻는 메시지가 여러 번 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-268">For the first time using the Storage Explorer on macOS, you might see multiple prompts asking for user's permission to access keychain.</span></span> <span data-ttu-id="c4296-269">확인 메시지가 다시 표시되지 않도록 항상 허용을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-269">We suggest you select Always Allow so the prompt won't show up again</span></span>

<span data-ttu-id="c4296-270">11/18/2016</span><span class="sxs-lookup"><span data-stu-id="c4296-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="c4296-271">버전 0.8.6</span><span class="sxs-lookup"><span data-stu-id="c4296-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="c4296-272">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-272">New</span></span>

* <span data-ttu-id="c4296-273">쉬운 탐색을 위해 가장 자주 사용되는 서비스를 빠른 액세스 기능에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-273">You can now pin most frequently used services to the Quick Access for easy navigation</span></span>
* <span data-ttu-id="c4296-274">이제 다른 탭에 있는 여러 편집기를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="c4296-275">한 번 클릭하면 임시 탭이 열리고, 두 번 클릭하면 영구 탭이 열립니다. 임시 탭을 클릭하여 영구 탭으로 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-275">Single click to open a temporary tab; double click to open a permanent tab. You can also click on the temporary tab to make it a permanent tab</span></span>
* <span data-ttu-id="c4296-276">특히 빠른 컴퓨터에서 큰 파일에 대해 업로드 및 다운로드를 수행할 때 성능 및 안정성이 크게 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="c4296-277">이제 blob 컨테이너에 빈 "가상" 폴더를 만들 수 있음</span><span class="sxs-lookup"><span data-stu-id="c4296-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="c4296-278">새롭게 향상된 하위 문자열 검색에 범위 지정 검색 기능이 다시 도입되었으므로 이제 검색 시에 다음의 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="c4296-279">전체 검색 - 검색 입력란에 검색 용어만 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-279">Global search - just enter a search term into the search textbox</span></span>
    * <span data-ttu-id="c4296-280">범위 지정 검색 - 노드 옆의 돋보기 아이콘을 클릭하고 경로 끝에 검색 용어를 추가하거나 마우스 오른쪽 단추를 클릭하고 "여기에서 검색"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-280">Scoped search - click the magnifying glass icon next to a node, then add a search term to the end of the path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="c4296-281">밝게(기본값), 어둡게, 고대비 검정 및 고대비 흰색 등의 다양한 테마를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="c4296-282">편집 -&gt; 테마로 이동하여 테마 기본 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-282">Go to Edit -&gt; Themes to change your theming preference</span></span>
* <span data-ttu-id="c4296-283">Blob 및 파일 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="c4296-284">이제 인코딩된 큐 메시지(Base64)와 인코딩되지 않은 큐 메시지가 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="c4296-285">이제 Linux에서는 64비트 OS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="c4296-286">이번 릴리스에서는 64비트 Ubuntu 16.04.1 LTS만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="c4296-287">로고가 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-288">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-288">Fixes</span></span>

* <span data-ttu-id="c4296-289">수정됨: 화면 중단 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="c4296-290">수정됨: 향상된 보안</span><span class="sxs-lookup"><span data-stu-id="c4296-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="c4296-291">수정됨: 가끔씩 연결된 계정이 중복으로 표시되는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="c4296-292">수정됨: Blob의 콘텐츠 형식이 정의되어 있지 않으면 예외가 발생할 수 있는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="c4296-293">수정됨: 빈 테이블에서 쿼리 패널을 열 수 없는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-293">Fixed: Opening the Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="c4296-294">수정됨: 검색의 버그가 확인 및 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="c4296-295">수정됨: "추가 로드"를 클릭하면 로드되는 리소스의 수가 50개에서 100개로 늘어났습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-295">Fixed: Increased the number of resources loaded from 50 to 100 when clicking "Load More"</span></span>
* <span data-ttu-id="c4296-296">수정됨: 이제는 첫 실행 시 계정에 로그인하면 기본적으로 해당 계정의 모든 구독이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="c4296-297">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-297">Known Issues</span></span>

* <span data-ttu-id="c4296-298">Ubuntu 14.04에서는 이 Storage 탐색기 릴리스가 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-298">This release of the Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="c4296-299">같은 리소스에 대해 여러 탭을 열려는 경우 같은 리소스를 계속해서 클릭하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c4296-299">To open multiple tabs for the same resource, do not continuously click on the same resource.</span></span> <span data-ttu-id="c4296-300">다른 리소스를 클릭한 후에 다시 돌아가서 원래 리소스를 클릭하여 다른 탭에서 다시 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-300">Click on another resource and then go back and then click on the original resource to open it again in another tab</span></span> 
* <span data-ttu-id="c4296-301">빠른 액세스는 구독 기반 항목에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="c4296-302">로컬 리소스 또는 키나 SAS 토큰을 통해 연결된 리소스는 이번 릴리스에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="c4296-303">보유하고 있는 리소스 수에 따라 빠른 액세스 기능으로 대상 리소스로 이동하는 데 몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-303">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="c4296-304">4개 이상의 Blob 또는 파일 그룹을 동시에 업로드하면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-304">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="c4296-305">검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하되거나 처리되지 않은 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="c4296-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="c4296-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="c4296-307">버전 0.8.5</span><span class="sxs-lookup"><span data-stu-id="c4296-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="c4296-308">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-308">New</span></span>

* <span data-ttu-id="c4296-309">이제 Portal에서 생성된 SAS 키를 사용하여 Storage 계정 및 리소스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-309">Can now use Portal-generated SAS keys to attach to Storage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-310">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-310">Fixes</span></span>

* <span data-ttu-id="c4296-311">수정됨: 검색 중에 경합 상태가 발생하면 가끔씩 노드를 확장할 수 없게 되는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-311">Fixed: race condition during search sometimes caused nodes to become non-expandable</span></span>
* <span data-ttu-id="c4296-312">수정됨: 계정 이름과 키를 사용하여 Storage 계정에 연결할 때 "HTTP 사용"이 작동하지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-312">Fixed: "Use HTTP" doesn't work when connecting to Storage Accounts with account name and key</span></span>
* <span data-ttu-id="c4296-313">수정됨: SAS 키(구체적으로는 Portal에서 생성된 키)에서 "후행 슬래시" 오류가 반환되는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="c4296-314">수정됨: 테이블 가져오기 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="c4296-315">가끔씩 파티션 키와 행 키가 서로 바뀌는 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="c4296-316">"null" 파티션 키를 읽을 수 없는 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-316">Unable to read "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4296-317">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-317">Known Issues</span></span>

* <span data-ttu-id="c4296-318">검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="c4296-319">Azure Stack은 현재 파일을 지원하지 않으므로 파일을 확장하려고 하면 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-319">Azure Stack doesn't currently support Files, so trying to expand Files will show an error</span></span>

<span data-ttu-id="c4296-320">09/12/2016</span><span class="sxs-lookup"><span data-stu-id="c4296-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="c4296-321">버전 0.8.4</span><span class="sxs-lookup"><span data-stu-id="c4296-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="c4296-322">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-322">New</span></span>

* <span data-ttu-id="c4296-323">리소스를 공유하고 쉽게 액세스하기 위해 Storage 계정, 컨테이너, 큐, 테이블 또는 파일 공유에 대한 직접 링크를 생성할 수 있습니다(Windows 및 Mac OS 지원).</span><span class="sxs-lookup"><span data-stu-id="c4296-323">Generate direct links to storage accounts, containers, queues, tables, or file shares for sharing and easy access to your resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="c4296-324">검색 상자에서 Blob 컨테이너, 테이블, 큐, 파일 공유 또는 저장소 계정 검색</span><span class="sxs-lookup"><span data-stu-id="c4296-324">Search for your blob containers, tables, queues, file shares, or storage accounts from the search box</span></span>
* <span data-ttu-id="c4296-325">이제 테이블 쿼리 작성기에서 절을 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-325">You can now group clauses in the table query builder</span></span>
* <span data-ttu-id="c4296-326">SAS에 연결된 계정 및 컨테이너 내에서 Blob 컨테이너, 파일 공유, 테이블, Blob, Blob 폴더, 파일 및 디렉터리 복사/붙여넣기 및 이름 바꾸기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="c4296-327">이제 Blob 컨테이너와 파일 공유의 이름 바꾸기 및 복사 시에 속성과 메타데이터가 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-328">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-328">Fixes</span></span>

* <span data-ttu-id="c4296-329">수정됨: 부울 또는 이진 속성을 포함하는 테이블 엔터티를 편집할 수 없는 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4296-330">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-330">Known Issues</span></span>

* <span data-ttu-id="c4296-331">검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="c4296-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="c4296-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="c4296-333">버전 0.8.3</span><span class="sxs-lookup"><span data-stu-id="c4296-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="c4296-334">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-334">New</span></span>

* <span data-ttu-id="c4296-335">컨테이너, 테이블, 파일 공유의 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="c4296-336">쿼리 작성기 환경이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-336">Improved Query builder experience</span></span>
* <span data-ttu-id="c4296-337">쿼리를 저장하고 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-337">Ability to save and load queries</span></span>
* <span data-ttu-id="c4296-338">리소스를 공유하고 쉽게 액세스하기 위해 Storage 계정, 컨테이너, 큐, 테이블 또는 파일 공유에 대한 직접 링크를 생성할 수 있습니다(Windows 전용/Mac OS는 조만간 지원될 예정).</span><span class="sxs-lookup"><span data-stu-id="c4296-338">Direct links to storage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="c4296-339">CORS 규칙을 관리 및 구성하는 기능</span><span class="sxs-lookup"><span data-stu-id="c4296-339">Ability to manage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-340">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-340">Fixes</span></span>

* <span data-ttu-id="c4296-341">수정됨: Microsoft 계정을 8-12시간마다 다시 인증해야 하는 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4296-342">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-342">Known Issues</span></span>

* <span data-ttu-id="c4296-343">가끔씩 UI가 중지된 것처럼 보일 수 있습니다. 창을 최대화하면 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-343">Sometimes the UI might appear frozen - maximizing the window helps resolve this issue</span></span>
* <span data-ttu-id="c4296-344">macOS 설치 시 관리자 권한이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="c4296-345">계정 설정 패널에 구독을 필터링하려면 자격 증명을 다시 입력하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-345">Account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="c4296-346">파일 공유, Blob 컨테이너 및 테이블의 이름을 바꾸면 파일 공유 할당량, 공용 액세스 수준, 액세스 정책 등 컨테이너에 대한 메타데이터나 기타 속성이 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on the container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="c4296-347">blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="c4296-348">Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="c4296-349">SAS에 연결된 계정 내에서는 리소스 복사 또는 이름 바꾸기가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="c4296-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="c4296-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="c4296-351">버전 0.8.2</span><span class="sxs-lookup"><span data-stu-id="c4296-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="c4296-352">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-352">New</span></span>

* <span data-ttu-id="c4296-353">Storage 계정이 구독별로 그룹화됩니다. 키 또는 SAS를 통해 연결된 개발 Storage 및 리소스는 (로컬 및 연결됨) 노드 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="c4296-354">"Azure 계정 설정" 패널에서 계정을 로그오프할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="c4296-355">로그인을 사용 및 관리하도록 프록시 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-355">Configure proxy settings to enable and manage sign-in</span></span>
* <span data-ttu-id="c4296-356">Blob 임대를 작성/중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-356">Create and break blob leases</span></span>
* <span data-ttu-id="c4296-357">클릭 한 번으로 Blob 컨테이너, 큐, 테이블 및 파일을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-358">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-358">Fixes</span></span>

* <span data-ttu-id="c4296-359">수정됨: .NET 또는 Java 라이브러리와 함께 삽입된 큐 메시지가 Base64에서 올바르게 디코드되지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="c4296-360">수정됨: $metrics 테이블이 Blob Storage 계정에 대해 표시되지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="c4296-361">수정됨: 로컬(개발) 저장소에 대해 테이블 노드가 작동하지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4296-362">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-362">Known Issues</span></span>

* <span data-ttu-id="c4296-363">macOS 설치 시 관리자 권한이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="c4296-364">06/15/2016</span><span class="sxs-lookup"><span data-stu-id="c4296-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="c4296-365">버전 0.8.0</span><span class="sxs-lookup"><span data-stu-id="c4296-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="c4296-366">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-366">New</span></span>

* <span data-ttu-id="c4296-367">파일 공유 지원: 파일 및 디렉터리 보기/업로드/다운로드/복사, SAS URI 만들기 및 연결이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="c4296-368">SAS URI 또는 계정 키를 사용하여 Storage에 연결하기 위한 사용자 환경이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-368">Improved user experience for connecting to Storage with SAS URIs or account keys</span></span>
* <span data-ttu-id="c4296-369">테이블 쿼리 결과를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-369">Export table query results</span></span>
* <span data-ttu-id="c4296-370">테이블 열 다시 정렬 및 사용자 지정이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-370">Table column reordering and customization</span></span>
* <span data-ttu-id="c4296-371">메트릭이 사용하도록 설정된 Storage 계정의 $logs Blob 컨테이너와 $metrics 테이블을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="c4296-372">내보내기 및 가져오기 동작이 개선되어 이제 속성 값 형식이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-373">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-373">Fixes</span></span>

* <span data-ttu-id="c4296-374">수정됨: 큰 Blob를 업로드하거나 다운로드하면 업로드/다운로드가 완전히 진행되지 않는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="c4296-375">수정됨: 숫자 문자열 값("1")이 포함된 엔터티를 편집하거나 추가하거나 가져오면 해당 값이 double로 변환되는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it to double</span></span>
* <span data-ttu-id="c4296-376">수정됨: 로컬 개발 환경에서 테이블 노드를 확장할 수 없는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-376">Fixed: Unable to expand the table node in the local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4296-377">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-377">Known Issues</span></span>

* <span data-ttu-id="c4296-378">$metrics 테이블이 Blob Storage 계정에 대해 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="c4296-379">Base64 인코딩을 사용하여 인코딩된 큐 메시지를 프로그래밍 방식으로 추가하면 올바르게 표시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-379">Queue messages added programmatically may not be displayed correctly if the messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="c4296-380">05/17/2016</span><span class="sxs-lookup"><span data-stu-id="c4296-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="c4296-381">버전 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="c4296-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="c4296-382">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-382">New</span></span>

* <span data-ttu-id="c4296-383">앱 작동 중단 시의 오류가 보다 효율적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-384">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-384">Fixes</span></span>

* <span data-ttu-id="c4296-385">로그인 자격 증명이 필요할 때 정보 표시줄 메시지가 가끔씩 표시되지 않는 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4296-386">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-386">Known Issues</span></span>

* <span data-ttu-id="c4296-387">테이블: "1" 또는 "1.0"과 같이 모호한 숫자 값이 포함된 속성이 있는 엔터티를 추가하거나 편집하거나 가져올 때 사용자가 해당 엔터티를 `Edm.String`으로 보내려고 하면 값이 클라이언트 API를 통해 Edm.Double로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and the user tries to send it as an `Edm.String`, the value will come back through the client API as an Edm.Double</span></span>

<span data-ttu-id="c4296-388">03/31/2016</span><span class="sxs-lookup"><span data-stu-id="c4296-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="c4296-389">버전 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="c4296-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="c4296-390">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-390">New</span></span>

* <span data-ttu-id="c4296-391">테이블 지원: 엔터티 보기/쿼리/내보내기/가져오기 및 CRUD 작업이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="c4296-392">큐 지원: 메시지 보기, 추가, 큐에서 제거가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="c4296-393">Storage 계정에 대해 SAS URI를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="c4296-394">SAS URI를 사용하여 Storage 계정에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-394">Connecting to Storage Accounts with SAS URIs</span></span>
* <span data-ttu-id="c4296-395">이후 Storage 탐색기 업데이트를 위한 업데이트 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-395">Update notifications for future updates to Storage Explorer</span></span>
* <span data-ttu-id="c4296-396">디자인이 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-397">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-397">Fixes</span></span>

* <span data-ttu-id="c4296-398">성능과 안정성이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="c4296-399">알려진 문제 &amp; 완화 방법</span><span class="sxs-lookup"><span data-stu-id="c4296-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="c4296-400">큰 Blob 파일 다운로드가 제대로 작동하지 않습니다. 이 문제를 해결하는 방법이 제공될 때까지는 AzCopy를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="c4296-401">홈 폴더를 찾을 수 없거나 홈 폴더에 쓸 수 없는 경우 계정 자격 증명이 검색되거나 캐시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-401">Account credentials will not be retrieved nor cached if the home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="c4296-402">"1" 또는 "1.0"과 같이 모호한 숫자 값이 포함된 속성이 있는 엔터티를 추가하거나 편집하거나 가져올 때 사용자가 해당 엔터티를 `Edm.String`으로 보내려고 하면 값이 클라이언트 API를 통해 Edm.Double로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and the user tries to send it as an `Edm.String`, the value will come back through the client API as an Edm.Double</span></span>
* <span data-ttu-id="c4296-403">여러 줄 된 레코드가 포함된 CSV 파일을 가져올 때 데이터가 잘리거나 암호화될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-403">When importing CSV files with multiline records, the data may get chopped or scrambled</span></span>

<span data-ttu-id="c4296-404">02/03/2016</span><span class="sxs-lookup"><span data-stu-id="c4296-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="c4296-405">버전 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="c4296-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-406">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-406">Fixes</span></span>

* <span data-ttu-id="c4296-407">Blob 업로드, 다운로드 및 복사 시의 전반적인 성능이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="c4296-408">01/14/2016</span><span class="sxs-lookup"><span data-stu-id="c4296-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="c4296-409">버전 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="c4296-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="c4296-410">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-410">New</span></span>

* <span data-ttu-id="c4296-411">Linux 지원이 추가되었습니다(OSX에 대한 패리티 기능).</span><span class="sxs-lookup"><span data-stu-id="c4296-411">Linux support (parity features to OSX)</span></span>
* <span data-ttu-id="c4296-412">SAS(공유 액세스 서명) 키를 사용하여 Blob 컨테이너를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="c4296-413">Azure 중국의 Storage 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="c4296-414">사용자 지정 끝점이 있는 Storage 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="c4296-415">내용 텍스트 및 그림 blob 열기 및 보기</span><span class="sxs-lookup"><span data-stu-id="c4296-415">Open and view the contents text and picture blobs</span></span>
* <span data-ttu-id="c4296-416">blob 속성 및 메타데이터 보기 및 편집</span><span class="sxs-lookup"><span data-stu-id="c4296-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="c4296-417">수정 프로그램</span><span class="sxs-lookup"><span data-stu-id="c4296-417">Fixes</span></span>

* <span data-ttu-id="c4296-418">수정됨: 500개가 넘는 많은 Blob를 업로드하거나 다운로드할 때 가끔씩 앱에 흰색 화면이 표시될 수 있는 현상이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause the app to have a white screen</span></span> 
* <span data-ttu-id="c4296-419">수정됨: Blob 컨테이너 공용 액세스 수준을 설정할 때 컨테이너에서 포커스를 다시 설정할 때까지 새 값이 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-419">Fixed: when setting blob container public access level, the new value is not updated until you re-set the focus on the container.</span></span> <span data-ttu-id="c4296-420">또한 대화 상자에서는 실제 현재 값이 아닌 "공용 액세스 권한 없음"이 항상 기본값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-420">Also, the dialog always defaults to "No public access", and not the actual current value.</span></span>
* <span data-ttu-id="c4296-421">전반적인 키보드/손쉬운 사용 및 UI 지원이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="c4296-422">이동 경로 기록 텍스트가 길면 공백이 추가되어 줄이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="c4296-423">SAS 대화 상자에서 입력 유효성 검사가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="c4296-424">사용자 자격 증명이 만료되어도 로컬 저장소는 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-424">Local storage continues to be available even if user credentials have expired</span></span>
* <span data-ttu-id="c4296-425">열었던 Blob 컨테이너를 삭제하면 오른쪽의 Blob 탐색기가 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-425">When an opened blob container is deleted, the blob explorer on the right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4296-426">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-426">Known Issues</span></span>

* <span data-ttu-id="c4296-427">Ubuntu 설치 시에는 gcc 버전을 업데이트하거나 업그레이드해야 합니다. 업그레이드 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-427">Linux install needs gcc version updated or upgraded – steps to upgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="c4296-428">11/18/2015</span><span class="sxs-lookup"><span data-stu-id="c4296-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="c4296-429">버전 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="c4296-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="c4296-430">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="c4296-430">New</span></span>

* <span data-ttu-id="c4296-431">macOS 및 Windows 버전이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="c4296-432">조직 계정, Microsoft 계정, 2FA 등을 사용하여 로그인해 Storage 계정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-432">Sign in to view your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="c4296-433">로컬 개발 저장소가 제공됩니다(Storage 에뮬레이터 사용, Windows 전용).</span><span class="sxs-lookup"><span data-stu-id="c4296-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="c4296-434">Azure Resource Manager 및 클래식 리소스가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="c4296-435">Blob, 큐 또는 테이블을 만들고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="c4296-436">특정 Blob, 큐 또는 테이블을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="c4296-437">Blob 컨테이너의 내용을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-437">Explore the contents of blob containers</span></span>
* <span data-ttu-id="c4296-438">디렉터리를 보고 디렉터리 간을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-438">View and navigate through directories</span></span>
* <span data-ttu-id="c4296-439">Blob와 폴더를 업로드, 다운로드 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="c4296-440">blob 속성 및 메타데이터 보기 및 편집</span><span class="sxs-lookup"><span data-stu-id="c4296-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="c4296-441">SAS 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-441">Generate SAS keys</span></span>
* <span data-ttu-id="c4296-442">SAP(저장된 액세스 정책)를 관리하고 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="c4296-443">접두사별로 blob 검색</span><span class="sxs-lookup"><span data-stu-id="c4296-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="c4296-444">파일을 끌어서 놓는 방식으로 업로드하거나 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-444">Drag 'n drop files to upload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c4296-445">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4296-445">Known Issues</span></span>

* <span data-ttu-id="c4296-446">Blob 컨테이너 공용 액세스 수준을 설정할 때 컨테이너에서 포커스를 다시 설정할 때까지 새 값이 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-446">When setting blob container public access level, the new value is not updated until you re-set the focus on the container</span></span>
* <span data-ttu-id="c4296-447">공용 액세스 수준을 설정하기 위해 대화 상자를 열면 실제 현재 값이 아닌 "공용 액세스 권한 없음"이 항상 기본값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-447">When you open the dialog to set the public access level, it always shows "No public access" as the default, and not the actual current value</span></span>
* <span data-ttu-id="c4296-448">다운로드한 Blob 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="c4296-449">오류 발생 시 활동 로그 항목이 가끔씩 진행 중인 상태에서 "중단"되고 오류가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and the error is not displayed</span></span>
* <span data-ttu-id="c4296-450">많은 Blob를 업로드하거나 다운로드하려고 할 때 가끔씩 작동이 중단되거나 완전히 흰색 화면으로 바뀔 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-450">Sometimes crashes or turns completely white when trying to upload or download a large number of blobs</span></span>
* <span data-ttu-id="c4296-451">가끔씩 복사 작업을 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="c4296-452">컨테이너(Blob/테이블/큐)를 만드는 동안 잘못된 이름을 입력하고 다른 컨테이너 형식으로 다른 컨테이너 만들기를 진행하는 경우 새 형식에 포커스를 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-452">During creating a container (blob/queue/table), if you input an invalid name and proceed to create another under a different container type you cannot set focus on the new type</span></span>
* <span data-ttu-id="c4296-453">새 폴더를 만들거나 폴더 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4296-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md