---
title: " Azure Site Recovery에서 구성 서버 관리 | Microsoft Doc"
description: "이 문서에서는 구성 서버를 설정 및 관리하는 방법을 설명합니다."
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
ms.openlocfilehash: 36da8c7d0f3ace194522e5288f26069cf46d470e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="352f8-103">구성 서버 관리</span><span class="sxs-lookup"><span data-stu-id="352f8-103">Manage a Configuration Server</span></span>

<span data-ttu-id="352f8-104">구성 서버는 Site Recovery 서비스와 온-프레미스 인프라 간의 코디네이터로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-104">Configuration Server acts as a coordinator between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="352f8-105">이 문서에서는 구성 서버를 설정, 구성 및 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-105">This article describes how you can set up, configure, and manage the Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="352f8-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="352f8-106">Prerequisites</span></span>
<span data-ttu-id="352f8-107">다음은 구성 서버를 설정하는 데 필요한 최소 하드웨어, 소프트웨어 및 네트워크 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-107">The following are the minimum hardware, software, and network configuration required to set up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="352f8-108">[용량 계획](site-recovery-capacity-planner.md)은 로드 요구 사항에 맞는 구성으로 구성 서버를 배포하는지 확인하는 중요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="352f8-109">[구성 서버에 대한 크기 조정 요구 사항](#sizing-requirements-for-a-configuration-server)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="352f8-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a><span data-ttu-id="352f8-110">구성 서버 소프트웨어 다운로드</span><span class="sxs-lookup"><span data-stu-id="352f8-110">Downloading the Configuration Server software</span></span>
1. <span data-ttu-id="352f8-111">Azure Portal에 로그온하고 Recovery Services 자격 증명 모음으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="352f8-112">**Site Recovery 인프라** > **구성 서버**(VMware 및 물리적 컴퓨터용 아래)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![서버 페이지 추가](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="352f8-114">**+ 서버** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-114">Click the **+Servers** button.</span></span>
4. <span data-ttu-id="352f8-115">**서버 추가** 페이지에서 다운로드 단추를 클릭하여 등록 키를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-115">On the **Add Server** page, click the Download button to download the Registration key.</span></span> <span data-ttu-id="352f8-116">구성 서버 설치 동안 Azure Site Recovery 서비스에 등록하기 위해 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-116">You need this key during the Configuration Server installation to register it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="352f8-117">**Microsoft Azure Site Recovery 통합 설치 다운로드** 링크를 클릭하여 구성 서버의 최신 버전을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Configuration Server.</span></span>

  ![다운로드 페이지](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="352f8-119">최신 버전의 구성 서버를 [Microsoft 다운로드 센터 다운로드 페이지](http://aka.ms/unifiedsetup)에서 직접 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-119">Latest version of the Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="352f8-120">GUI에서 구성 서버 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="352f8-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="352f8-121">명령줄에서 구성 서버 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="352f8-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="352f8-122">샘플 사용</span><span class="sxs-lookup"><span data-stu-id="352f8-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="352f8-123">구성 서버 설치 관리자 명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="352f8-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="352f8-124">MySql 자격 증명 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="352f8-124">Create a MySql credentials file</span></span>
<span data-ttu-id="352f8-125">MySQLCredsFilePath 매개 변수는 입력으로 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="352f8-126">다음 형식을 사용하여 파일을 만들고 입력 MySQLCredsFilePath 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-126">Create the file using the following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="352f8-127">프록시 설정 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="352f8-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="352f8-128">ProxySettingsFilePath 매개 변수는 입력으로 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="352f8-129">다음 형식을 사용하여 파일을 만들고 입력 ProxySettingsFilePath 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-129">Create the file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="352f8-130">구성 서버의 프록시 설정 수정</span><span class="sxs-lookup"><span data-stu-id="352f8-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="352f8-131">구성 서버에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-131">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="352f8-132">바로 가기를 사용하여 cspsconfigtool.exe를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-132">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
3. <span data-ttu-id="352f8-133">**자격 증명 모음 등록** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-133">Click the **Vault Registration** tab.</span></span>
4. <span data-ttu-id="352f8-134">포털에서 새 자격 증명 모음 등록 파일을 다운로드하고 도구에 대한 입력으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-134">Download a new Vault Registration file from the portal and provide it as input to the tool.</span></span>

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="352f8-136">새 프록시 서버 세부 정보를 제공하고 **등록** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-136">Provide the new Proxy Server details and click the **Register** button.</span></span>
6. <span data-ttu-id="352f8-137">관리자 PowerShell 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="352f8-138">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-138">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="352f8-139">이 구성 서버에 확장 프로세스 서버가 연결된 경우 배포의 [모든 확장 프로세스 서버에서 프록시 설정을 수정](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-139">If you have Scale-out Process servers attached to this Configuration Server, you need to [fix the proxy settings on all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a><span data-ttu-id="352f8-140">동일한 Recovery Services 자격 증명 모음을 사용하여 구성 서버 등록</span><span class="sxs-lookup"><span data-stu-id="352f8-140">Re-register a Configuration Server with the same Recovery Services Vault</span></span>
  1. <span data-ttu-id="352f8-141">구성 서버에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-141">Login to your Configuration Server.</span></span>
  2. <span data-ttu-id="352f8-142">데스크톱에서 바로 가기를 사용하여 cspsconfigtool.exe를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-142">Launch the cspsconfigtool.exe using the shortcut on your desktop.</span></span>
  3. <span data-ttu-id="352f8-143">**자격 증명 모음 등록** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-143">Click the **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="352f8-144">포털에서 새 등록 파일을 다운로드하고 도구에 대한 입력으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-144">Download a new Registration file from the portal and provide it as input to the tool.</span></span>
        <span data-ttu-id="352f8-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="352f8-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="352f8-146">프록시 서버 세부 정보를 제공하고 **등록** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-146">Provide the Proxy Server details and click the **Register** button.</span></span>  
  6. <span data-ttu-id="352f8-147">관리자 PowerShell 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="352f8-148">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-148">Run the following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="352f8-149">확장 프로세스 서버가 이 구성 서버에 연결되어 있는 경우 배포에서 [모든 확장 프로세스 서버를 다시 등록](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-149">If you have Scale-out Process servers attached to this Configuration Server, you need to [re-register all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="352f8-150">다른 Recovery Services 자격 증명 모음에 구성 서버 등록</span><span class="sxs-lookup"><span data-stu-id="352f8-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="352f8-151">구성 서버에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-151">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="352f8-152">관리자 명령 프롬프트에서 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-152">from an admin command prompt, run the command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="352f8-153">바로 가기를 사용하여 cspsconfigtool.exe를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-153">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
4. <span data-ttu-id="352f8-154">**자격 증명 모음 등록** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-154">Click the **Vault Registration** tab.</span></span>
5. <span data-ttu-id="352f8-155">포털에서 새 등록 파일을 다운로드하고 도구에 대한 입력으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-155">Download a new Registration file from the portal and provide it as input to the tool.</span></span>

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="352f8-157">프록시 서버 세부 정보를 제공하고 **등록** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-157">Provide the Proxy Server details and click the **Register** button.</span></span>  
7. <span data-ttu-id="352f8-158">관리자 PowerShell 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="352f8-159">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-159">Run the following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="352f8-160">구성 서버 서비스 해제</span><span class="sxs-lookup"><span data-stu-id="352f8-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="352f8-161">구성 서버의 서비스 해제를 시작하기 전에 다음 사항을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="352f8-161">Ensure the following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="352f8-162">이 구성 서버 아래의 모든 가상 컴퓨터에 대한 보호를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="352f8-163">구성 서버에서 모든 복제 정책을 연결 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-163">Disassociate all Replication policies from the Configuration Server.</span></span>
3. <span data-ttu-id="352f8-164">구성 서버에 연결된 모든 vCenter 서버/vSphere 호스트를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-164">Delete all vCenters servers/vSphere hosts that are associated to the Configuration Server.</span></span>

### <a name="delete-the-configuration-server-from-azure-portal"></a><span data-ttu-id="352f8-165">Azure Portal에서 구성 서버 삭제</span><span class="sxs-lookup"><span data-stu-id="352f8-165">Delete the Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="352f8-166">Azure Portal의 자격 증명 모음 메뉴에서 **Site Recovery 인프라** > **구성 서버**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-166">In Azure portal, browse to **Site Recovery Infrastructure** > **Configuration Servers** from the Vault menu.</span></span>
2. <span data-ttu-id="352f8-167">서비스를 해제하려는 구성 서버를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-167">Click the Configuration Server that you want to decommission.</span></span>
3. <span data-ttu-id="352f8-168">구성 서버의 세부 정보 페이지에서 삭제 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-168">On the Configuration Server's details page, click the Delete button.</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="352f8-170">**예**를 클릭하여 서버 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-170">Click **Yes** to confirm the deletion of the server.</span></span>

  >[!WARNING]
  <span data-ttu-id="352f8-171">가상 컴퓨터, 복제 정책 또는 vCenter 서버/vSphere 호스트가 이 구성 서버에 연결되어 있으면 서버를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete the server.</span></span> <span data-ttu-id="352f8-172">자격 증명 모음을 삭제하기 전에 이러한 엔터티를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-172">Delete these entities before you try to delete the vault.</span></span>

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="352f8-173">구성 서버 소프트웨어 및 해당 종속성 제거</span><span class="sxs-lookup"><span data-stu-id="352f8-173">Uninstall the Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="352f8-174">Azure Site Recovery에서 구성 서버를 다시 사용하려는 경우에는 4단계로 직접 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-174">If you plan to reuse the Configuration Server with Azure Site Recovery again, then you can skip to step 4 directly</span></span>

1. <span data-ttu-id="352f8-175">관리자 권한으로 구성 서버에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-175">Log on to the Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="352f8-176">제어판 > 프로그램 > 프로그램 제거 열기</span><span class="sxs-lookup"><span data-stu-id="352f8-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="352f8-177">다음 순서로 프로그램을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-177">Uninstall the programs in the following sequence:</span></span>
  * <span data-ttu-id="352f8-178">Microsoft Azure Recovery Services 에이전트</span><span class="sxs-lookup"><span data-stu-id="352f8-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="352f8-179">Microsoft Azure Site Recovery 모바일 서비스/마스터 대상 서버</span><span class="sxs-lookup"><span data-stu-id="352f8-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="352f8-180">Microsoft Azure Site Recovery 공급자</span><span class="sxs-lookup"><span data-stu-id="352f8-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="352f8-181">Microsoft Azure Site Recovery 구성 서버/프로세스 서버</span><span class="sxs-lookup"><span data-stu-id="352f8-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="352f8-182">Microsoft Azure Site Recovery 구성 서버 종속성</span><span class="sxs-lookup"><span data-stu-id="352f8-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="352f8-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="352f8-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="352f8-184">관리자 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-184">Run the following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="352f8-185">구성 서버 SSL(Secure Socket Layer) 인증서 갱신</span><span class="sxs-lookup"><span data-stu-id="352f8-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="352f8-186">구성 서버에는 기본 제공 웹 서버가 있습니다. 이 서버는 구성 서버에 연결된 모바일 서비스, 프로세스 서버 및 마스터 대상 서버의 작업을 오케스트레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-186">The Configuration Server has an inbuilt webserver, which orchestrates the activities of the Mobility Service, Process Servers, and Master Target servers connected to the Configuration Server.</span></span> <span data-ttu-id="352f8-187">구성 서버의 웹 서버는 SSL 인증서를 사용하여 해당 클라이언트를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-187">The Configuration Server's webserver uses an SSL certificate to authenticate its clients.</span></span> <span data-ttu-id="352f8-188">이 인증서의 만료 기간은 3년이며 다음 방법을 사용하여 언제든지 갱신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-188">This certificate has an expiry of three years and can be renewed at any time using the following method:</span></span>

> [!WARNING]
<span data-ttu-id="352f8-189">인증서 만료는 버전 9.4.XXXX.X 이상에서만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="352f8-190">인증서 갱신 워크플로를 시작하기 전에 모든 Azure Site Recovery 구성 요소(구성 서버, 프로세스 서버, 마스터 대상 서버, 모바일 서비스)를 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-190">Upgrade all the Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start the Renew Certificates workflow.</span></span>

1. <span data-ttu-id="352f8-191">Azure Portal에서 자격 증명 모음 > Site Recovery 인프라 > 구성 서버로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-191">On the Azure portal, browse to your Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="352f8-192">SSL 인증서를 갱신해야 하는 구성 서버를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-192">Click the Configuration Server for which you need to renew the SSL Certificate for.</span></span>
3. <span data-ttu-id="352f8-193">구성 서버 상태에서 SSL 인증서에 대한 만료 날짜를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-193">Under the Configuration Server health, you can see the expiry date for the SSL Certificate.</span></span>
4. <span data-ttu-id="352f8-194">다음 그림과 같이 **인증서 갱신** 작업을 클릭하여 인증서를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-194">Renew the certificate by clicking the **Renew Certificates** action as shown in the following image:</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="352f8-196">보안 소켓 계층 인증서 만료 경고</span><span class="sxs-lookup"><span data-stu-id="352f8-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="352f8-197">2016년 5월 이전에 발생한 모든 설치에 대한 SSL 인증서의 유효 기간은 1년으로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-197">The SSL Certificate's validity for all installations that happened before May 2016 was set to one year.</span></span> <span data-ttu-id="352f8-198">Azure Portal에 인증서 만료 알림이 표시되기 시작했을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-198">you have started seeing certificate expiry notifications showing up in the Azure portal.</span></span>

1. <span data-ttu-id="352f8-199">구성 서버의 SSL 인증서가 향후 2개월 내에 만료 예정인 경우 Azure Portal 및 전자 메일을 통해 사용자에게 알림이 제공되기 시작합니다(Azure Site Recovery 알림을 구독해야 함).</span><span class="sxs-lookup"><span data-stu-id="352f8-199">If the Configuration Server's SSL certificate is going to expire in the next two months, the service starts notifying users via the Azure portal & email (you need to be subscribed to Azure Site Recovery notifications).</span></span> <span data-ttu-id="352f8-200">자격 증명 모음 리소스 페이지에 알림 배너가 표시되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-200">You start seeing a notification banner on the Vault's resource page.</span></span>

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="352f8-202">이 배너를 클릭하면 인증서 만료에 대한 추가 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-202">Click the banner to get additional details on the Certificate expiry.</span></span>

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="352f8-204">**지금 갱신** 단추 대신 **지금 업그레이드** 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="352f8-205">이것은 작업 환경의 일부 구성 요소가 아직 9.4.xxxx.x 이상 버전으로 업그레이드되지 않았음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-205">This means that there are some components in your environment that have not yet been upgraded to 9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="352f8-206">구성 서버에 대한 크기 조정 요구 사항</span><span class="sxs-lookup"><span data-stu-id="352f8-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="352f8-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="352f8-207">**CPU**</span></span> | <span data-ttu-id="352f8-208">**메모리**</span><span class="sxs-lookup"><span data-stu-id="352f8-208">**Memory**</span></span> | <span data-ttu-id="352f8-209">**캐시 디스크 크기**</span><span class="sxs-lookup"><span data-stu-id="352f8-209">**Cache disk size**</span></span> | <span data-ttu-id="352f8-210">**데이터 변경률**</span><span class="sxs-lookup"><span data-stu-id="352f8-210">**Data change rate**</span></span> | <span data-ttu-id="352f8-211">**보호된 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="352f8-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="352f8-212">8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="352f8-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="352f8-213">16GB</span><span class="sxs-lookup"><span data-stu-id="352f8-213">16 GB</span></span> |<span data-ttu-id="352f8-214">300GB</span><span class="sxs-lookup"><span data-stu-id="352f8-214">300 GB</span></span> |<span data-ttu-id="352f8-215">500GB 이하</span><span class="sxs-lookup"><span data-stu-id="352f8-215">500 GB or less</span></span> |<span data-ttu-id="352f8-216">100대 미만의 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="352f8-217">12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="352f8-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="352f8-218">18GB</span><span class="sxs-lookup"><span data-stu-id="352f8-218">18 GB</span></span> |<span data-ttu-id="352f8-219">600GB</span><span class="sxs-lookup"><span data-stu-id="352f8-219">600 GB</span></span> |<span data-ttu-id="352f8-220">500GB ~ 1TB</span><span class="sxs-lookup"><span data-stu-id="352f8-220">500 GB to 1 TB</span></span> |<span data-ttu-id="352f8-221">100-150대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="352f8-222">16개 vCPU(2개 소켓 * 8코어 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="352f8-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="352f8-223">32GB</span><span class="sxs-lookup"><span data-stu-id="352f8-223">32 GB</span></span> |<span data-ttu-id="352f8-224">1TB</span><span class="sxs-lookup"><span data-stu-id="352f8-224">1 TB</span></span> |<span data-ttu-id="352f8-225">1TB ~ 2TB</span><span class="sxs-lookup"><span data-stu-id="352f8-225">1 TB to 2 TB</span></span> |<span data-ttu-id="352f8-226">150-200대 컴퓨터를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="352f8-227">일별 데이터 변동이 2TB를 초과하거나 200개 이상의 가상 컴퓨터를 복제하려는 경우 추가 프로세스 서버를 배포하여 복제 트래픽 부하를 분산하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-227">If your daily data churn exceeds 2 TB, or you plan to replicate more than 200 virtual machines, it is recommended to deploy additional process servers to load balance the replication traffic.</span></span> <span data-ttu-id="352f8-228">확장 프로세스 서버를 배포하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="352f8-228">Learn more about How to deploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="352f8-229">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="352f8-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
