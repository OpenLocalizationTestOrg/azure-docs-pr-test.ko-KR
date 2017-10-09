---
title: " Azure Site Recovery에서 구성 서버 관리 | Microsoft Doc"
description: "이 문서에서는 설명 방법을 tooset 하 고 구성 서버를 관리 합니다."
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="0c6e3-103">구성 서버 관리</span><span class="sxs-lookup"><span data-stu-id="0c6e3-103">Manage a Configuration Server</span></span>

<span data-ttu-id="0c6e3-104">구성 서버 hello Site Recovery 서비스와 온-프레미스 인프라 간의 코디네이터로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-104">Configuration Server acts as a coordinator between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="0c6e3-105">이 문서에서는 설정, 구성 하는 방법 관리 hello 구성 서버를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-105">This article describes how you can set up, configure, and manage hello Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c6e3-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0c6e3-106">Prerequisites</span></span>
<span data-ttu-id="0c6e3-107">hello 다음 hello 최소 하드웨어, 소프트웨어 및 구성 서버를 네트워크 구성이 필요 tooset은입니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-107">hello following are hello minimum hardware, software, and network configuration required tooset up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="0c6e3-108">[용량 계획](site-recovery-capacity-planner.md) 를 배포 하는 구성 사용 하 여 구성 서버 hello 해당 도구 모음 하는 중요 한 단계 tooensure는 로드 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="0c6e3-109">[구성 서버에 대한 크기 조정 요구 사항](#sizing-requirements-for-a-configuration-server)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a><span data-ttu-id="0c6e3-110">Hello 구성 서버 소프트웨어를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-110">Downloading hello Configuration Server software</span></span>
1. <span data-ttu-id="0c6e3-111">Azure 포털 및 찾아보기 tooyour 복구 서비스 자격 증명 모음 toohello에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="0c6e3-112">너무 찾아보기**사이트 복구 인프라** > **구성 서버** (아래에 대 한 VMware & 물리적 컴퓨터의 경우).</span><span class="sxs-lookup"><span data-stu-id="0c6e3-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![서버 페이지 추가](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="0c6e3-114">Hello 클릭 **+ 서버** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-114">Click hello **+Servers** button.</span></span>
4. <span data-ttu-id="0c6e3-115">Hello에 **서버 추가** 페이지 hello 다운로드 단추 toodownload hello 등록 키를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-115">On hello **Add Server** page, click hello Download button toodownload hello Registration key.</span></span> <span data-ttu-id="0c6e3-116">Hello 구성 서버 설치 tooregister 하는 동안이 키가 필요 하면 Azure Site Recovery 서비스와 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-116">You need this key during hello Configuration Server installation tooregister it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="0c6e3-117">Hello 클릭 **다운로드 hello Microsoft Azure Site Recovery 통합 설치** 링크 toodownload hello 최신 버전의 구성 서버 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Configuration Server.</span></span>

  ![다운로드 페이지](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="0c6e3-119">최신 버전의 hello 구성 서버에서 직접 다운로드할 수 있습니다 [Microsoft 다운로드 센터 다운로드 페이지](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="0c6e3-119">Latest version of hello Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="0c6e3-120">GUI에서 구성 서버 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="0c6e3-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="0c6e3-121">명령줄에서 구성 서버 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="0c6e3-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="0c6e3-122">샘플 사용</span><span class="sxs-lookup"><span data-stu-id="0c6e3-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="0c6e3-123">구성 서버 설치 관리자 명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="0c6e3-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="0c6e3-124">MySql 자격 증명 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="0c6e3-124">Create a MySql credentials file</span></span>
<span data-ttu-id="0c6e3-125">MySQLCredsFilePath 매개 변수는 입력으로 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="0c6e3-126">다음 서식을 지정 하 고 입력된 MySQLCredsFilePath 매개 변수로 전달 하는 hello를 사용 하 여 hello 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-126">Create hello file using hello following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="0c6e3-127">프록시 설정 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="0c6e3-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="0c6e3-128">ProxySettingsFilePath 매개 변수는 입력으로 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="0c6e3-129">다음 서식을 지정 하 고 입력된 ProxySettingsFilePath 매개 변수로 전달 하는 hello를 사용 하 여 hello 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-129">Create hello file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="0c6e3-130">구성 서버의 프록시 설정 수정</span><span class="sxs-lookup"><span data-stu-id="0c6e3-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="0c6e3-131">로그인 tooyour 구성 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-131">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="0c6e3-132">바로 가기 hello를 사용 하 여 hello cspsconfigtool.exe를 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-132">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
3. <span data-ttu-id="0c6e3-133">Hello 클릭 **자격 증명 모음 등록** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-133">Click hello **Vault Registration** tab.</span></span>
4. <span data-ttu-id="0c6e3-134">Hello 포털에서 새 자격 증명 모음 등록 파일을 다운로드 하 고 입력된 toohello 도구로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-134">Download a new Vault Registration file from hello portal and provide it as input toohello tool.</span></span>

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="0c6e3-136">Hello 새 프록시 서버 세부 정보를 제공 하 고 hello 클릭 **등록** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-136">Provide hello new Proxy Server details and click hello **Register** button.</span></span>
6. <span data-ttu-id="0c6e3-137">관리자 PowerShell 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="0c6e3-138">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-138">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="0c6e3-139">있는 경우 확장 프로세스 서버 toothis 구성 서버를 연결, 너무 해야[hello 프록시 설정을 모든 hello 확장 프로세스 서버에서 수정](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) 배포에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-139">If you have Scale-out Process servers attached toothis Configuration Server, you need too[fix hello proxy settings on all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a><span data-ttu-id="0c6e3-140">Hello 사용 하 여 구성 서버를 다시 등록 동일한 복구 서비스 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="0c6e3-140">Re-register a Configuration Server with hello same Recovery Services Vault</span></span>
  1. <span data-ttu-id="0c6e3-141">로그인 tooyour 구성 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-141">Login tooyour Configuration Server.</span></span>
  2. <span data-ttu-id="0c6e3-142">바탕 화면에 바로 가기 hello를 사용 하 여 hello cspsconfigtool.exe를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-142">Launch hello cspsconfigtool.exe using hello shortcut on your desktop.</span></span>
  3. <span data-ttu-id="0c6e3-143">Hello 클릭 **자격 증명 모음 등록** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-143">Click hello **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="0c6e3-144">Hello 포털에서 새 등록 파일을 다운로드 하 고 입력된 toohello 도구로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-144">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>
        <span data-ttu-id="0c6e3-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="0c6e3-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="0c6e3-146">Hello 프록시 서버 세부 정보를 제공 하 고 hello 클릭 **등록** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-146">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
  6. <span data-ttu-id="0c6e3-147">관리자 PowerShell 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="0c6e3-148">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-148">Run hello following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="0c6e3-149">있는 경우 확장 프로세스 서버 toothis 구성 서버를 연결, 너무 필요한[모든 hello 확장 프로세스 서버를 다시 등록](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) 배포에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-149">If you have Scale-out Process servers attached toothis Configuration Server, you need too[re-register all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="0c6e3-150">다른 Recovery Services 자격 증명 모음에 구성 서버 등록</span><span class="sxs-lookup"><span data-stu-id="0c6e3-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="0c6e3-151">로그인 tooyour 구성 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-151">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="0c6e3-152">hello 명령을 실행 하는 관리자 명령 프롬프트에서</span><span class="sxs-lookup"><span data-stu-id="0c6e3-152">from an admin command prompt, run hello command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="0c6e3-153">바로 가기 hello를 사용 하 여 hello cspsconfigtool.exe를 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-153">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
4. <span data-ttu-id="0c6e3-154">Hello 클릭 **자격 증명 모음 등록** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-154">Click hello **Vault Registration** tab.</span></span>
5. <span data-ttu-id="0c6e3-155">Hello 포털에서 새 등록 파일을 다운로드 하 고 입력된 toohello 도구로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-155">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="0c6e3-157">Hello 프록시 서버 세부 정보를 제공 하 고 hello 클릭 **등록** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-157">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
7. <span data-ttu-id="0c6e3-158">관리자 PowerShell 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="0c6e3-159">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-159">Run hello following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="0c6e3-160">구성 서버 서비스 해제</span><span class="sxs-lookup"><span data-stu-id="0c6e3-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="0c6e3-161">구성 서버를 서비스 해제를 시작 하기 전에 hello 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-161">Ensure hello following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="0c6e3-162">이 구성 서버 아래의 모든 가상 컴퓨터에 대한 보호를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="0c6e3-163">모든 복제 정책을 hello 구성 서버에서에서 연결이 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-163">Disassociate all Replication policies from hello Configuration Server.</span></span>
3. <span data-ttu-id="0c6e3-164">Vcenter 서버/vSphere 있는 모든 호스트에 연결 된 toohello 구성 서버를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-164">Delete all vCenters servers/vSphere hosts that are associated toohello Configuration Server.</span></span>

### <a name="delete-hello-configuration-server-from-azure-portal"></a><span data-ttu-id="0c6e3-165">Azure 포털에서 구성 서버 hello를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-165">Delete hello Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="0c6e3-166">Azure 포털에서 찾아보기 너무**사이트 복구 인프라** > **구성 서버** hello 자격 증명 모음의 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-166">In Azure portal, browse too**Site Recovery Infrastructure** > **Configuration Servers** from hello Vault menu.</span></span>
2. <span data-ttu-id="0c6e3-167">Hello toodecommission 구성 서버를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-167">Click hello Configuration Server that you want toodecommission.</span></span>
3. <span data-ttu-id="0c6e3-168">Hello 구성 서버 세부 정보 페이지에서 hello 삭제 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-168">On hello Configuration Server's details page, click hello Delete button.</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="0c6e3-170">클릭 **예** hello 서버의 tooconfirm hello 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-170">Click **Yes** tooconfirm hello deletion of hello server.</span></span>

  >[!WARNING]
  <span data-ttu-id="0c6e3-171">모든 가상 컴퓨터, 복제 정책 또는 vCenter 서버/vSphere 호스트가 구성 서버와 연결 된 경우 hello 서버를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete hello server.</span></span> <span data-ttu-id="0c6e3-172">Toodelete hello 자격 증명 모음을 시도 하기 전에 이러한 엔터티를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-172">Delete these entities before you try toodelete hello vault.</span></span>

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="0c6e3-173">Hello 구성 서버 소프트웨어와 그 종속성 제거</span><span class="sxs-lookup"><span data-stu-id="0c6e3-173">Uninstall hello Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="0c6e3-174">Tooreuse hello Azure Site Recovery와 구성 서버를 다시 계획 하는 경우를 건너뛸 수 있습니다 toostep 4 직접</span><span class="sxs-lookup"><span data-stu-id="0c6e3-174">If you plan tooreuse hello Configuration Server with Azure Site Recovery again, then you can skip toostep 4 directly</span></span>

1. <span data-ttu-id="0c6e3-175">관리자 권한으로 toohello 구성 서버에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-175">Log on toohello Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="0c6e3-176">제어판 > 프로그램 > 프로그램 제거 열기</span><span class="sxs-lookup"><span data-stu-id="0c6e3-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="0c6e3-177">시퀀스를 수행 하는 hello의 hello 프로그램을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-177">Uninstall hello programs in hello following sequence:</span></span>
  * <span data-ttu-id="0c6e3-178">Microsoft Azure Recovery Services 에이전트</span><span class="sxs-lookup"><span data-stu-id="0c6e3-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="0c6e3-179">Microsoft Azure Site Recovery 모바일 서비스/마스터 대상 서버</span><span class="sxs-lookup"><span data-stu-id="0c6e3-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="0c6e3-180">Microsoft Azure Site Recovery 공급자</span><span class="sxs-lookup"><span data-stu-id="0c6e3-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="0c6e3-181">Microsoft Azure Site Recovery 구성 서버/프로세스 서버</span><span class="sxs-lookup"><span data-stu-id="0c6e3-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="0c6e3-182">Microsoft Azure Site Recovery 구성 서버 종속성</span><span class="sxs-lookup"><span data-stu-id="0c6e3-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="0c6e3-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="0c6e3-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="0c6e3-184">다음에서 명령을 hello 및 관리자 명령 프롬프트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-184">Run hello following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="0c6e3-185">구성 서버 SSL(Secure Socket Layer) 인증서 갱신</span><span class="sxs-lookup"><span data-stu-id="0c6e3-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="0c6e3-186">hello 구성 서버에는 기본 제공된 웹 서버, 프로세스 서버 hello 모바일 서비스의 활동을 hello를 오케스트레이션 하는 및 마스터 대상 서버가 toohello 구성 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-186">hello Configuration Server has an inbuilt webserver, which orchestrates hello activities of hello Mobility Service, Process Servers, and Master Target servers connected toohello Configuration Server.</span></span> <span data-ttu-id="0c6e3-187">hello 구성 서버의 웹 서버 SSL 인증서 tooauthenticate 여기에 클라이언트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-187">hello Configuration Server's webserver uses an SSL certificate tooauthenticate its clients.</span></span> <span data-ttu-id="0c6e3-188">이 인증서 만료 3 년 개이고 메서드 뒤 hello를 사용 하 여 언제 든 갱신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-188">This certificate has an expiry of three years and can be renewed at any time using hello following method:</span></span>

> [!WARNING]
<span data-ttu-id="0c6e3-189">인증서 만료는 버전 9.4.XXXX.X 이상에서만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="0c6e3-190">모든 hello Azure Site Recovery 구성 요소 (구성 서버, 프로세스 서버, 마스터 대상 서버, 모바일 서비스)를 업그레이드 전에 hello 인증서 갱신 워크플로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-190">Upgrade all hello Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start hello Renew Certificates workflow.</span></span>

1. <span data-ttu-id="0c6e3-191">Azure 포털 hello, 자격 증명 모음 tooyour 찾아보기 > 사이트 복구 인프라 > 구성 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-191">On hello Azure portal, browse tooyour Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="0c6e3-192">클릭 toorenew 필요한 hello 구성 서버 hello에 대 한 SSL 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-192">Click hello Configuration Server for which you need toorenew hello SSL Certificate for.</span></span>
3. <span data-ttu-id="0c6e3-193">Hello 구성 서버 상태에서 hello SSL 인증서에 대 한 hello 만료 날짜를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-193">Under hello Configuration Server health, you can see hello expiry date for hello SSL Certificate.</span></span>
4. <span data-ttu-id="0c6e3-194">Hello를 클릭 하 여 hello 인증서 갱신 **인증서 갱신** hello 다음 이미지와 같이 작업:</span><span class="sxs-lookup"><span data-stu-id="0c6e3-194">Renew hello certificate by clicking hello **Renew Certificates** action as shown in hello following image:</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="0c6e3-196">보안 소켓 계층 인증서 만료 경고</span><span class="sxs-lookup"><span data-stu-id="0c6e3-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="0c6e3-197">hello 2016 년 5 월 이전에 발생 하는 모든 설치에 대 한 SSL 인증서의 유효 기간 설정 된 tooone 연도입니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-197">hello SSL Certificate's validity for all installations that happened before May 2016 was set tooone year.</span></span> <span data-ttu-id="0c6e3-198">hello Azure 포털에에서 표시 하는 인증서 만료 알림 보기를 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-198">you have started seeing certificate expiry notifications showing up in hello Azure portal.</span></span>

1. <span data-ttu-id="0c6e3-199">Hello 구성 서버 SSL 인증서를 송신 경우 hello에 tooexpire 향후 2 개월 이내, hello Azure 포털 및 전자 메일 (구독 toobe tooAzure Site Recovery 알림 필요)를 통해 사용자에 게 알리는 hello 서비스가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-199">If hello Configuration Server's SSL certificate is going tooexpire in hello next two months, hello service starts notifying users via hello Azure portal & email (you need toobe subscribed tooAzure Site Recovery notifications).</span></span> <span data-ttu-id="0c6e3-200">먼저 hello 자격 증명 모음의 리소스 페이지에 알림 배너를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-200">You start seeing a notification banner on hello Vault's resource page.</span></span>

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="0c6e3-202">Hello 배너 tooget hello 인증서 만료 시 추가 정보를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-202">Click hello banner tooget additional details on hello Certificate expiry.</span></span>

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="0c6e3-204">**지금 갱신** 단추 대신 **지금 업그레이드** 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="0c6e3-205">이 일부 구성 요소는 사용자 환경에서 아직 않은 업그레이드 된 too9.4.xxxx.x 또는 더 높은 버전을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-205">This means that there are some components in your environment that have not yet been upgraded too9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="0c6e3-206">구성 서버에 대한 크기 조정 요구 사항</span><span class="sxs-lookup"><span data-stu-id="0c6e3-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="0c6e3-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="0c6e3-207">**CPU**</span></span> | <span data-ttu-id="0c6e3-208">**메모리**</span><span class="sxs-lookup"><span data-stu-id="0c6e3-208">**Memory**</span></span> | <span data-ttu-id="0c6e3-209">**캐시 디스크 크기**</span><span class="sxs-lookup"><span data-stu-id="0c6e3-209">**Cache disk size**</span></span> | <span data-ttu-id="0c6e3-210">**데이터 변경률**</span><span class="sxs-lookup"><span data-stu-id="0c6e3-210">**Data change rate**</span></span> | <span data-ttu-id="0c6e3-211">**보호된 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="0c6e3-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0c6e3-212">8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="0c6e3-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="0c6e3-213">16GB</span><span class="sxs-lookup"><span data-stu-id="0c6e3-213">16 GB</span></span> |<span data-ttu-id="0c6e3-214">300GB</span><span class="sxs-lookup"><span data-stu-id="0c6e3-214">300 GB</span></span> |<span data-ttu-id="0c6e3-215">500GB 이하</span><span class="sxs-lookup"><span data-stu-id="0c6e3-215">500 GB or less</span></span> |<span data-ttu-id="0c6e3-216">100대 미만의 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="0c6e3-217">12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="0c6e3-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="0c6e3-218">18GB</span><span class="sxs-lookup"><span data-stu-id="0c6e3-218">18 GB</span></span> |<span data-ttu-id="0c6e3-219">600GB</span><span class="sxs-lookup"><span data-stu-id="0c6e3-219">600 GB</span></span> |<span data-ttu-id="0c6e3-220">500GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="0c6e3-220">500 GB too1 TB</span></span> |<span data-ttu-id="0c6e3-221">100-150대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="0c6e3-222">16개 vCPU(2개 소켓 * 8코어 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="0c6e3-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="0c6e3-223">32GB</span><span class="sxs-lookup"><span data-stu-id="0c6e3-223">32 GB</span></span> |<span data-ttu-id="0c6e3-224">1TB</span><span class="sxs-lookup"><span data-stu-id="0c6e3-224">1 TB</span></span> |<span data-ttu-id="0c6e3-225">1TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="0c6e3-225">1 TB too2 TB</span></span> |<span data-ttu-id="0c6e3-226">150-200대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="0c6e3-227">일별 데이터 변동을 프로그램 2TB를 초과 하거나 tooreplicate 200 개 이상의 가상 컴퓨터를 계획, toodeploy 추가 프로세스 서버 tooload hello 복제 트래픽은 분산 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0c6e3-227">If your daily data churn exceeds 2 TB, or you plan tooreplicate more than 200 virtual machines, it is recommended toodeploy additional process servers tooload balance hello replication traffic.</span></span> <span data-ttu-id="0c6e3-228">어떻게 toodeploy 확장 프로세스 서버에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="0c6e3-228">Learn more about How toodeploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="0c6e3-229">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="0c6e3-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
