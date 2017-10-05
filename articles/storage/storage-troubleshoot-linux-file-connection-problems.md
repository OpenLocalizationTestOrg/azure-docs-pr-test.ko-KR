---
title: "Linux에서 Azure File Storage 문제 해결 | Microsoft Docs"
description: "Linux에서 Azure File Storage 문제 해결"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 62cd62ec3a2900f06acacc0852a48b5e3ff1c8cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="4cf36-103">Linux에서 Azure File Storage 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4cf36-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="4cf36-104">이 문서에는 Linux 클라이언트에서 연결할 때 Microsoft Azure File Storage에 관련된 일반적인 문제 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="4cf36-105">또한 이러한 문제의 가능한 원인과 해결 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-to-open-a-file"></a><span data-ttu-id="4cf36-106">파일을 열려고 할 때 “[사용 권한 거부됨] 디스크 할당량이 초과됨”</span><span class="sxs-lookup"><span data-stu-id="4cf36-106">"[permission denied] Disk quota exceeded" when you try to open a file</span></span>

<span data-ttu-id="4cf36-107">Linux에서는 다음과 같은 오류 메시지가 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-107">In Linux, you receive an error message that resembles the following:</span></span>

<span data-ttu-id="4cf36-108">**<filename> [사용 권한 거부됨] 디스크 할당량이 초과됨**</span><span class="sxs-lookup"><span data-stu-id="4cf36-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="4cf36-109">원인</span><span class="sxs-lookup"><span data-stu-id="4cf36-109">Cause</span></span>

<span data-ttu-id="4cf36-110">파일에 허용되는 동시 열린 핸들의 상한에 도달했습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-110">You have reached the upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf36-111">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf36-111">Solution</span></span>

