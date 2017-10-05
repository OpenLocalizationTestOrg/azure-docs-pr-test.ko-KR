---
title: "Azure 백업: PowerShell을 사용하여 DPM 워크로드 백업 | Microsoft Docs"
description: "PowerShell을 사용하여 DPM(Data Protection Manager)에 대해 Azure 백업을 배포 및 관리하는 방법을 알아봅니다."
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 943a12dcba49a114d206b9dab968da332ea99926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="74ef7-103">PowerShell을 사용하여 DPM(Data Protection Manager) 서버용 Azure 백업 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="74ef7-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74ef7-104">ARM</span><span class="sxs-lookup"><span data-stu-id="74ef7-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="74ef7-105">클래식</span><span class="sxs-lookup"><span data-stu-id="74ef7-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="74ef7-106">이 문서에서는 PowerShell을 사용하여 백업 자격 증명 모음에서 DPM 데이터를 백업 및 복구하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-106">This article explains how to use PowerShell to back up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="74ef7-107">모든 새 배포에 Recovery Services 자격 증명 모음을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="74ef7-108">새 Azure Backup 사용자인 경우 [PowerShell을 사용하여 Data Protection Manager 데이터를 Azure로 배포 및 관리](backup-dpm-automation.md) 문서를 사용하여 Recovery Services 자격 증명 모음에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-108">If you are a new Azure Backup user, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74ef7-109">이제 Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="74ef7-110">자세한 내용은 [Recovery Services 자격 증명 모음으로 Backup 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74ef7-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="74ef7-111">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="74ef7-112">2017년 10월 15일 이후부터는 PowerShell을 사용하여 Backup 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="74ef7-113">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="74ef7-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="74ef7-114">남아 있는 모든 Backup 자격 증명 모음이 Recovery Services 자격 증명 모음으로 자동 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="74ef7-115">클래식 포털에서는 백업 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="74ef7-116">대신 Azure Portal을 사용하여 Recovery Services 자격 증명 모음에서 백업 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="74ef7-117">PowerShell 환경 설정</span><span class="sxs-lookup"><span data-stu-id="74ef7-117">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="74ef7-118">PowerShell을 사용하여 Data Protection Manager에서 Azure로의 백업을 관리하기 전에 PowerShell에서 적합한 환경을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-118">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you will need to have the right environment in PowerShell.</span></span> <span data-ttu-id="74ef7-119">PowerShell 세션 시작 시 다음 명령을 실행하여 정확한 모듈을 가져오고 DPM cmdlet을 올바르게 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-119">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="74ef7-120">설정 및 등록</span><span class="sxs-lookup"><span data-stu-id="74ef7-120">Setup and Registration</span></span>
<span data-ttu-id="74ef7-121">시작하려면</span><span class="sxs-lookup"><span data-stu-id="74ef7-121">To begin:</span></span>

