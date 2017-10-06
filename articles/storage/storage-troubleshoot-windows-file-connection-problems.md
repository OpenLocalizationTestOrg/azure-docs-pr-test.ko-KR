---
title: "Windows에서 Azure 파일 저장소 문제 aaaTroubleshoot | Microsoft Docs"
description: "Windows에서 Azure File Storage 문제 해결"
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
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: ba0315d1add76a27fec93a9aee3aa99ccb7fa164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="915e1-103">Windows에서 Azure File Storage 문제 해결</span><span class="sxs-lookup"><span data-stu-id="915e1-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="915e1-104">이 문서에서는 Windows 클라이언트에서 연결할 때 Azure 파일 저장소 tooMicrosoft를 관련된 된 일반적인 문제를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="915e1-105">또한 이러한 문제의 가능한 원인과 해결 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="915e1-106">또한이 문서의 단계 toohello 문제 해결을 사용할 수도 있습니다 [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) 클라이언트 환경에 올바른 필수 구성 요소는 해당 hello Windows 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-106">In addition toohello troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that hello Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="915e1-107">AzFileDiagnostics이이 문서에 언급 된 hello 증상 및 쉽게 환경 tooget 최적의 성능을 설정할 수 있는 대부분의 검색을 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-107">AzFileDiagnostics automates detection of most of hello symptoms mentioned in this article and helps set up your environment tooget optimal performance.</span></span> <span data-ttu-id="915e1-108">Hello에이 정보를 찾을 수도 [문제 해결사를 공유 하는 Azure 파일](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) tooassist 단계를 제공 하는 연결/매핑/탑재 Azure 파일 공유 하는 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-108">You can also find this information in hello [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps tooassist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="915e1-109">Azure 파일 공유를 탑재 또는 탑재 해제하는 경우 오류 53, 오류 67 또는 오류 87 발생</span><span class="sxs-lookup"><span data-stu-id="915e1-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="915e1-110">온-프레미스 또는 다른 데이터 센터에서 파일 공유 toomount을 시도할 때 다음 오류 hello를 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-110">When you try toomount a file share from on-premises or from a different datacenter, you might receive hello following errors:</span></span>

- <span data-ttu-id="915e1-111">시스템 오류 53이 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-111">System error 53 has occurred.</span></span> <span data-ttu-id="915e1-112">hello 네트워크 경로 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-112">hello network path was not found.</span></span>
- <span data-ttu-id="915e1-113">시스템 오류 67이 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-113">System error 67 has occurred.</span></span> <span data-ttu-id="915e1-114">hello 네트워크 이름을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-114">hello network name cannot be found.</span></span>
- <span data-ttu-id="915e1-115">시스템 오류 87이 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-115">System error 87 has occurred.</span></span> <span data-ttu-id="915e1-116">hello 매개 변수가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-116">hello parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="915e1-117">원인 1: 암호화되지 않은 통신 채널</span><span class="sxs-lookup"><span data-stu-id="915e1-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="915e1-118">보안상의 이유로 연결 hello 통신 채널 암호화 되지 않습니다 및 hello 연결 시도에서 수행 되지 않습니다 tooAzure 파일 공유는 차단 hello hello Azure 파일 공유 상주 하는 동일한 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-118">For security reasons, connections tooAzure file shares are blocked if hello communication channel isn’t encrypted and if hello connection attempt isn't made from hello same datacenter where hello Azure file shares reside.</span></span> <span data-ttu-id="915e1-119">통신 채널 암호화 hello 사용자의 클라이언트 운영 체제에서 SMB 암호화를 지원할 경우에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-119">Communication channel encryption is provided only if hello user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="915e1-120">각 시스템의 Windows 8, Windows Server 2012 이후 버전은 암호화를 지원하는 SMB 3.0이 포함된 요청을 협상합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="915e1-121">원인 1의 해결 방법</span><span class="sxs-lookup"><span data-stu-id="915e1-121">Solution for cause 1</span></span>

<span data-ttu-id="915e1-122">Hello 다음 중 하나를 수행 하는 클라이언트에서 연결:</span><span class="sxs-lookup"><span data-stu-id="915e1-122">Connect from a client that does one of hello following:</span></span>

- <span data-ttu-id="915e1-123">Windows 8 및 Windows Server 2012 또는 이후 버전의 hello 요구 사항을 충족</span><span class="sxs-lookup"><span data-stu-id="915e1-123">Meets hello requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="915e1-124">Hello에 가상 컴퓨터에서 동일한 연결 hello hello Azure 파일 공유에 사용 되는 Azure 저장소 계정으로 데이터 센터</span><span class="sxs-lookup"><span data-stu-id="915e1-124">Connects from a virtual machine in hello same datacenter as hello Azure storage account that is used for hello Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="915e1-125">원인 2: 포트 445 차단</span><span class="sxs-lookup"><span data-stu-id="915e1-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="915e1-126">시스템 오류 53 또는 시스템 오류 67 포트 445 아웃 바운드 통신 tooan Azure 파일 저장소 datacenter 차단 된 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-126">System error 53 or system error 67 can occur if port 445 outbound communication tooan Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="915e1-127">포트 445에서에서 액세스를 허용 하거나 거부 하는 Isp의 toosee hello 요약 너무 이동[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-127">toosee hello summary of ISPs that allow or disallow access from port 445, go too[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="915e1-128">toounderstand hello 이유가 hello "시스템 오류 53" 메시지 인지 Portqry tooquery hello TCP:445 끝점을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-128">toounderstand whether this is hello reason behind hello "System error 53" message, you can use Portqry tooquery hello TCP:445 endpoint.</span></span> <span data-ttu-id="915e1-129">Hello TCP:445 끝점 필터링으로 표시 되 면 hello TCP 포트는 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-129">If hello TCP:445 endpoint is displayed as filtered, hello TCP port is blocked.</span></span> <span data-ttu-id="915e1-130">다음은 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="915e1-131">TCP 포트 445 hello 네트워크 경로 따라 규칙에 의해 차단 되 면 hello 출력을 따라 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-131">If TCP port 445 is blocked by a rule along hello network path, you will see hello following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="915e1-132">방법에 대 한 자세한 내용은 toouse Portqry, 참조 [hello Portqry.exe 명령줄 유틸리티의 설명](https://support.microsoft.com/help/310099)합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-132">For more information about how toouse Portqry, see [Description of hello Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="915e1-133">원인 2의 해결 방법</span><span class="sxs-lookup"><span data-stu-id="915e1-133">Solution for cause 2</span></span>

<span data-ttu-id="915e1-134">IT 부서 tooopen 포트 445 아웃 바운드 너무 작업할[Azure IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-134">Work with your IT department tooopen port 445 outbound too[Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="915e1-135">원인 3: NTLMv1 사용</span><span class="sxs-lookup"><span data-stu-id="915e1-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="915e1-136">시스템 오류 53 또는 시스템 오류 87 NTLMv1 통신 hello 클라이언트에 설정 된 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on hello client.</span></span> <span data-ttu-id="915e1-137">Azure File Storage는 NTLMv2 인증만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="915e1-138">NTLMv1을 사용하도록 설정하면 클라이언트 보안이 약화됩니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="915e1-139">따라서 Azure File Storage에 대한 통신이 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="915e1-140">toodetermine는 hello 오류 hello 원인 인지 여부를는 다음 레지스트리 하위 키 해당 hello tooa 값 3으로 설정 되어 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-140">toodetermine whether this is hello cause of hello error, verify that hello following registry subkey is set tooa value of 3:</span></span>

<span data-ttu-id="915e1-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="915e1-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="915e1-142">자세한 내용은 참조 hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) technet 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-142">For more information, see hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="915e1-143">원인 3의 해결 방법</span><span class="sxs-lookup"><span data-stu-id="915e1-143">Solution for cause 3</span></span>

<span data-ttu-id="915e1-144">Hello 되돌리기 **LmCompatibilityLevel** hello 레지스트리 하위 키 다음의 3 기본값인 toohello 값:</span><span class="sxs-lookup"><span data-stu-id="915e1-144">Revert hello **LmCompatibilityLevel** value toohello default value of 3 in hello following registry subkey:</span></span>

  <span data-ttu-id="915e1-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="915e1-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a><span data-ttu-id="915e1-146">오류 1816 "할당량이 충분 하지 않습니다는 사용할 수 있는 tooprocess이이 명령은" tooan Azure 파일 공유를 복사 하는 경우</span><span class="sxs-lookup"><span data-stu-id="915e1-146">Error 1816 “Not enough quota is available tooprocess this command” when you copy tooan Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="915e1-147">원인</span><span class="sxs-lookup"><span data-stu-id="915e1-147">Cause</span></span>

<span data-ttu-id="915e1-148">오류 1816 hello hello 파일 공유는 탑재 된 hello 컴퓨터에 있는 파일에 허용 되는 동시 열린 핸들의 상한에 도달 하면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-148">Error 1816 happens when you reach hello upper limit of concurrent open handles that are allowed for a file on hello computer where hello file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="915e1-149">해결 방법</span><span class="sxs-lookup"><span data-stu-id="915e1-149">Solution</span></span>

<span data-ttu-id="915e1-150">일부 핸들을 닫아 hello 동시 열려 있는 핸들 수를 줄인 후 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="915e1-150">Reduce hello number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="915e1-151">자세한 내용은 [Microsoft Azure Storage 성능 및 확장성 검사 목록](storage-performance-checklist.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="915e1-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a><span data-ttu-id="915e1-152">Windows에서 Azure 파일 저장소에서 tooand를 복사 하는 느린 파일</span><span class="sxs-lookup"><span data-stu-id="915e1-152">Slow file copying tooand from Azure File storage in Windows</span></span>

<span data-ttu-id="915e1-153">Tootransfer 파일 toohello Azure 파일 서비스를 시도 하면 성능 저하를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-153">You might see slow performance when you try tootransfer files toohello Azure File service.</span></span>

- <span data-ttu-id="915e1-154">특정 최소 I/O 크기 요구 사항이 없다면 최적의 성능을 위해 I/O 크기 hello으로 1MB를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="915e1-155">알고 있는 경우 확장 하는 파일의 최종 크기 hello 쓰고 hello hello 파일에 기록 되지 않은 꼬리 포함 되어 있으면 0으로 다음 집합 hello 파일 크기 확장 쓰기 각 쓰기를 수행 하는 대신 미리 소프트웨어 호환성 문제가 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-155">If you know hello final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when hello unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="915e1-156">Hello 오른쪽 복사 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-156">Use hello right copy method:</span></span>
    -   <span data-ttu-id="915e1-157">두 파일 공유 간의 전송에는 [AzCopy](storage-use-azcopy.md#file-copy)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="915e1-158">온-프레미스 컴퓨터와 파일 공유 간에는 [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="915e1-159">Windows 8.1 또는 Windows Server 2012 R2에 대한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="915e1-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="915e1-160">Windows 8.1 또는 Windows Server 2012 r 2를 실행 하는 클라이언트 해야 해당 hello [KB3114025](https://support.microsoft.com/help/3114025) 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that hello [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="915e1-161">이 핫픽스 create hello 성능을 향상 시키고 핸들을 닫아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-161">This hotfix improves hello performance of create and close handles.</span></span>

<span data-ttu-id="915e1-162">Hello 핫픽스가 설치 되어 있는지 여부를 스크립트 toocheck 다음 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-162">You can run hello following script toocheck whether hello hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="915e1-163">핫픽스를 설치 하는 경우 hello 다음과 같은 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-163">If hotfix is installed, hello following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="915e1-164">2015년 12월부터 Azure Marketplace의 Windows Server 2012 R2 이미지에는 핫픽스 KB3114025가 기본적으로 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="915e1-165">**내 컴퓨터**에 드라이브 문자를 포함한 폴더가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="915e1-166">Hello 공유 toobe 나타납니다 넷 사용을 사용 하 여 관리자 권한으로 Azure 파일 공유를 매핑하는 경우 없습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-166">If you map an Azure file share as an administrator by using net use, hello share appears toobe missing.</span></span>

### <a name="cause"></a><span data-ttu-id="915e1-167">원인</span><span class="sxs-lookup"><span data-stu-id="915e1-167">Cause</span></span>

<span data-ttu-id="915e1-168">기본적으로 Windows File Explorer는 관리자 권한으로 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="915e1-169">관리 명령 프롬프트에서 net 사용 하 여를 실행 하는 경우에 관리자 권한으로 hello 네트워크 드라이브를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-169">If you run net use from an administrative command prompt, you map hello network drive as an administrator.</span></span> <span data-ttu-id="915e1-170">매핑된 드라이브는 사용자 중심 이므로 다른 사용자 계정으로 탑재 된 경우 hello 사용자 계정에 기록 된 hello 드라이브가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-170">Because mapped drives are user-centric, hello user account that is logged in does not display hello drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="915e1-171">해결 방법</span><span class="sxs-lookup"><span data-stu-id="915e1-171">Solution</span></span>
<span data-ttu-id="915e1-172">관리자가 아닌 명령줄에서 hello 공유를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-172">Mount hello share from a non-administrator command line.</span></span> <span data-ttu-id="915e1-173">따를 수 있습니다 [이 TechNet 항목](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** 레지스트리 값입니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a><span data-ttu-id="915e1-174">Hello 저장소 계정에 슬래시를 포함 하는 경우 net use 명령 실패</span><span class="sxs-lookup"><span data-stu-id="915e1-174">Net use command fails if hello storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="915e1-175">원인</span><span class="sxs-lookup"><span data-stu-id="915e1-175">Cause</span></span>

<span data-ttu-id="915e1-176">명령줄 옵션으로 슬래시 (/)를 해석 하는 hello net use 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-176">hello net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="915e1-177">사용자 계정 이름은 슬래시로 시작 되 면 hello 드라이브 매핑이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-177">If your user account name starts with a forward slash, hello drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="915e1-178">해결 방법</span><span class="sxs-lookup"><span data-stu-id="915e1-178">Solution</span></span>

<span data-ttu-id="915e1-179">Hello hello 문제에 대 한 단계 toowork 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-179">You can use either of hello following steps toowork around hello problem:</span></span>

- <span data-ttu-id="915e1-180">Hello 다음 PowerShell 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-180">Run hello following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="915e1-181">배치 파일에서 hello 명령 이러한 방식으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-181">From a batch file, you can run hello command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="915e1-182">Hello 슬래시가 hello 첫 번째 문자가 아닌 경우이 문제에 대-hello 키 toowork 큰따옴표로 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-182">Put double quotation marks around hello key toowork around this problem--unless hello forward slash is hello first character.</span></span> <span data-ttu-id="915e1-183">인 경우 hello 대화형 모드를 사용 하 여 및 암호를 별도로 입력 또는 사용자 키 tooget 슬래시 문자로 시작 하지 않습니다는 키를 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-183">If it is, either use hello interactive mode and enter your password separately or regenerate your keys tooget a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="915e1-184">응용 프로그램 또는 서비스가 탑재된 Azure File Storage 드라이브에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="915e1-185">원인</span><span class="sxs-lookup"><span data-stu-id="915e1-185">Cause</span></span>

<span data-ttu-id="915e1-186">드라이브는 사용자별로 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-186">Drives are mounted per user.</span></span> <span data-ttu-id="915e1-187">응용 프로그램 또는 서비스 hello hello 드라이브를 마운트 하는 것 보다 다른 사용자 계정으로 실행 hello 드라이브 hello 응용 프로그램에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-187">If your application or service is running under a different user account than hello one that mounted hello drive, hello application will not see hello drive.</span></span>

### <a name="solution"></a><span data-ttu-id="915e1-188">해결 방법</span><span class="sxs-lookup"><span data-stu-id="915e1-188">Solution</span></span>

<span data-ttu-id="915e1-189">Hello 솔루션을 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-189">Use one of hello following solutions:</span></span>

-   <span data-ttu-id="915e1-190">Hello에서 hello 드라이브 탑재 hello 응용 프로그램을 포함 하는 동일한 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-190">Mount hello drive from hello same user account that contains hello application.</span></span> <span data-ttu-id="915e1-191">PsExec와 같은 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="915e1-192">Hello 저장소 계정 이름과 키 hello net use 명령의 hello 사용자 이름 및 암호 매개 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-192">Pass hello storage account name and key in hello user name and password parameters of hello net use command.</span></span>

<span data-ttu-id="915e1-193">다음이 지침을 따를 후 hello hello 시스템/네트워크 서비스 계정에 대 한 넷 사용을 실행 하면 다음과 같은 오류 메시지가 표시 될 수 있습니다: "시스템 오류 1312 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-193">After you follow these instructions, you might receive hello following error message when you run net use for hello system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="915e1-194">지정된 로그온 세션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-194">A specified logon session does not exist.</span></span> <span data-ttu-id="915e1-195">이미 종료되었을 수 있습니다."</span><span class="sxs-lookup"><span data-stu-id="915e1-195">It may already have been terminated."</span></span> <span data-ttu-id="915e1-196">이 경우 해당 hello 사용자 이름을 사용 하 여 toonet 전달 되는 도메인 정보가 포함 되어 있는지 확인 (예: "[저장소 계정 이름]. file.core.windows.net").</span><span class="sxs-lookup"><span data-stu-id="915e1-196">If this occurs, make sure that hello username that is passed toonet use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a><span data-ttu-id="915e1-197">오류 "복사 하는 암호화를 지원 하지 않는 파일 tooa 대상을"</span><span class="sxs-lookup"><span data-stu-id="915e1-197">Error "You are copying a file tooa destination that does not support encryption"</span></span>

<span data-ttu-id="915e1-198">Hello 네트워크를 통해 파일이 복사 되 면 hello 파일에서 해독 된 hello 원본 컴퓨터를 일반 텍스트로 전송 되 고 hello 대상에 다시 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-198">When a file is copied over hello network, hello file is decrypted on hello source computer, transmitted in plaintext, and re-encrypted at hello destination.</span></span> <span data-ttu-id="915e1-199">그러나 hello toocopy 암호화 된 파일을 만들려고 하는 경우 다음 오류가 표시 될 수 있습니다: "hello 파일 tooa 대상 암호화를 지원 하지 않는 복사 됩니다."</span><span class="sxs-lookup"><span data-stu-id="915e1-199">However, you might see hello following error when you're trying toocopy an encrypted file: "You are copying hello file tooa destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="915e1-200">원인</span><span class="sxs-lookup"><span data-stu-id="915e1-200">Cause</span></span>
<span data-ttu-id="915e1-201">EFS(파일 시스템 암호화)를 사용하는 경우 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="915e1-202">BitLocker로 암호화 된 파일 복사 tooAzure 파일 저장소를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-202">BitLocker-encrypted files can be copied tooAzure File storage.</span></span> <span data-ttu-id="915e1-203">하지만 Azure File Storage는 NTFS EFS를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="915e1-204">해결 방법</span><span class="sxs-lookup"><span data-stu-id="915e1-204">Workaround</span></span>
<span data-ttu-id="915e1-205">hello 네트워크를 통해 파일 toocopy 하면 먼저 암호를 해독 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-205">toocopy a file over hello network, you must first decrypt it.</span></span> <span data-ttu-id="915e1-206">Hello 메서드를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-206">Use one of hello following methods:</span></span>

- <span data-ttu-id="915e1-207">사용 하 여 hello **/d 복사** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-207">Use hello **copy /d** command.</span></span> <span data-ttu-id="915e1-208">Hello 암호화를 통해 파일 toobe hello 대상에서 해독 된 파일으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-208">It allows hello encrypted files toobe saved as decrypted files at hello destination.</span></span>
- <span data-ttu-id="915e1-209">Hello 다음 레지스트리 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-209">Set hello following registry key:</span></span>
  - <span data-ttu-id="915e1-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="915e1-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="915e1-211">Value type = DWORD</span><span class="sxs-lookup"><span data-stu-id="915e1-211">Value type = DWORD</span></span>
  - <span data-ttu-id="915e1-212">Name = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="915e1-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="915e1-213">Value = 1</span><span class="sxs-lookup"><span data-stu-id="915e1-213">Value = 1</span></span>

<span data-ttu-id="915e1-214">주의 설정을 hello 레지스트리 키를 toonetwork 공유 적용 된 모든 복사 작업에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-214">Be aware that setting hello registry key affects all copy operations that are made toonetwork shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="915e1-215">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="915e1-215">Need help?</span></span> <span data-ttu-id="915e1-216">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="915e1-216">Contact support.</span></span>
<span data-ttu-id="915e1-217">도움이 필요 하면 여전히 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="915e1-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
