---
title: " Azure Site Recovery에서 확장 프로세스 서버 관리 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery에서 확장 프로세스 서버를 설정하고 관리하는 방법을 설명합니다."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: e5c01de19917235c34c035415df86291b9152bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="3f2f3-103">확장 프로세스 서버 관리</span><span class="sxs-lookup"><span data-stu-id="3f2f3-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="3f2f3-104">확장 프로세스 서버는 Site Recovery 서비스와 온-프레미스 인프라 간의 데이터 전송에 대한 코디네이터로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-104">Scale-out Process Server acts as a coordinator for data transfer between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="3f2f3-105">이 문서에서는 확장 프로세스 서버를 설정, 구성 및 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f2f3-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3f2f3-106">Prerequisites</span></span>
<span data-ttu-id="3f2f3-107">다음은 확장 프로세스 서버를 설정하는 데 필요한 권장되는 하드웨어, 소프트웨어 및 네트워크 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-107">The following are the recommended hardware, software, and network configuration required to set up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="3f2f3-108">[용량 계획](site-recovery-capacity-planner.md)은 로드 요구 사항에 맞는 구성으로 확장 프로세스 서버를 배포하는지 확인하는 중요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="3f2f3-109">[확장 프로세스 서버에 대한 특성 크기 조정](#sizing-requirements-for-a-configuration-server)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-scale-out-process-server-software"></a><span data-ttu-id="3f2f3-110">확장 프로세스 서버 소프트웨어 다운로드</span><span class="sxs-lookup"><span data-stu-id="3f2f3-110">Downloading the Scale-out Process Server software</span></span>
1. <span data-ttu-id="3f2f3-111">Azure Portal에 로그온하고 Recovery Services 자격 증명 모음으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="3f2f3-112">**Site Recovery 인프라** > **구성 서버**(VMware 및 물리적 컴퓨터용 아래)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="3f2f3-113">구성 서버를 선택하여 구성 서버의 세부 정보 페이지로 드릴다운합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-113">Select your configuration server to drill down into the configuration server's details page.</span></span>
4. <span data-ttu-id="3f2f3-114">**+ 프로세스 서버** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-114">Click the **+ Process Server** button.</span></span>
5. <span data-ttu-id="3f2f3-115">**프로세스 서버 추가** 페이지의 **프로세스 서버를 배포할 위치 선택** 드롭다운에서 **온-프레미스로 확장 프로세스 서버 배포** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-115">In the **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from the **Choose where you want to deploy your process server** drop-down.</span></span>

  ![서버 페이지 추가](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="3f2f3-117">**Microsoft Azure Site Recovery 통합 설치 다운로드** 링크를 클릭하여 확장 프로세스 서버 설치의 최신 버전을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="3f2f3-118">확장 프로세서 서버의 버전은 사용자 환경에서 실행 중인 구성 서버 버전과 동일하거나 낮아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-118">The version of your Scale-out Process Server should be equal to or lesser than the Configuration Server version running in your environment.</span></span> <span data-ttu-id="3f2f3-119">버전 호환성을 보장하는 간단한 방법은 구성 서버를 설치/업데이트하는 데 최근에 사용한 동일한 설치 관리자 비트를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-119">A simple way to ensure version compatibility is to use the same installer bits that you recently used to install/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="3f2f3-120">GUI에서 확장 프로세스 서버 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="3f2f3-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="3f2f3-121">200대가 넘는 원본 컴퓨터로 배포 규모를 확장해야 하고 총 이탈률이 2TB를 초과하는 경우 트래픽 볼륨을 처리할 추가 프로세스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-121">If you have to scale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers to handle the traffic volume.</span></span>

<span data-ttu-id="3f2f3-122">[프로세스 서버에 대한 크기 권장 사항](#size-recommendations-for-the-process-server)을 확인한 후 다음 지침에 따라 프로세스 서버를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-122">Check the [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions to set up the process server.</span></span> <span data-ttu-id="3f2f3-123">서버를 설정한 후 이를 사용하도록 원본 컴퓨터를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-123">After setting up the server, you migrate source machines to use it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="3f2f3-124">명령줄을 사용하여 확장 프로세스 서버 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="3f2f3-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="3f2f3-125">샘플 사용</span><span class="sxs-lookup"><span data-stu-id="3f2f3-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="3f2f3-126">확장 프로세스 서버 설치 관리자 명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="3f2f3-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="3f2f3-127">프록시 설정 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="3f2f3-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="3f2f3-128">ProxySettingsFilePath 매개 변수는 입력으로 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="3f2f3-129">다음 형식을 사용하여 파일을 만들고 입력 ProxySettingsFilePath 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-129">Create file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="3f2f3-130">확장 프로세스 서버에 대한 프록시 설정 수정</span><span class="sxs-lookup"><span data-stu-id="3f2f3-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="3f2f3-131">확장 프로세스 서버에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="3f2f3-132">관리자 PowerShell 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="3f2f3-133">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-133">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="3f2f3-134">그런 다음 디렉터리 **%PROGRAMDATA%\ASR\Agent**로 이동하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-134">Next browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="3f2f3-135">확장 프로세스 서버 다시 등록</span><span class="sxs-lookup"><span data-stu-id="3f2f3-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="3f2f3-136">그런 다음 관리자 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="3f2f3-137">**%PROGRAMDATA%\ASR\Agent** 디렉터리로 이동하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-137">Browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="3f2f3-138">확장 프로세스 서버 업그레이드</span><span class="sxs-lookup"><span data-stu-id="3f2f3-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="3f2f3-139">확장 프로세스 서버 서비스 해제</span><span class="sxs-lookup"><span data-stu-id="3f2f3-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="3f2f3-140">다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-140">Ensure that:</span></span>
  - <span data-ttu-id="3f2f3-141">Azure Portal에서 구성 서버의 연결 상태가 **Connected**로 표시됨</span><span class="sxs-lookup"><span data-stu-id="3f2f3-141">Configuration Server's connection state shows as **Connected** in the Azure portal</span></span>
  - <span data-ttu-id="3f2f3-142">프로세스 서버는 여전히 구성 서버와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-142">Process Server's is still able to communicate with the Configuration server.</span></span>
2. <span data-ttu-id="3f2f3-143">관리자 권한으로 프로세스 서버에 로그인</span><span class="sxs-lookup"><span data-stu-id="3f2f3-143">Log in to the process server as an administrator</span></span>
3. <span data-ttu-id="3f2f3-144">제어판 > 프로그램 > 프로그램 제거 열기</span><span class="sxs-lookup"><span data-stu-id="3f2f3-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="3f2f3-145">다음 순서로 프로그램을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-145">Uninstall the programs in the sequence given following:</span></span>
  * <span data-ttu-id="3f2f3-146">Microsoft Azure Site Recovery 구성 서버/프로세스 서버</span><span class="sxs-lookup"><span data-stu-id="3f2f3-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="3f2f3-147">Microsoft Azure Site Recovery 구성 서버 종속성</span><span class="sxs-lookup"><span data-stu-id="3f2f3-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="3f2f3-148">Microsoft Azure Recovery Services 에이전트</span><span class="sxs-lookup"><span data-stu-id="3f2f3-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="3f2f3-149">프로세스 서버 삭제가 Azure Portal에 반영되는 데 최대 15분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-149">It can take up-to 15 minutes for the Process Server deletion to reflect in the Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="3f2f3-150">프로세스 서버가 구성 서버와 통신할 수 없는 경우(포털의 연결 상태가 Disconnected) 다음 단계를 따라 구성 서버에서 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-150">If the Process server is unable to communicate with the Configuration Server (Connection State in portal is Disconnected), then you need to follow the following steps to purge it from the Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="3f2f3-151">구성 서버에서 연결이 끊긴 확장 프로세스 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="3f2f3-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="3f2f3-152">확장 프로세스 서버에 대한 크기 조정 요구 사항</span><span class="sxs-lookup"><span data-stu-id="3f2f3-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="3f2f3-153">**추가 프로세스 서버**</span><span class="sxs-lookup"><span data-stu-id="3f2f3-153">**Additional process server**</span></span> | <span data-ttu-id="3f2f3-154">**캐시 디스크 크기**</span><span class="sxs-lookup"><span data-stu-id="3f2f3-154">**Cache disk size**</span></span> | <span data-ttu-id="3f2f3-155">**데이터 변경률**</span><span class="sxs-lookup"><span data-stu-id="3f2f3-155">**Data change rate**</span></span> | <span data-ttu-id="3f2f3-156">**보호된 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="3f2f3-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="3f2f3-157">4개 vCPU(2개 소켓 * 2코어 @ 2.5GHz), 8GB 메모리</span><span class="sxs-lookup"><span data-stu-id="3f2f3-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="3f2f3-158">300GB</span><span class="sxs-lookup"><span data-stu-id="3f2f3-158">300 GB</span></span> |<span data-ttu-id="3f2f3-159">250GB 이하</span><span class="sxs-lookup"><span data-stu-id="3f2f3-159">250 GB or less</span></span> |<span data-ttu-id="3f2f3-160">85대 이하의 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="3f2f3-161">8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 12GB 메모리</span><span class="sxs-lookup"><span data-stu-id="3f2f3-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="3f2f3-162">600GB</span><span class="sxs-lookup"><span data-stu-id="3f2f3-162">600 GB</span></span> |<span data-ttu-id="3f2f3-163">250GB ~ 1TB</span><span class="sxs-lookup"><span data-stu-id="3f2f3-163">250 GB to 1 TB</span></span> |<span data-ttu-id="3f2f3-164">85-150대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="3f2f3-165">12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz), 24GB 메모리</span><span class="sxs-lookup"><span data-stu-id="3f2f3-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="3f2f3-166">1TB</span><span class="sxs-lookup"><span data-stu-id="3f2f3-166">1 TB</span></span> |<span data-ttu-id="3f2f3-167">1TB ~ 2TB</span><span class="sxs-lookup"><span data-stu-id="3f2f3-167">1 TB to 2 TB</span></span> |<span data-ttu-id="3f2f3-168">150-225대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2f3-168">Replicate between 150-225 machines.</span></span> |