<span data-ttu-id="4cf36-112">일부 핸들을 닫아 동시 열린 핸들 수를 줄인 후 작업을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="4cf36-112">Reduce the number of concurrent open handles by closing some handles, and then retry the operation.</span></span> <span data-ttu-id="4cf36-113">자세한 내용은 [Microsoft Azure Storage 성능 및 확장성 검사 목록](storage-performance-checklist.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4cf36-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-linux"></a><span data-ttu-id="4cf36-114">Linux에서 Azure File Storage 간에 느린 파일 복사</span><span class="sxs-lookup"><span data-stu-id="4cf36-114">Slow file copying to and from Azure File storage in Linux</span></span>

-   <span data-ttu-id="4cf36-115">최소 I/O 크기에 대한 특정 요구 사항이 없을 경우 최적 성능을 위해 I/O 크기로 1MB를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="4cf36-116">쓰기를 사용하여 확장 중인 파일의 최종 크기를 알고 파일에 아직 기록되지 않은 꼬리에 0이 포함될 때 소프트웨어에 호환성 문제가 없다면 모든 쓰기를 확장 쓰기로 설정하는 대신 파일 크기를 미리 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-116">If you know the final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="4cf36-117">copy 메서드를 다음과 같이 올바르게 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-117">Use the right copy method:</span></span>
    -   <span data-ttu-id="4cf36-118">두 파일 공유 간의 전송에는 [AzCopy](storage-use-azcopy.md#file-copy)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-118">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="4cf36-119">온-프레미스 컴퓨터와 파일 공유 간에는 [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="4cf36-120">다시 연결 시간 제한으로 인한 "탑재 오류(112): 호스트가 중단됨"</span><span class="sxs-lookup"><span data-stu-id="4cf36-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="4cf36-121">Linux 클라이언트에서 클라이언트가 장시간 유휴 상태일 경우 "112" 탑재 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-121">A "112" mount error occurs on the Linux client when the client has been idle for a long time.</span></span> <span data-ttu-id="4cf36-122">오랫동안 유휴 상태일 경우 클라이언트 연결이 끊어지고 연결 시간이 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-122">After extended idle time, the client disconnects and the connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="4cf36-123">원인</span><span class="sxs-lookup"><span data-stu-id="4cf36-123">Cause</span></span>

<span data-ttu-id="4cf36-124">다음과 같은 이유로 연결이 유휴 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-124">The connection can be idle for the following reasons:</span></span>

-   <span data-ttu-id="4cf36-125">기본 “소프트” 탑재 옵션을 사용하는 경우 서버에 TCP 연결을 다시 설정하지 않는 네트워크 통신 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-125">Network communication failures that prevent re-establishing a TCP connection to the server when the default “soft” mount option is used</span></span>
-   <span data-ttu-id="4cf36-126">이전 커널에 존재하지 않는 최근 재연결 수정</span><span class="sxs-lookup"><span data-stu-id="4cf36-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="4cf36-127">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf36-127">Solution</span></span>

<span data-ttu-id="4cf36-128">Linux 커널의 이러한 재연결 문제는 현재 다음 변경의 일부로 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-128">This reconnection problem in the Linux kernel is now fixed as part of the following changes:</span></span>

- [<span data-ttu-id="4cf36-129">소켓 재연결 후에 오랫동안 smb3 세션 재연결이 지연되지 않도록 재연결 수정</span><span class="sxs-lookup"><span data-stu-id="4cf36-129">Fix reconnect to not defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="4cf36-130">소켓 재연결 직후 에코 서비스 호출</span><span class="sxs-lookup"><span data-stu-id="4cf36-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="4cf36-131">CIFS: 재연결 동안 가능한 메모리 손상 수정</span><span class="sxs-lookup"><span data-stu-id="4cf36-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [<span data-ttu-id="4cf36-132">CIFS: 재연결 동안 가능한 뮤텍스 이중 잠금 해결(커널 v4.9 이상)</span><span class="sxs-lookup"><span data-stu-id="4cf36-132">CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

<span data-ttu-id="4cf36-133">그러나 이 변경 내용이 모든 Linux 배포판에 아직 이식되지 않은 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-133">However, these changes might not be ported yet to all the Linux distributions.</span></span> <span data-ttu-id="4cf36-134">이 수정 및 기타 재연결 수정은 다음 널리 사용되는 Linux 커널 4.4.40, 4.8.16 및 4.9.1에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-134">This fix and other reconnection fixes are made in the following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="4cf36-135">이러한 권장된 커널 버전 중 하나로 업그레이드하여 이 수정을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-135">You can get this fix by upgrading to one of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="4cf36-136">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf36-136">Workaround</span></span>

<span data-ttu-id="4cf36-137">하드 탑재를 지정하여 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="4cf36-138">클라이언트는 연결될 때까지 또는 명시적으로 중단될 때까지 대기하게 되어 네트워크 시간 제한으로 인해 오류가 발생하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-138">This forces the client to wait until a connection is established or until it’s explicitly interrupted and can be used to prevent errors because of network time-outs.</span></span> <span data-ttu-id="4cf36-139">그러나 이 해결 방법은 무한 대기를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="4cf36-140">필요에 따라 연결을 중지할 준비가 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-140">Be prepared to stop connections as necessary.</span></span>

<span data-ttu-id="4cf36-141">최신 커널 버전으로 업그레이드할 수 없는 경우 30초보다 짧은 간격으로 쓰는 Azure 파일 공유에 파일을 보관하여 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-141">If you cannot upgrade to the latest kernel versions, you can work around this problem by keeping a file in the Azure file share that you write to every 30 seconds or less.</span></span> <span data-ttu-id="4cf36-142">이 작업은 만든 또는 수정된 날짜를 파일에 다시 쓰는 등의 쓰기 작업이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-142">This must be a write operation, such as rewriting the created or modified date on the file.</span></span> <span data-ttu-id="4cf36-143">그렇지 않으면 캐시된 결과를 얻을 수 있고 작업이 재연결을 트리거하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-143">Otherwise, you might get cached results, and your operation might not trigger the reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="4cf36-144">SMB 3.0을 사용하여 Azure File Storage를 탑재할 때 "탑재 오류(115): 현재 작업 진행 중"</span><span class="sxs-lookup"><span data-stu-id="4cf36-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="4cf36-145">원인</span><span class="sxs-lookup"><span data-stu-id="4cf36-145">Cause</span></span>

<span data-ttu-id="4cf36-146">일부 Linux 배포에서는 SMB 3.0의 암호화 기능이 아직 지원되지 않으므로 사용자가 SMB 3.0을 사용하여 Azure File Storage를 탑재하려고 하면 기능 누락으로 인해 “115” 오류 메시지를 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try to mount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf36-147">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf36-147">Solution</span></span>

<span data-ttu-id="4cf36-148">Linux용 SMB 3.0에 대한 암호화 기능이 4.11 커널에 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="4cf36-149">이 기능을 사용하면 온-프레미스 또는 다른 Azure 지역에서 Azure 파일 공유를 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="4cf36-150">게시 당시, 이 기능은 Ubuntu 17.04 및 Ubuntu 16.10으로 백포팅되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-150">At the time of publishing, this functionality has been backported to Ubuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="4cf36-151">Linux SMB 클라이언트가 암호화를 지원하지 않을 경우 File Storage 계정과 같은 데이터 센터의 Azure Linux VM에서 SMB 2.1을 사용하여 Azure File Storage를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in the same datacenter as the File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="4cf36-152">Linux VM에 탑재된 Azure 파일 공유의 성능 저하</span><span class="sxs-lookup"><span data-stu-id="4cf36-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="4cf36-153">원인</span><span class="sxs-lookup"><span data-stu-id="4cf36-153">Cause</span></span>

<span data-ttu-id="4cf36-154">성능 저하의 한 가지 가능한 원인은 캐싱 비활성화입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf36-155">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf36-155">Solution</span></span>

<span data-ttu-id="4cf36-156">캐싱의 비활성화 여부를 확인하려면 **cache=** 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-156">To check whether caching is disabled, look for the **cache=** entry.</span></span> 

<span data-ttu-id="4cf36-157">**cache=none**은 캐싱이 비활성화되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="4cf36-158">기본 캐싱이나 “엄격한” 캐싱 모드를 활성화하는 명령을 탑재하기 위해 기본 탑재 명령을 사용하거나 명시적으로 **cache=strict** 옵션을 추가하여 공유를 다시 탑재하세요.</span><span class="sxs-lookup"><span data-stu-id="4cf36-158">Remount the share by using the default mount command or by explicitly adding the **cache=strict** option to the mount command to ensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="4cf36-159">일부 시나리오에서는 **serverino** 탑재 옵션으로 **ls** 명령을 유도하여 모든 디렉터리 항목에 대해 stat를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-159">In some scenarios, the **serverino** mount option can cause the **ls** command to run stat against every directory entry.</span></span> <span data-ttu-id="4cf36-160">이러한 동작은 큰 디렉터리를 나열하는 경우 성능 저하를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="4cf36-161">**/etc/fstab** 항목에서 탑재 옵션을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-161">You can check the mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="4cf36-162">**sudo mount | grep cifs** 명령을 실행하고 다음 출력 예와 같은 해당 출력을 확인하여 올바른 옵션이 사용되는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-162">You can also check whether the correct options are being used by running the  **sudo mount | grep cifs** command and checking its output, such as the following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="4cf36-163">**cache=strict** 또는 **serverino** 옵션이 없는 경우 [설명서](storage-how-to-use-files-linux.md)의 mount 명령을 실행하여 은 Azure File Storage를 분리했다가 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-163">If the **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running the mount command from the [documentation](storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="4cf36-164">그런 다음 **/etc/fstab** 항목에 올바른 옵션이 있는지 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-164">Then, recheck that the **/etc/fstab** entry has the correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-to-linux"></a><span data-ttu-id="4cf36-165">Windows에서 Linux로 파일을 복사할 때 타임 스탬프 손실됨</span><span class="sxs-lookup"><span data-stu-id="4cf36-165">Time stamps were lost in copying files from Windows to Linux</span></span>

<span data-ttu-id="4cf36-166">Linux/Unix 플랫폼에서 파일 1 및 파일 2의 소유자가 다른 경우 **cp-p** 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-166">On Linux/Unix platforms, the **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="4cf36-167">원인</span><span class="sxs-lookup"><span data-stu-id="4cf36-167">Cause</span></span>

<span data-ttu-id="4cf36-168">COPYFILE에서 force 플래그 **f**로 인해 Unix에서 **cp -p -f**가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-168">The force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="4cf36-169">이 명령은 또한 소유하지 않은 파일의 타임 스탬프를 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-169">This command also fails to preserve the time stamp of the file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="4cf36-170">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4cf36-170">Workaround</span></span>

<span data-ttu-id="4cf36-171">파일 복사를 위해 저장소 계정 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf36-171">Use the storage account user for copying the files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="4cf36-172">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="4cf36-172">Need help?</span></span> <span data-ttu-id="4cf36-173">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="4cf36-173">Contact support.</span></span>

<span data-ttu-id="4cf36-174">도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="4cf36-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