1. <span data-ttu-id="74ef7-122">[최신 PowerShell을 다운로드](https://github.com/Azure/azure-powershell/releases)합니다(필요한 최소 버전: 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="74ef7-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="74ef7-123">다음과 같은 *Switch-azuremode* commandlet을 통해 **AzureResourceManager** 모드로 전환하여 Azure 백업 commandlet을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-123">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="74ef7-124">PowerShell로 다음과 같은 설정 및 등록 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-124">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="74ef7-125">백업 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="74ef7-125">Create a backup vault</span></span>
* <span data-ttu-id="74ef7-126">Azure 백업 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="74ef7-126">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="74ef7-127">Azure 백업 서비스 등록</span><span class="sxs-lookup"><span data-stu-id="74ef7-127">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="74ef7-128">네트워킹 서비스</span><span class="sxs-lookup"><span data-stu-id="74ef7-128">Networking settings</span></span>
* <span data-ttu-id="74ef7-129">암호화 설정</span><span class="sxs-lookup"><span data-stu-id="74ef7-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="74ef7-130">백업 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="74ef7-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="74ef7-131">처음으로 Azure 백업을 사용하는 고객의 경우, 구독과 함께 사용할 Azure 백업 공급자를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-131">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="74ef7-132">이는 다음 명령을 실행하여 수행할 수 있습니다. Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="74ef7-132">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="74ef7-133">**New-AzureRMBackupVault** commandlet을 사용하여 새 백업 자격 증명 모음을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-133">You can create a new backup vault using the **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="74ef7-134">백업 저장소는 ARM 리소스이므로 리소스 그룹 내에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-134">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="74ef7-135">승격된 Azure PowerShell 콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-135">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="74ef7-136">**Get-AzureRMBackupVault** commandlet을 사용하여 지정된 구독의 모든 백업 자격 증명 모음 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-136">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="74ef7-137">DPM 서버에 Azure 백업 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="74ef7-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="74ef7-138">Azure 백업 에이전트를 설치하기 전에 Windows Server에 설치 관리자를 다운로드해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="74ef7-139">최신 버전의 설치 관리자는 [Microsoft 다운로드 센터](http://aka.ms/azurebackup_agent) 또는 백업 자격 증명 모음 대시보드 페이지에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="74ef7-140">쉽게 액세스할 수 있는 위치(예: *C:\Downloads\*)에 설치 관리자를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="74ef7-141">에이전트를 설치하려면 **DPM 서버**의 승격된 PowerShell 콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="74ef7-142">그러면 에이전트가 모두 기본 옵션으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="74ef7-143">설치는 백그라운드에서 몇 분 정도 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="74ef7-144">*/nu* 옵션을 지정하지 않으면 설치 마지막에 **Windows 업데이트** 창이 열리고 업데이트가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-144">If you do not specify the */nu* option the **Windows Update** window will open at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="74ef7-145">설치된 프로그램 목록에 에이전트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-145">The agent will show in the list of installed programs.</span></span> <span data-ttu-id="74ef7-146">설치된 프로그램 목록을 보려면 **제어판** > **프로그램** > **프로그램 및 기능**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![에이전트 설치됨](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="74ef7-148">설치 옵션</span><span class="sxs-lookup"><span data-stu-id="74ef7-148">Installation options</span></span>
<span data-ttu-id="74ef7-149">명령줄을 통해 사용 가능한 모든 옵션을 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-149">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="74ef7-150">사용 가능한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-150">The available options include:</span></span>

| <span data-ttu-id="74ef7-151">옵션</span><span class="sxs-lookup"><span data-stu-id="74ef7-151">Option</span></span> | <span data-ttu-id="74ef7-152">세부 정보</span><span class="sxs-lookup"><span data-stu-id="74ef7-152">Details</span></span> | <span data-ttu-id="74ef7-153">기본값</span><span class="sxs-lookup"><span data-stu-id="74ef7-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="74ef7-154">/q</span><span class="sxs-lookup"><span data-stu-id="74ef7-154">/q</span></span> |<span data-ttu-id="74ef7-155">자동 설치</span><span class="sxs-lookup"><span data-stu-id="74ef7-155">Quiet installation</span></span> |- |
| <span data-ttu-id="74ef7-156">/p:"위치"</span><span class="sxs-lookup"><span data-stu-id="74ef7-156">/p:"location"</span></span> |<span data-ttu-id="74ef7-157">Azure 백업 에이전트의 설치 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="74ef7-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="74ef7-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="74ef7-159">/s:"위치"</span><span class="sxs-lookup"><span data-stu-id="74ef7-159">/s:"location"</span></span> |<span data-ttu-id="74ef7-160">Azure 백업 에이전트의 캐시 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="74ef7-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="74ef7-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="74ef7-162">/m</span><span class="sxs-lookup"><span data-stu-id="74ef7-162">/m</span></span> |<span data-ttu-id="74ef7-163">Microsoft 업데이트에 옵트인</span><span class="sxs-lookup"><span data-stu-id="74ef7-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="74ef7-164">/nu</span><span class="sxs-lookup"><span data-stu-id="74ef7-164">/nu</span></span> |<span data-ttu-id="74ef7-165">설치가 완료된 후 업데이트에 대한 검사 안 함</span><span class="sxs-lookup"><span data-stu-id="74ef7-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="74ef7-166">/d</span><span class="sxs-lookup"><span data-stu-id="74ef7-166">/d</span></span> |<span data-ttu-id="74ef7-167">Microsoft Azure Recovery Services 에이전트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="74ef7-168">/ph</span><span class="sxs-lookup"><span data-stu-id="74ef7-168">/ph</span></span> |<span data-ttu-id="74ef7-169">프록시 호스트 주소</span><span class="sxs-lookup"><span data-stu-id="74ef7-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="74ef7-170">/po</span><span class="sxs-lookup"><span data-stu-id="74ef7-170">/po</span></span> |<span data-ttu-id="74ef7-171">프록시 호스트 포트 번호</span><span class="sxs-lookup"><span data-stu-id="74ef7-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="74ef7-172">/pu</span><span class="sxs-lookup"><span data-stu-id="74ef7-172">/pu</span></span> |<span data-ttu-id="74ef7-173">프록시 호스트 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="74ef7-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="74ef7-174">/pw</span><span class="sxs-lookup"><span data-stu-id="74ef7-174">/pw</span></span> |<span data-ttu-id="74ef7-175">프록시 암호</span><span class="sxs-lookup"><span data-stu-id="74ef7-175">Proxy Password</span></span> |- |

### <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="74ef7-176">Azure 백업 서비스 등록</span><span class="sxs-lookup"><span data-stu-id="74ef7-176">Registering with the Azure Backup service</span></span>
<span data-ttu-id="74ef7-177">Azure 백업 서비스에 등록하려면 먼저 [필수 조건](backup-azure-dpm-introduction.md)이 충족되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-177">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="74ef7-178">다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-178">You must:</span></span>

* <span data-ttu-id="74ef7-179">유효한 Azure 구독이 있어야 함</span><span class="sxs-lookup"><span data-stu-id="74ef7-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="74ef7-180">백업 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="74ef7-180">Have a backup vault</span></span>

<span data-ttu-id="74ef7-181">자격 증명 모음을 다운로드하려면 Azure PowerShell 콘솔에서 **Get-AzureBackupVaultCredentials** commandlet을 실행하고 *C:\Downloads\*와 같은 편리한 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-181">To download the vault credentials, run the **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="74ef7-182">[Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet을 사용하여 컴퓨터에 저장소를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-182">Registering the machine with the vault is done using the [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="74ef7-183">그러면 지정된 저장소 자격 증명을 사용하여 “TestingServer”라는 DPM 서버에 Microsoft Azure 저장소가 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-183">This will register the DPM Server named “TestingServer” with Microsoft Azure Vault using the specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74ef7-184">저장소 자격 증명 파일을 지정할 때 상대 경로를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="74ef7-184">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="74ef7-185">cmdlet 입력 내용은 반드시 절대 경로를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-185">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="74ef7-186">초기 구성 설정</span><span class="sxs-lookup"><span data-stu-id="74ef7-186">Initial configuration settings</span></span>
<span data-ttu-id="74ef7-187">DPM 서버를 Azure 백업 저장소에 등록하면 기본 구독 설정으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-187">Once the DPM Server is registered with the Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="74ef7-188">이러한 구독 설정에는 네트워킹, 암호화 및 스테이징 영역이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-188">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="74ef7-189">구독 설정을 변경하려면 우선 [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet을 사용하여 기존(기본) 설정에 대한 핸들을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-189">To begin changing the subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="74ef7-190">[Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet을 사용하여 이 로컬 PowerShell 개체 ```$setting```에 대한 모든 수정을 수행한 다음 전체 개체를 DPM 및 Azure 백업에 커밋하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-190">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="74ef7-191">```–Commit``` 플래그를 사용하여 해당 변경 내용이 유지되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-191">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="74ef7-192">커밋하지 않으면 설정이 적용되지 않으며 Azure 백업에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-192">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="74ef7-193">네트워킹</span><span class="sxs-lookup"><span data-stu-id="74ef7-193">Networking</span></span>
<span data-ttu-id="74ef7-194">프록시 서버를 통해 DPM 컴퓨터를 인터넷상의 Azure 백업 서비스에 연결하는 경우 백업에 성공하려면 프록시 서버 설정을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-194">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for backups to succeed.</span></span> <span data-ttu-id="74ef7-195">이 작업은 ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` 및 ```ProxyPassword``` 매개 변수를 [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet과 함께 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-195">This is done by using the ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="74ef7-196">이 예제에서는 프록시 서버가 없으므로 프록시와 관련된 모든 정보를 명시적으로 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="74ef7-197">대역폭 사용 역시 주의 정해진 요일에 대해 ```-WorkHourBandwidth``` 및 ```-NonWorkHourBandwidth``` 옵션으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="74ef7-198">이 예제에서는 제한을 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-the-staging-area"></a><span data-ttu-id="74ef7-199">스테이징 영역 구성</span><span class="sxs-lookup"><span data-stu-id="74ef7-199">Configuring the staging Area</span></span>
<span data-ttu-id="74ef7-200">DPM 서버에서 실행 중인 Azure 백업 에이전트에는 클라우드로부터 복원된 데이터를 위한 임시 저장소가 필요합니다(로컬 스테이징 영역).</span><span class="sxs-lookup"><span data-stu-id="74ef7-200">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="74ef7-201">[Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet과 ```-StagingAreaPath``` 매개 변수를 사용하여 스테이징 영역을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-201">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="74ef7-202">위의 예제에서 스테이징 영역은 PowerShell 개체 ```$setting```에서 *C:\StagingArea*로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-202">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="74ef7-203">지정된 폴더가 이미 있어야 하며, 그렇지 않으면 구독 설정의 최종 커밋에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-203">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="74ef7-204">암호화 설정</span><span class="sxs-lookup"><span data-stu-id="74ef7-204">Encryption settings</span></span>
<span data-ttu-id="74ef7-205">Azure 백업에 전송되는 백업 데이터는 데이터의 기밀성을 보호하기 위해 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-205">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="74ef7-206">암호화 암호는 복원 시 데이터를 해독하기 위한 “암호"입니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-206">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="74ef7-207">이 정보를 설정한 후에 안전하게 보관하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-207">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="74ef7-208">아래 예제에서 첫 번째 명령은 ```passphrase123456789``` 문자열을 보안 문자열로 변환하고 보안 문자열을 ```$Passphrase```(이)라는 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-208">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="74ef7-209">두 번째 명령은 암호화 백업의 암호로 ```$Passphrase```에서 보안 문자열을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-209">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="74ef7-210">암호 정보를 설정한 후에는 안전하게 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-210">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="74ef7-211">이 암호 없이는 Azure에서 데이터를 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-211">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="74ef7-212">이 시점에서 ```$setting``` 개체에 필요한 모든 사항을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-212">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="74ef7-213">변경 내용은 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-213">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="74ef7-214">Azure 백업에 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="74ef7-214">Protect data to Azure Backup</span></span>
<span data-ttu-id="74ef7-215">이 섹션에서는 DPM에 프로덕션 서버를 추가한 후 데이터를 로컬 DPM 저장소에 보호한 다음 Azure 백업에 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-215">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="74ef7-216">예제에서 파일과 폴더를 백업하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-216">In the examples we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="74ef7-217">논리는 모든 DPM 지원 데이터 소스를 백업하도록 쉽게 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-217">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="74ef7-218">모든 DPM 백업은 4개 부분으로 구성된 보호 그룹(PG)에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="74ef7-219">**그룹 멤버**는 동일한 보호 그룹 내에서 보호하려는 모든 보호 개체(DPM에서는 *데이터 원본*)의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-219">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="74ef7-220">예를 들어, 백업 요구 사항이 다르기 때문에 하나의 보호 그룹에서는 프로덕션 VM을 보호하고 다른 보호 그룹에서는 SQL Server 데이터베이스를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-220">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="74ef7-221">프로덕션 서버에 데이터 원본을 백업할 수 있으려면 DPM 에이전트가 서버에 설치되어 있고 DPM에 의해 관리되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-221">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="74ef7-222">[DPM 에이전트를 설치](https://technet.microsoft.com/library/bb870935.aspx)하고 해당 DPM 서버에 링크하는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-222">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="74ef7-223">**데이터 보호 방법**은 대상 백업 위치(테이프, 디스크 및 클라우드)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-223">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="74ef7-224">이 예에서는 데이터를 로컬 디스크와 클라우드에 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-224">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="74ef7-225">백업을 수행해야 할 때와 DPM 서버 및 프로덕션 서버 간의 데이터 동기화 빈도를 지정하는 **백업 일정**입니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-225">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="74ef7-226">Azure에 복구 지점을 보존할 기간을 지정하는 **보존 일정**입니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-226">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="74ef7-227">보호 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="74ef7-227">Creating a protection group</span></span>
<span data-ttu-id="74ef7-228">[New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet을 사용하여 새 보호 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-228">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="74ef7-229">위의 cmdlet은 *ProtectGroup01* 보호 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-229">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="74ef7-230">나중에 기존 보호 그룹을 수정하여 Azure 클라우드에 백업을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-230">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="74ef7-231">하지만 보호 그룹(신규 또는 기존)을 변경하려면 *Get-DPMModifiableProtectionGroup* cmdlet을 사용하여 [수정 가능한](https://technet.microsoft.com/library/hh881713) 개체에 대한 핸들을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-231">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="74ef7-232">보호 그룹에 그룹 멤버 추가</span><span class="sxs-lookup"><span data-stu-id="74ef7-232">Adding group members to the Protection Group</span></span>
<span data-ttu-id="74ef7-233">각 DPM 에이전트는 설치된 서버의 데이터 원본 목록을 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-233">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="74ef7-234">데이터 원본을 보호 그룹에 추가하려면 DPM 에이전트가 먼저 DPM 서버에 데이터 원본 목록이 다시 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-234">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="74ef7-235">그런 다음 하나 이상의 데이터 원본을 선택하여 보호 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-235">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="74ef7-236">이 작업을 수행하는 데 필요한 PowerShell 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-236">The PowerShell steps needed to get achieve this are:</span></span>

1. <span data-ttu-id="74ef7-237">DPM 에이전트를 통해 DPM에 의해 관리되는 모든 서버 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-237">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="74ef7-238">특정 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-238">Choose a specific server.</span></span>
3. <span data-ttu-id="74ef7-239">서버의 모든 데이터 원본 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-239">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="74ef7-240">하나 이상의 데이터 원본을 선택하고 보호 그룹에 추가</span><span class="sxs-lookup"><span data-stu-id="74ef7-240">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="74ef7-241">DPM 에이전트가 설치되어 있고 DPM 서버에 의해 관리되고 있는 서버 목록은 [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet을 사용하여 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-241">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="74ef7-242">이 예제에서는 백업에 대해 이름이 *productionserver01* 인 PS만 필터링하여 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="74ef7-243">이제 [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet을 사용하여 ```$server```에서 데이터 원본 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-243">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="74ef7-244">이 예제에서는 백업을 위해 구성하려는 *D:\* 볼륨을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-244">In this example we are filtering for the volume *D:\* which we want to configure for backup.</span></span> <span data-ttu-id="74ef7-245">그런 다음 이 데이터 원본은 [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet을 사용하여 보호 그룹에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-245">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="74ef7-246">추가하려면 *수정 가능한* ```$MPG``` 보호 그룹 개체를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-246">Remember to use the *modifable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="74ef7-247">선택한 모든 데이터 원본이 보호 그룹에 추가될 때까지 필요한 만큼 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-247">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="74ef7-248">또한 하나의 데이터 원본으로만 시작한 다음, 보호 그룹을 만들기 위한 워크플로를 완료하고 나중에 해당 보호 그룹에 더 많은 데이터 원본을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-248">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="74ef7-249">데이터 보호 방법 선택</span><span class="sxs-lookup"><span data-stu-id="74ef7-249">Selecting the data protection method</span></span>
<span data-ttu-id="74ef7-250">데이터 원본이 보호 그룹에 추가되고 나면 다음 단계는 [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet을 사용하여 보호 방법을 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-250">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="74ef7-251">이 예제에서는 보호 그룹이 로컬 디스크 및 클라우드 백업에 대한 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-251">In this example, the Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="74ef7-252">-Online 플래그와 함께 [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet을 사용하여 클라우드에 대해 보호하려는 데이터소스를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-252">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="74ef7-253">보존 범위 설정</span><span class="sxs-lookup"><span data-stu-id="74ef7-253">Setting the retention range</span></span>
<span data-ttu-id="74ef7-254">[Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet을 사용하여 백업 시점의 보존을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-254">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="74ef7-255">백업 일정을 정의하기 전에 보존을 설정하는 것이 좀 이상하게 보일 수 있지만 ```Set-DPMPolicyObjective``` cmdlet을 사용하면 기본 백업 일정이 자동으로 설정되며, 이 일정은 나중에 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-255">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="74ef7-256">항상 백업 일정을 먼저 설정하고 그 후에 보존 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-256">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="74ef7-257">아래 예제에서는 cmdlet이 디스크 백업에 대한 보존 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-257">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="74ef7-258">이 값은 10일 동안 백업을 유지하고 6시간마다 프로덕션 서버와 DPM 서버 간에 데이터를 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-258">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="74ef7-259">```SynchronizationFrequencyMinutes```는 백업 시점 생성 빈도를 정의하지 않지만 DPM 서버에 데이터를 복사하는 빈도는 정의합니다. 따라서 백업이 너무 커지지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-259">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="74ef7-260">Azure에 백업하는 경우(DPM에서는 온라인 백업) [GFS(Grandfather-Father-Son) 체계를 사용하여 장기 보존](backup-azure-backup-cloud-as-tape.md)을 위한 보존 범위를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-260">For backups going to Azure (DPM refers to these as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="74ef7-261">즉, 매일, 매주, 매월 및 매년 보존 정책이 포함된 통합 보존 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="74ef7-262">이 예에서는 필요한 복잡한 보존 체계를 나타내는 배열을 만든 다음 [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet을 사용하여 보존 범위를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-262">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="74ef7-263">백업 일정 설정</span><span class="sxs-lookup"><span data-stu-id="74ef7-263">Set the backup schedule</span></span>
<span data-ttu-id="74ef7-264">```Set-DPMPolicyObjective``` cmdlet을 사용하여 보호 목표를 지정하면 DPM은 기본 백업 일정을 자동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-264">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="74ef7-265">기본 일정을 변경하려면 [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet을 사용한 후 [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-265">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="74ef7-266">위의 예에서 ```$onlineSch```는 GFS 체계에서 보호 그룹에 대한 기존 온라인 보호 일정이 포함된 4개의 요소가 있는 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-266">In the example above, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="74ef7-267">```$onlineSch[0]```에는 매일 일정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-267">```$onlineSch[0]``` will contain the daily schedule</span></span>
2. <span data-ttu-id="74ef7-268">```$onlineSch[1]```에는 매주 일정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-268">```$onlineSch[1]``` will contain the weekly schedule</span></span>
3. <span data-ttu-id="74ef7-269">```$onlineSch[2]```에는 매월 일정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-269">```$onlineSch[2]``` will contain the monthly schedule</span></span>
4. <span data-ttu-id="74ef7-270">```$onlineSch[3]```에는 매년 일정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-270">```$onlineSch[3]``` will contain the yearly schedule</span></span>

<span data-ttu-id="74ef7-271">따라서 매주 일정을 수정해야 하는 경우에는 ```$onlineSch[1]```을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-271">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="74ef7-272">초기 백업</span><span class="sxs-lookup"><span data-stu-id="74ef7-272">Initial backup</span></span>
<span data-ttu-id="74ef7-273">데이터 원본을 처음으로 백업하는 경우, DPM은 최초 복제본을 만들어야 하며, 이것은 DPM 복제본 볼륨에서 보호될 데이터 원본의 사본을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-273">When backing up a datasource for the first time, DPM needs to create an initial replica which will create a copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="74ef7-274">이 작업은 [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet을 ```-NOW``` 매개 변수와 함께 사용하여 특정 시간 동안 예약하거나 수동으로 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-274">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="74ef7-275">DPM 복제본 및 복구 지점 볼륨 크기 변경</span><span class="sxs-lookup"><span data-stu-id="74ef7-275">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="74ef7-276">또한 아래의 예제와 같이 [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet을 사용하여 섀도 복사본 볼륨뿐만 아니라 DPM 복제본 볼륨의 크기를 변경할 수 있습니다. Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="74ef7-276">You can also change the size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="74ef7-277">보호 그룹에 변경 내용 커밋</span><span class="sxs-lookup"><span data-stu-id="74ef7-277">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="74ef7-278">마지막으로, 변경 내용을 DPM이 새로운 보호 그룹 구성에 따라 백업을 수행하기 전에 먼저 변경 내용을 커밋해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-278">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="74ef7-279">이 작업은 [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet을 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-279">This is done using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="74ef7-280">백업 시점 보기</span><span class="sxs-lookup"><span data-stu-id="74ef7-280">View the backup points</span></span>
<span data-ttu-id="74ef7-281">[Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet을 사용하여 데이터 원본에 대한 모든 복구 지점 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-281">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="74ef7-282">이 예제에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-282">In this example, we will:</span></span>

* <span data-ttu-id="74ef7-283"> ```$PG```</span><span class="sxs-lookup"><span data-stu-id="74ef7-283">fetch all the PGs on the DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="74ef7-284"> ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="74ef7-284">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="74ef7-285">데이터 원본에 대한 모든 복구 지점을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-285">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="74ef7-286">Azure에 보호된 데이터 복원</span><span class="sxs-lookup"><span data-stu-id="74ef7-286">Restore data protected on Azure</span></span>
<span data-ttu-id="74ef7-287">데이터 복원은 ```RecoverableItem``` 개체와 ```RecoveryOption``` 개체의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="74ef7-288">이전 섹션에서 데이터 원본의 백업 시점 목록을 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-288">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="74ef7-289">아래 예제에서는 백업 시점과 복구 대상을 결합하여 Hyper-V 가상 컴퓨터를 Azure 백업에서 복원하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-289">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="74ef7-290">다음 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-290">This includes:</span></span>

* <span data-ttu-id="74ef7-291">[New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet을 사용하여 복구 옵션 만들기</span><span class="sxs-lookup"><span data-stu-id="74ef7-291">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="74ef7-292">```Get-DPMRecoveryPoint``` cmdlet을 사용하여 백업 시점 배열 가져오기</span><span class="sxs-lookup"><span data-stu-id="74ef7-292">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="74ef7-293">복원할 백업 시점 선택</span><span class="sxs-lookup"><span data-stu-id="74ef7-293">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="74ef7-294">명령은 모든 데이터 원본 유형에 대해 쉽게 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ef7-294">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74ef7-295">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74ef7-295">Next steps</span></span>
* <span data-ttu-id="74ef7-296">DPM에 대한 Azure 백업에 대한 자세한 정보는 [DPM 백업 소개](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="74ef7-296">For more information about Azure Backup for DPM see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
