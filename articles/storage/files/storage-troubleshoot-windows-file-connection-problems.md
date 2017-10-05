---
title: "Windows에서 Azure File Storage 문제 해결 | Microsoft Docs"
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
ms.openlocfilehash: daaf7d0589f5e2d82b43dad879bffd23370a2c81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="beeb6-103">Windows에서 Azure File Storage 문제 해결</span><span class="sxs-lookup"><span data-stu-id="beeb6-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="beeb6-104">이 문서에는 Windows 클라이언트에서 연결할 때 Microsoft Azure File Storage에 관련된 일반적인 문제가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="beeb6-105">또한 이러한 문제의 가능한 원인과 해결 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="beeb6-106">이 문서의 문제 해결 단계 외에도 [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5)를 사용하여 Windows 클라이언트 환경의 필수 구성 요소가 올바른지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-106">In addition to the troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that the Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="beeb6-107">AzFileDiagnostics는 이 문서에서 설명하는 대부분의 현상을 자동으로 감지하고 최적의 성능을 얻도록 환경을 설정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-107">AzFileDiagnostics automates detection of most of the symptoms mentioned in this article and helps set up your environment to get optimal performance.</span></span> <span data-ttu-id="beeb6-108">이 정보는 Azure 파일 공유 연결/매핑/탑재 관련 문제에 도움이 되는 단계를 제공하는 [Azure 파일 공유 문제 해결사](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares)에서도 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-108">You can also find this information in the [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps to assist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="beeb6-109">Azure 파일 공유를 탑재 또는 탑재 해제하는 경우 오류 53, 오류 67 또는 오류 87 발생</span><span class="sxs-lookup"><span data-stu-id="beeb6-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="beeb6-110">온-프레미스 또는 다른 데이터 센터에서 파일 공유를 탑재하려고 할 때 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-110">When you try to mount a file share from on-premises or from a different datacenter, you might receive the following errors:</span></span>

- <span data-ttu-id="beeb6-111">시스템 오류 53이 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-111">System error 53 has occurred.</span></span> <span data-ttu-id="beeb6-112">네트워크 경로를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-112">The network path was not found.</span></span>
- <span data-ttu-id="beeb6-113">시스템 오류 67이 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-113">System error 67 has occurred.</span></span> <span data-ttu-id="beeb6-114">네트워크 이름을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-114">The network name cannot be found.</span></span>
- <span data-ttu-id="beeb6-115">시스템 오류 87이 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-115">System error 87 has occurred.</span></span> <span data-ttu-id="beeb6-116">매개 변수가 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-116">The parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="beeb6-117">원인 1: 암호화되지 않은 통신 채널</span><span class="sxs-lookup"><span data-stu-id="beeb6-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="beeb6-118">보안상 이유로, 통신 채널이 암호화되지 않고 Azure 파일 공유가 있는 같은 데이터 센터에서 연결 시도가 이루어지지 않을 경우 Azure 파일 공유에 대한 연결이 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-118">For security reasons, connections to Azure file shares are blocked if the communication channel isn’t encrypted and if the connection attempt isn't made from the same datacenter where the Azure file shares reside.</span></span> <span data-ttu-id="beeb6-119">사용자의 클라이언트 OS가 SMB 암호화를 지원하는 경우에만 통신 채널 암호화가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-119">Communication channel encryption is provided only if the user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="beeb6-120">각 시스템의 Windows 8, Windows Server 2012 이후 버전은 암호화를 지원하는 SMB 3.0이 포함된 요청을 협상합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="beeb6-121">원인 1의 해결 방법</span><span class="sxs-lookup"><span data-stu-id="beeb6-121">Solution for cause 1</span></span>

<span data-ttu-id="beeb6-122">다음 중 하나를 수행하는 클라이언트에서 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-122">Connect from a client that does one of the following:</span></span>

- <span data-ttu-id="beeb6-123">Windows 8 및 Windows Server 2012 이후 버전의 요구 사항을 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-123">Meets the requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="beeb6-124">Azure 파일 공유에 사용되는 Azure Storage 계정과 동일한 데이터 센터의 가상 컴퓨터에서 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-124">Connects from a virtual machine in the same datacenter as the Azure storage account that is used for the Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="beeb6-125">원인 2: 포트 445 차단</span><span class="sxs-lookup"><span data-stu-id="beeb6-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="beeb6-126">시스템 오류 53 또는 시스템 오류 67은 Azure File 데이터 센터에 대한 포트 445 아웃바운드 통신이 차단될 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-126">System error 53 or system error 67 can occur if port 445 outbound communication to an Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="beeb6-127">포트 445에서 시작되는 액세스를 허용하거나 거부하는 ISP에 대한 요약을 확인하려면 [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-127">To see the summary of ISPs that allow or disallow access from port 445, go to [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="beeb6-128">이 이유로 "시스템 오류 53" 메시지가 수신되었는지 이해하려면 Portqry를 사용하여 TCP:445 끝점을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-128">To understand whether this is the reason behind the "System error 53" message, you can use Portqry to query the TCP:445 endpoint.</span></span> <span data-ttu-id="beeb6-129">TCP:445 끝점이 필터링됨으로 표시될 경우 TCP 포트가 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-129">If the TCP:445 endpoint is displayed as filtered, the TCP port is blocked.</span></span> <span data-ttu-id="beeb6-130">다음은 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="beeb6-131">TCP 포트 445가 네트워크 경로를 따라 규칙을 통해 차단될 경우 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-131">If TCP port 445 is blocked by a rule along the network path, you will see the following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="beeb6-132">Portqry 사용 방법에 대한 자세한 내용은 [Portqry.exe 명령줄 유틸리티에 대한 설명](https://support.microsoft.com/help/310099)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="beeb6-132">For more information about how to use Portqry, see [Description of the Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="beeb6-133">원인 2의 해결 방법</span><span class="sxs-lookup"><span data-stu-id="beeb6-133">Solution for cause 2</span></span>

<span data-ttu-id="beeb6-134">IT 부서와 협력하여 [Azure IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)에 대한 포트 445 아웃바운드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-134">Work with your IT department to open port 445 outbound to [Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="beeb6-135">원인 3: NTLMv1 사용</span><span class="sxs-lookup"><span data-stu-id="beeb6-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="beeb6-136">클라이언트에서 NTLMv1 통신이 사용될 경우 시스템 오류 53 또는 시스템 오류 87이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on the client.</span></span> <span data-ttu-id="beeb6-137">Azure File Storage는 NTLMv2 인증만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="beeb6-138">NTLMv1을 사용하도록 설정하면 클라이언트 보안이 약화됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="beeb6-139">따라서 Azure File Storage에 대한 통신이 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="beeb6-140">이것이 오류의 원인인지 확인하려면 다음 레지스트리 하위 키가 3의 값으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-140">To determine whether this is the cause of the error, verify that the following registry subkey is set to a value of 3:</span></span>

<span data-ttu-id="beeb6-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="beeb6-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="beeb6-142">자세한 내용은 TechNet에서 [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="beeb6-142">For more information, see the [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="beeb6-143">원인 3의 해결 방법</span><span class="sxs-lookup"><span data-stu-id="beeb6-143">Solution for cause 3</span></span>

<span data-ttu-id="beeb6-144">**LmCompatibilityLevel** 값을 다음 레지스트리 하위 키의 기본값인 3으로 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-144">Revert the **LmCompatibilityLevel** value to the default value of 3 in the following registry subkey:</span></span>

  <span data-ttu-id="beeb6-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="beeb6-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-to-process-this-command-when-you-copy-to-an-azure-file-share"></a><span data-ttu-id="beeb6-146">Azure 파일 공유에 복사하는 경우 오류 1816 "이 명령을 처리할 수 있는 할당량이 충분하지 않습니다." 발생</span><span class="sxs-lookup"><span data-stu-id="beeb6-146">Error 1816 “Not enough quota is available to process this command” when you copy to an Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="beeb6-147">원인</span><span class="sxs-lookup"><span data-stu-id="beeb6-147">Cause</span></span>

<span data-ttu-id="beeb6-148">파일 공유가 탑재되어 있는 컴퓨터의 파일에 허용되는 동시 오픈 핸들의 상한값에 도달하는 경우 오류 1816이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-148">Error 1816 happens when you reach the upper limit of concurrent open handles that are allowed for a file on the computer where the file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="beeb6-149">해결 방법</span><span class="sxs-lookup"><span data-stu-id="beeb6-149">Solution</span></span>

<span data-ttu-id="beeb6-150">일부 핸들을 닫아 동시 열린 핸들 수를 줄이고 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="beeb6-150">Reduce the number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="beeb6-151">자세한 내용은 [Microsoft Azure Storage 성능 및 확장성 검사 목록](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="beeb6-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-windows"></a><span data-ttu-id="beeb6-152">Windows에서 Azure File Storage 간에 느린 파일 복사</span><span class="sxs-lookup"><span data-stu-id="beeb6-152">Slow file copying to and from Azure File storage in Windows</span></span>

<span data-ttu-id="beeb6-153">Azure File 서비스에 파일을 전송하려고 하면 성능 저하가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-153">You might see slow performance when you try to transfer files to the Azure File service.</span></span>

- <span data-ttu-id="beeb6-154">최소 I/O 크기에 대한 특정 요구 사항이 없을 경우 최적 성능을 위해 I/O 크기로 1MB를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="beeb6-155">쓰기를 사용하여 확장 중인 파일의 최종 크기를 알고 파일에 아직 기록되지 않은 꼬리에 0이 포함될 때 소프트웨어에 호환성 문제가 발생하지 않는다면 모든 쓰기를 확장 쓰기로 설정하는 대신 파일 크기를 미리 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-155">If you know the final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when the unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="beeb6-156">copy 메서드를 다음과 같이 올바르게 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-156">Use the right copy method:</span></span>
    -   <span data-ttu-id="beeb6-157">두 파일 공유 간의 전송에는 [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-157">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="beeb6-158">온-프레미스 컴퓨터와 파일 공유 간에는 [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="beeb6-159">Windows 8.1 또는 Windows Server 2012 R2에 대한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="beeb6-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="beeb6-160">Windows 8.1 또는 Windows Server 2012 R2를 실행 중인 클라이언트에서는 핫픽스 [KB3114025](https://support.microsoft.com/help/3114025)가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that the [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="beeb6-161">이 핫픽스는 핸들 만들기 및 닫기 성능을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-161">This hotfix improves the performance of create and close handles.</span></span>

<span data-ttu-id="beeb6-162">다음 스크립트를 실행하여 핫픽스가 설치되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-162">You can run the following script to check whether the hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="beeb6-163">핫픽스가 설치된 경우 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-163">If hotfix is installed, the following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="beeb6-164">2015년 12월부터 Azure Marketplace의 Windows Server 2012 R2 이미지에는 핫픽스 KB3114025가 기본적으로 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="beeb6-165">**내 컴퓨터**에 드라이브 문자를 포함한 폴더가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="beeb6-166">net use를 사용하여 관리자 권한으로 Azure 파일 공유를 매핑하는 경우 공유가 누락될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-166">If you map an Azure file share as an administrator by using net use, the share appears to be missing.</span></span>

### <a name="cause"></a><span data-ttu-id="beeb6-167">원인</span><span class="sxs-lookup"><span data-stu-id="beeb6-167">Cause</span></span>

<span data-ttu-id="beeb6-168">기본적으로 Windows File Explorer는 관리자 권한으로 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="beeb6-169">관리자 명령 프롬프트에서 net use를 실행할 경우 네트워크 드라이브를 관리자 권한으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-169">If you run net use from an administrative command prompt, you map the network drive as an administrator.</span></span> <span data-ttu-id="beeb6-170">매핑된 드라이브는 사용자 중심이므로 다른 사용자 계정으로 탑재될 경우 로그인된 사용자 계정에 드라이브가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-170">Because mapped drives are user-centric, the user account that is logged in does not display the drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="beeb6-171">해결 방법</span><span class="sxs-lookup"><span data-stu-id="beeb6-171">Solution</span></span>
<span data-ttu-id="beeb6-172">비관리자 명령줄에서 공유를 탑재하세요.</span><span class="sxs-lookup"><span data-stu-id="beeb6-172">Mount the share from a non-administrator command line.</span></span> <span data-ttu-id="beeb6-173">또는 [이 TechNet 항목](https://technet.microsoft.com/library/ee844140.aspx)에 따라 **EnableLinkedConnections** 레지스트리 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) to configure the **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-the-storage-account-contains-a-forward-slash"></a><span data-ttu-id="beeb6-174">내 저장소 계정에 슬래시(/)가 포함되는 경우 net use 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-174">Net use command fails if the storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="beeb6-175">원인</span><span class="sxs-lookup"><span data-stu-id="beeb6-175">Cause</span></span>

<span data-ttu-id="beeb6-176">net use 명령은 슬래시(/)를 명령줄 옵션으로 해석합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-176">The net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="beeb6-177">사용자 계정 이름이 슬래시로 시작되면 드라이브 매핑에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-177">If your user account name starts with a forward slash, the drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="beeb6-178">해결 방법</span><span class="sxs-lookup"><span data-stu-id="beeb6-178">Solution</span></span>

<span data-ttu-id="beeb6-179">다음 단계 중 하나를 사용하여 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-179">You can use either of the following steps to work around the problem:</span></span>

- <span data-ttu-id="beeb6-180">다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-180">Run the following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="beeb6-181">배치 파일에서 다음과 같은 방식으로 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-181">From a batch file, you can run the command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="beeb6-182">슬래시(/)가 첫 번째 문자가 아닐 경우 키 주위에 큰따옴표를 배치하여 이 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-182">Put double quotation marks around the key to work around this problem--unless the forward slash is the first character.</span></span> <span data-ttu-id="beeb6-183">슬래시(/)가 첫 번째 문자일 경우 대화형 모드를 사용하여 암호를 개별적으로 입력하거나 키를 다시 생성하여 슬래시(/) 문자로 시작되지 않는 키를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-183">If it is, either use the interactive mode and enter your password separately or regenerate your keys to get a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="beeb6-184">응용 프로그램 또는 서비스가 탑재된 Azure File Storage 드라이브에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="beeb6-185">원인</span><span class="sxs-lookup"><span data-stu-id="beeb6-185">Cause</span></span>

<span data-ttu-id="beeb6-186">드라이브는 사용자별로 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-186">Drives are mounted per user.</span></span> <span data-ttu-id="beeb6-187">응용 프로그램 또는 서비스가 드라이브를 탑재한 계정이 아닌 다른 사용자 계정으로 실행되는 경우 응용 프로그램에는 드라이브가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-187">If your application or service is running under a different user account than the one that mounted the drive, the application will not see the drive.</span></span>

### <a name="solution"></a><span data-ttu-id="beeb6-188">해결 방법</span><span class="sxs-lookup"><span data-stu-id="beeb6-188">Solution</span></span>

<span data-ttu-id="beeb6-189">다음 해결 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-189">Use one of the following solutions:</span></span>

-   <span data-ttu-id="beeb6-190">응용 프로그램을 포함하는 동일한 사용자 계정에서 드라이브를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-190">Mount the drive from the same user account that contains the application.</span></span> <span data-ttu-id="beeb6-191">PsExec와 같은 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="beeb6-192">net use 명령의 사용자 이름 및 암호 매개 변수에 저장소 계정 이름 및 키를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-192">Pass the storage account name and key in the user name and password parameters of the net use command.</span></span>

<span data-ttu-id="beeb6-193">다음과 같은 지침을 따르고 시스템/네트워크 서비스 계정에 net use를 실행하면 다음과 같은 오류 메시지가 표시될 수 있습니다. "시스템 오류 1312가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-193">After you follow these instructions, you might receive the following error message when you run net use for the system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="beeb6-194">지정된 로그온 세션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-194">A specified logon session does not exist.</span></span> <span data-ttu-id="beeb6-195">이미 종료되었을 수 있습니다."</span><span class="sxs-lookup"><span data-stu-id="beeb6-195">It may already have been terminated."</span></span> <span data-ttu-id="beeb6-196">이 문제가 발생하면 net use에 전달되는 사용자 이름에 도메인 정보(예: "[저장소 계정 이름].file.core.windows.net")가 포함되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-196">If this occurs, make sure that the username that is passed to net use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-to-a-destination-that-does-not-support-encryption"></a><span data-ttu-id="beeb6-197">“암호화를 지원하지 않는 대상에 파일을 복사하는 중임” 오류 발생</span><span class="sxs-lookup"><span data-stu-id="beeb6-197">Error "You are copying a file to a destination that does not support encryption"</span></span>

<span data-ttu-id="beeb6-198">네트워크를 통해 파일이 복사되면 파일은 원본 컴퓨터에서 암호를 해독하고, 일반 텍스트로 전송되어 대상에서 다시 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-198">When a file is copied over the network, the file is decrypted on the source computer, transmitted in plaintext, and re-encrypted at the destination.</span></span> <span data-ttu-id="beeb6-199">하지만 암호화된 파일을 복사하려 하는 경우 다음 오류가 발생할 수 있습니다. "암호화를 지원하지 않는 대상에 파일을 복사하고 있습니다."</span><span class="sxs-lookup"><span data-stu-id="beeb6-199">However, you might see the following error when you're trying to copy an encrypted file: "You are copying the file to a destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="beeb6-200">원인</span><span class="sxs-lookup"><span data-stu-id="beeb6-200">Cause</span></span>
<span data-ttu-id="beeb6-201">EFS(파일 시스템 암호화)를 사용하는 경우 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="beeb6-202">Bitlocker로 암호화된 파일을 Azure File Storage로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-202">BitLocker-encrypted files can be copied to Azure File storage.</span></span> <span data-ttu-id="beeb6-203">하지만 Azure File Storage는 NTFS EFS를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="beeb6-204">해결 방법</span><span class="sxs-lookup"><span data-stu-id="beeb6-204">Workaround</span></span>
<span data-ttu-id="beeb6-205">파일을 네트워크로 복사하려면 먼저 파일을 암호 해독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-205">To copy a file over the network, you must first decrypt it.</span></span> <span data-ttu-id="beeb6-206">다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-206">Use one of the following methods:</span></span>

- <span data-ttu-id="beeb6-207">**copy /d** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-207">Use the **copy /d** command.</span></span> <span data-ttu-id="beeb6-208">암호화된 파일을 대상에서 암호 해독된 파일로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-208">It allows the encrypted files to be saved as decrypted files at the destination.</span></span>
- <span data-ttu-id="beeb6-209">다음 레지스트리 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-209">Set the following registry key:</span></span>
  - <span data-ttu-id="beeb6-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="beeb6-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="beeb6-211">Value type = DWORD</span><span class="sxs-lookup"><span data-stu-id="beeb6-211">Value type = DWORD</span></span>
  - <span data-ttu-id="beeb6-212">Name = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="beeb6-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="beeb6-213">Value = 1</span><span class="sxs-lookup"><span data-stu-id="beeb6-213">Value = 1</span></span>

<span data-ttu-id="beeb6-214">레지스트리 키를 설정하면 네트워크 공유에 만들어진 모든 복사 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="beeb6-214">Be aware that setting the registry key affects all copy operations that are made to network shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="beeb6-215">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="beeb6-215">Need help?</span></span> <span data-ttu-id="beeb6-216">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="beeb6-216">Contact support.</span></span>
<span data-ttu-id="beeb6-217">도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="beeb6-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
