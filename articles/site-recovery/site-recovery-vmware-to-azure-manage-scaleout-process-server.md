---
title: " Azure Site Recovery에서 확장 프로세스 서버 관리 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooset 및 Azure 사이트 복구에서 확장 프로세스 서버를 관리 합니다."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="82fe5-103">확장 프로세스 서버 관리</span><span class="sxs-lookup"><span data-stu-id="82fe5-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="82fe5-104">확장 프로세스 서버 hello Site Recovery 서비스와 온-프레미스 인프라 간의 데이터 전송을 위해 코디네이터로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-104">Scale-out Process Server acts as a coordinator for data transfer between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="82fe5-105">이 문서에서는 확장 프로세스 서버를 설정, 구성 및 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82fe5-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="82fe5-106">Prerequisites</span></span>
<span data-ttu-id="82fe5-107">hello 하드웨어, 소프트웨어 및 네트워크 구성이 필요 tooset 확장 프로세스 서버를 권장 하는 hello 다음과가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-107">hello following are hello recommended hardware, software, and network configuration required tooset up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="82fe5-108">[용량 계획](site-recovery-capacity-planner.md) 배포 하는 hello 확장 프로세스 서버와 구성 도구 모음의 해당 하는 중요 한 단계 tooensure는 로드 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="82fe5-109">[확장 프로세스 서버에 대한 특성 크기 조정](#sizing-requirements-for-a-configuration-server)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a><span data-ttu-id="82fe5-110">Hello 확장 프로세스 서버 소프트웨어를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-110">Downloading hello Scale-out Process Server software</span></span>
1. <span data-ttu-id="82fe5-111">Azure 포털 및 찾아보기 tooyour 복구 서비스 자격 증명 모음 toohello에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="82fe5-112">너무 찾아보기**사이트 복구 인프라** > **구성 서버** (아래에 대 한 VMware & 물리적 컴퓨터의 경우).</span><span class="sxs-lookup"><span data-stu-id="82fe5-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="82fe5-113">아래로 hello 구성 서버 세부 정보 페이지에 구성 서버 toodrill를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-113">Select your configuration server toodrill down into hello configuration server's details page.</span></span>
4. <span data-ttu-id="82fe5-114">Hello 클릭 **+ 프로세스 서버** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-114">Click hello **+ Process Server** button.</span></span>
5. <span data-ttu-id="82fe5-115">Hello에 **추가 프로세스 서버** 페이지에서 **프로세스 서버를 확장 배포 온-프레미스** hello에서 옵션 **저장할 toodeploy 프로세스 서버 선택** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-115">In hello **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from hello **Choose where you want toodeploy your process server** drop-down.</span></span>

  ![서버 페이지 추가](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="82fe5-117">Hello 클릭 **다운로드 hello Microsoft Azure Site Recovery 통합 설치** 링크 toodownload hello hello 확장 프로세스 서버 설치의 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="82fe5-118">hello 확장 프로세스 서버 버전이 같아야 tooor 사용자 환경에서 실행 하는 hello 구성 서버 버전 보다 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-118">hello version of your Scale-out Process Server should be equal tooor lesser than hello Configuration Server version running in your environment.</span></span> <span data-ttu-id="82fe5-119">간단한 방법을 tooensure 버전 호환성은 toouse 최근에 사용 하 여 tooinstall/업데이트 구성 서버에 동일한 설치 관리자 비트 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-119">A simple way tooensure version compatibility is toouse hello same installer bits that you recently used tooinstall/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="82fe5-120">GUI에서 확장 프로세스 서버 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="82fe5-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="82fe5-121">원본 컴퓨터를 200 개 초과 배포 아웃 tooscale 했거나 총 매일 변동 비율로 2 테라바이트 이상 경우 추가 프로세스 서버 toohandle hello 트래픽 볼륨을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-121">If you have tooscale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers toohandle hello traffic volume.</span></span>

<span data-ttu-id="82fe5-122">Hello 확인 [크기 프로세스 서버에 대 한 권장 사항](#size-recommendations-for-the-process-server), 한 다음 이러한 지침 tooset hello 프로세스 서버를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-122">Check hello [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions tooset up hello process server.</span></span> <span data-ttu-id="82fe5-123">마이그레이션한 원본 컴퓨터 toouse hello 서버를 설정한 후 것입니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-123">After setting up hello server, you migrate source machines toouse it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="82fe5-124">명령줄을 사용하여 확장 프로세스 서버 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="82fe5-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="82fe5-125">샘플 사용</span><span class="sxs-lookup"><span data-stu-id="82fe5-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="82fe5-126">확장 프로세스 서버 설치 관리자 명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="82fe5-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="82fe5-127">프록시 설정 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="82fe5-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="82fe5-128">ProxySettingsFilePath 매개 변수는 입력으로 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="82fe5-129">다음 서식을 지정 하 고 입력된 ProxySettingsFilePath 매개 변수로 전달 하는 hello를 사용 하 여 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-129">Create file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="82fe5-130">확장 프로세스 서버에 대한 프록시 설정 수정</span><span class="sxs-lookup"><span data-stu-id="82fe5-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="82fe5-131">확장 프로세스 서버에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="82fe5-132">관리자 PowerShell 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="82fe5-133">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-133">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="82fe5-134">그런 다음 toohello 디렉터리 찾아보기 **%PROGRAMDATA%\ASR\Agent** 다음 명령이 실행된 하는 hello 및</span><span class="sxs-lookup"><span data-stu-id="82fe5-134">Next browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="82fe5-135">확장 프로세스 서버 다시 등록</span><span class="sxs-lookup"><span data-stu-id="82fe5-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="82fe5-136">그런 다음 관리자 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="82fe5-137">Toohello 디렉터리 찾아보기 **%PROGRAMDATA%\ASR\Agent** hello 명령을 실행 하 고</span><span class="sxs-lookup"><span data-stu-id="82fe5-137">Browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="82fe5-138">확장 프로세스 서버 업그레이드</span><span class="sxs-lookup"><span data-stu-id="82fe5-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="82fe5-139">확장 프로세스 서버 서비스 해제</span><span class="sxs-lookup"><span data-stu-id="82fe5-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="82fe5-140">다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-140">Ensure that:</span></span>
  - <span data-ttu-id="82fe5-141">구성 서버의 연결 상태 표시 **연결 됨** hello Azure 포털에서</span><span class="sxs-lookup"><span data-stu-id="82fe5-141">Configuration Server's connection state shows as **Connected** in hello Azure portal</span></span>
  - <span data-ttu-id="82fe5-142">프로세스 서버 hello 구성 서버와 여전히 수 toocommunicate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-142">Process Server's is still able toocommunicate with hello Configuration server.</span></span>
2. <span data-ttu-id="82fe5-143">관리자 권한으로 toohello 프로세스 서버에 로그인</span><span class="sxs-lookup"><span data-stu-id="82fe5-143">Log in toohello process server as an administrator</span></span>
3. <span data-ttu-id="82fe5-144">제어판 > 프로그램 > 프로그램 제거 열기</span><span class="sxs-lookup"><span data-stu-id="82fe5-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="82fe5-145">Hello 시퀀스 지정 된 다음에 hello 프로그램을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-145">Uninstall hello programs in hello sequence given following:</span></span>
  * <span data-ttu-id="82fe5-146">Microsoft Azure Site Recovery 구성 서버/프로세스 서버</span><span class="sxs-lookup"><span data-stu-id="82fe5-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="82fe5-147">Microsoft Azure Site Recovery 구성 서버 종속성</span><span class="sxs-lookup"><span data-stu-id="82fe5-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="82fe5-148">Microsoft Azure Recovery Services 에이전트</span><span class="sxs-lookup"><span data-stu-id="82fe5-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="82fe5-149">Hello Azure 포털에서에서 hello 프로세스 서버 삭제 tooreflect 위쪽 too15 분 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-149">It can take up-too15 minutes for hello Process Server deletion tooreflect in hello Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="82fe5-150">Hello 프로세스 서버가 구성 서버 hello로 없습니다 toocommunicate 인지 (포털에 대 한 연결 상태가 Disconnected)를 toofollow 필요 hello 단계 toopurge 다음 그 hello 구성 서버에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-150">If hello Process server is unable toocommunicate with hello Configuration Server (Connection State in portal is Disconnected), then you need toofollow hello following steps toopurge it from hello Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="82fe5-151">구성 서버에서 연결이 끊긴 확장 프로세스 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="82fe5-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="82fe5-152">확장 프로세스 서버에 대한 크기 조정 요구 사항</span><span class="sxs-lookup"><span data-stu-id="82fe5-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="82fe5-153">**추가 프로세스 서버**</span><span class="sxs-lookup"><span data-stu-id="82fe5-153">**Additional process server**</span></span> | <span data-ttu-id="82fe5-154">**캐시 디스크 크기**</span><span class="sxs-lookup"><span data-stu-id="82fe5-154">**Cache disk size**</span></span> | <span data-ttu-id="82fe5-155">**데이터 변경률**</span><span class="sxs-lookup"><span data-stu-id="82fe5-155">**Data change rate**</span></span> | <span data-ttu-id="82fe5-156">**보호된 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="82fe5-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="82fe5-157">4개 vCPU(2개 소켓 * 2코어 @ 2.5GHz), 8GB 메모리</span><span class="sxs-lookup"><span data-stu-id="82fe5-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="82fe5-158">300GB</span><span class="sxs-lookup"><span data-stu-id="82fe5-158">300 GB</span></span> |<span data-ttu-id="82fe5-159">250GB 이하</span><span class="sxs-lookup"><span data-stu-id="82fe5-159">250 GB or less</span></span> |<span data-ttu-id="82fe5-160">85대 이하의 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="82fe5-161">8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 12GB 메모리</span><span class="sxs-lookup"><span data-stu-id="82fe5-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="82fe5-162">600GB</span><span class="sxs-lookup"><span data-stu-id="82fe5-162">600 GB</span></span> |<span data-ttu-id="82fe5-163">250GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="82fe5-163">250 GB too1 TB</span></span> |<span data-ttu-id="82fe5-164">85-150대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="82fe5-165">12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz), 24GB 메모리</span><span class="sxs-lookup"><span data-stu-id="82fe5-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="82fe5-166">1TB</span><span class="sxs-lookup"><span data-stu-id="82fe5-166">1 TB</span></span> |<span data-ttu-id="82fe5-167">1TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="82fe5-167">1 TB too2 TB</span></span> |<span data-ttu-id="82fe5-168">150-225대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="82fe5-168">Replicate between 150-225 machines.</span></span> |
