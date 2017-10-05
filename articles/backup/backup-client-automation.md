---
title: "PowerShell을 사용하여 Azure에 Windows Server 백업 | Microsoft Docs"
description: "PowerShell을 사용하여 Azure 백업을 배포 및 관리하는 방법을 알아봅니다."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: d3f165c749af0553c4918b33b0d24cc1e21af2a9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="6a318-103">PowerShell을 사용하여 Windows Server/Windows Client용 Azure 백업 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="6a318-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6a318-104">ARM</span><span class="sxs-lookup"><span data-stu-id="6a318-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="6a318-105">클래식</span><span class="sxs-lookup"><span data-stu-id="6a318-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="6a318-106">이 문서에서는 Windows Server 또는 Windows Client에서 Azure 백업을 설정하고 백업과 복원을 관리하기 위해 PowerShell을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-106">This article shows you how to use PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="6a318-107">Azure Powershell 설치</span><span class="sxs-lookup"><span data-stu-id="6a318-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="6a318-108">이 문서에서는 리소스 그룹에서 Recovery Services 자격 증명 모음을 사용할 수 있도록 하는 ARM(Azure Resource Manager) 및 MS Online Backup PowerShell cmdlet을 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-108">This article focuses on the Azure Resource Manager (ARM) and the MS Online Backup PowerShell cmdlets that enable you to use a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="6a318-109">Azure PowerShell 1.0이 2015년 10월에 출시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="6a318-110">이 릴리스는 0.9.8 릴리스를 성공했으며 특히 cmdlet의 이름 지정 패턴에서 중요한 변경 내용이 이루어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-110">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="6a318-111">1.0 cmdlet는 명명 패턴{verb}-AzureRm{noun}을 따릅니다. 반면 0.9.8 이름은 **Rm**을 포함하지 않습니다.(예를 들어 New-AzureResourceGroup 대신 New-AzureRmResourceGroup)</span><span class="sxs-lookup"><span data-stu-id="6a318-111">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="6a318-112">반면 0.9.8 이름은 **Switch-AzureMode AzureResourceManager** 명령을 실행하여 리소스 관리자 모드를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-112">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="6a318-113">이 명령은 1.0 이상에서는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="6a318-114">1.0 이상 환경에서 0.9.8 환경을 위해 작성된 스크립트를 사용하려면 예기치 않은 영향을 방지하는 프로덕션에서 사용하기 전에 사전 프로덕션 환경에서 스크립트를 신중하게 업데이트하고 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-114">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully update and test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="6a318-115">[최신 PowerShell 릴리스를 다운로드](https://github.com/Azure/azure-powershell/releases) 합니다(필요한 최소 버전: 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="6a318-115">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="6a318-116">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="6a318-116">Create a recovery services vault</span></span>
<span data-ttu-id="6a318-117">다음 단계는 복구 서비스 자격 증명 모음을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-117">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="6a318-118">복구 서비스 자격 증명 모음은 백업 자격 증명 모음과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="6a318-119">처음으로 Azure Backup을 사용하는 경우 **Register-AzureRMResourceProvider** cmdlet을 사용하여 구독에 Azure Recovery Service 공급자를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-119">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="6a318-120">복구 서비스 자격 증명 모음은 ARM 리소스이므로 리소스 그룹 내에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-120">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="6a318-121">기존 리소스 그룹을 사용하거나 리소스 그룹을 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="6a318-122">새 리소스 그룹을 만들 때 리소스 그룹의 이름과 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-122">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="6a318-123">**New-AzureRmRecoveryServicesVault** cmdlet을 사용하여 새 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-123">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create the new vault.</span></span> <span data-ttu-id="6a318-124">리소스 그룹에 사용된 동일한 위치를 자격 증명 모음에도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-124">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="6a318-125">[LRS(로컬 중복 저장소)](../storage/common/storage-redundancy.md#locally-redundant-storage) 또는 [GRS(지역 중복 저장소)](../storage/common/storage-redundancy.md#geo-redundant-storage) 중에 사용할 저장소 중복 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-125">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="6a318-126">다음 예제는 testVault에 대한 BackupStorageRedundancy 옵션이 GeoRedundant로 설정된 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-126">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="6a318-127">많은 Azure 백업 cmdlet에는 복구 서비스 자격 증명 모음 개체가 입력으로 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-127">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="6a318-128">이런 이유 때문에, 백업 복구 서비스 자격 증명 모음 개체를 변수에 저장하는 것이 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-128">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="6a318-129">구독의 자격 증명 모음 보기</span><span class="sxs-lookup"><span data-stu-id="6a318-129">View the vaults in a subscription</span></span>
<span data-ttu-id="6a318-130">**Get-AzureRmRecoveryServicesVault** 를 사용하여 현재 구독의 모든 자격 증명 모음 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-130">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="6a318-131">이 명령을 사용하여 새 자격 증명 모음이 만들어졌는지 확인하거나 구독에서 사용할 수 있는 자격 증명 모음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-131">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="6a318-132">**Get-AzureRmRecoveryServicesVault** 명령을 실행하면 구독의 모든 자격 증명 모음이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-132">Run the command, **Get-AzureRmRecoveryServicesVault**, and all vaults in the subscription are listed.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="6a318-133">Azure 백업 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="6a318-133">Installing the Azure Backup agent</span></span>
<span data-ttu-id="6a318-134">Azure 백업 에이전트를 설치하기 전에 Windows Server에 설치 관리자를 다운로드해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-134">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="6a318-135">최신 버전의 설치 관리자는 [Microsoft 다운로드 센터](http://aka.ms/azurebackup_agent) 또는 복구 서비스의 자격 증명 모음 대시보드 페이지에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-135">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="6a318-136">쉽게 액세스할 수 있는 위치(예: *C:\Downloads\*)에 설치 관리자를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-136">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="6a318-137">또는 PowerShell을 사용하여 다운로더를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-137">Alternatively, use PowerShell to get the downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="6a318-138">에이전트를 설치하려면 승격된 PowerShell 콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-138">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="6a318-139">그러면 에이전트가 모두 기본 옵션으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-139">This installs the agent with all the default options.</span></span> <span data-ttu-id="6a318-140">설치는 백그라운드에서 몇 분 정도 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-140">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="6a318-141">*/nu* 옵션을 지정하지 않으면 설치 마지막에 **Windows 업데이트** 창이 열리고 업데이트가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-141">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="6a318-142">설치되면 설치된 프로그램 목록에 에이전트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-142">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="6a318-143">설치된 프로그램 목록을 보려면 **제어판** > **프로그램** > **프로그램 및 기능**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-143">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![에이전트 설치됨](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="6a318-145">설치 옵션</span><span class="sxs-lookup"><span data-stu-id="6a318-145">Installation options</span></span>
<span data-ttu-id="6a318-146">명령줄을 통해 사용 가능한 모든 옵션을 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-146">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="6a318-147">사용 가능한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-147">The available options include:</span></span>

| <span data-ttu-id="6a318-148">옵션</span><span class="sxs-lookup"><span data-stu-id="6a318-148">Option</span></span> | <span data-ttu-id="6a318-149">세부 정보</span><span class="sxs-lookup"><span data-stu-id="6a318-149">Details</span></span> | <span data-ttu-id="6a318-150">기본값</span><span class="sxs-lookup"><span data-stu-id="6a318-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a318-151">/q</span><span class="sxs-lookup"><span data-stu-id="6a318-151">/q</span></span> |<span data-ttu-id="6a318-152">자동 설치</span><span class="sxs-lookup"><span data-stu-id="6a318-152">Quiet installation</span></span> |- |
| <span data-ttu-id="6a318-153">/p:"위치"</span><span class="sxs-lookup"><span data-stu-id="6a318-153">/p:"location"</span></span> |<span data-ttu-id="6a318-154">Azure 백업 에이전트의 설치 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-154">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="6a318-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="6a318-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="6a318-156">/s:"위치"</span><span class="sxs-lookup"><span data-stu-id="6a318-156">/s:"location"</span></span> |<span data-ttu-id="6a318-157">Azure 백업 에이전트의 캐시 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-157">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="6a318-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="6a318-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="6a318-159">/m</span><span class="sxs-lookup"><span data-stu-id="6a318-159">/m</span></span> |<span data-ttu-id="6a318-160">Microsoft 업데이트에 옵트인</span><span class="sxs-lookup"><span data-stu-id="6a318-160">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="6a318-161">/nu</span><span class="sxs-lookup"><span data-stu-id="6a318-161">/nu</span></span> |<span data-ttu-id="6a318-162">설치가 완료된 후 업데이트에 대한 검사 안 함</span><span class="sxs-lookup"><span data-stu-id="6a318-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="6a318-163">/d</span><span class="sxs-lookup"><span data-stu-id="6a318-163">/d</span></span> |<span data-ttu-id="6a318-164">Microsoft Azure Recovery Services 에이전트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="6a318-165">/ph</span><span class="sxs-lookup"><span data-stu-id="6a318-165">/ph</span></span> |<span data-ttu-id="6a318-166">프록시 호스트 주소</span><span class="sxs-lookup"><span data-stu-id="6a318-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="6a318-167">/po</span><span class="sxs-lookup"><span data-stu-id="6a318-167">/po</span></span> |<span data-ttu-id="6a318-168">프록시 호스트 포트 번호</span><span class="sxs-lookup"><span data-stu-id="6a318-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="6a318-169">/pu</span><span class="sxs-lookup"><span data-stu-id="6a318-169">/pu</span></span> |<span data-ttu-id="6a318-170">프록시 호스트 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="6a318-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="6a318-171">/pw</span><span class="sxs-lookup"><span data-stu-id="6a318-171">/pw</span></span> |<span data-ttu-id="6a318-172">프록시 암호</span><span class="sxs-lookup"><span data-stu-id="6a318-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-to-a-recovery-services-vault"></a><span data-ttu-id="6a318-173">복구 서비스 자격 증명 모음에 Windows Server 또는 Windows 클라이언트 컴퓨터 등록</span><span class="sxs-lookup"><span data-stu-id="6a318-173">Registering Windows Server or Windows client machine to a Recovery Services Vault</span></span>
<span data-ttu-id="6a318-174">복구 서비스 자격 증명 모음을 만든 후에, 최신 에이전트 및 보관 자격 증명을 다운로드하여 편리한 위치(예: C:\Downloads)에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-174">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="6a318-175">Windows Server 또는 Windows 클라이언트 컴퓨터에서, [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet을 실행하여 컴퓨터를 자격 증명 모음에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-175">On the Windows Server or Windows client machine, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>
<span data-ttu-id="6a318-176">이 cmdlet 및 백업에 사용되는 다른 cmdlet은 Mars AgentInstaller에서 설치 과정의 일환으로 추가한 MSONLINE 모듈에서 비롯됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-176">This, and other cmdlets used for backup, are from the MSONLINE module which the Mars AgentInstaller added as part of the installation process.</span></span> 

<span data-ttu-id="6a318-177">에이전트 설치 관리자는 $Env:PSModulePath 변수를 업데이트하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-177">The Agent installer does not update the $Env:PSModulePath variable.</span></span> <span data-ttu-id="6a318-178">즉, 모듈 자동 로드에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-178">This means module auto-load fails.</span></span> <span data-ttu-id="6a318-179">이 문제를 해결하려면 다음을 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-179">To resolve this you can do the following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="6a318-180">또는 다음과 같이 스크립트에 모듈을 수동으로 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-180">Alternatively, you can manually load the module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="6a318-181">Online Backup cmdlet을 로드하면 자격 증명 모음을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-181">Once you load the Online Backup cmdlets, you register the vault credentials:</span></span>


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="6a318-182">저장소 자격 증명 파일을 지정할 때 상대 경로를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6a318-182">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="6a318-183">cmdlet 입력 내용은 반드시 절대 경로를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-183">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="6a318-184">네트워킹 서비스</span><span class="sxs-lookup"><span data-stu-id="6a318-184">Networking settings</span></span>
<span data-ttu-id="6a318-185">Windows 컴퓨터의 인터넷 연결이 프록시 서버를 통하는 경우, 프록시 설정도 에이전트에 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-185">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="6a318-186">이 예제에서는 프록시 서버가 없으므로 프록시와 관련된 모든 정보를 명시적으로 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="6a318-187">대역폭 사용 역시 주의 정해진 요일에 대해 ```work hour bandwidth``` 및 ```non-work hour bandwidth``` 옵션으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-187">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="6a318-188">프록시 및 대역폭 세부 정보 설정은 [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-188">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="6a318-189">암호화 설정</span><span class="sxs-lookup"><span data-stu-id="6a318-189">Encryption settings</span></span>
<span data-ttu-id="6a318-190">Azure 백업에 전송되는 백업 데이터는 데이터의 기밀성을 보호하기 위해 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-190">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="6a318-191">암호화 암호는 복원 시 데이터를 해독하기 위한 “암호"입니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-191">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="6a318-192">암호 정보를 설정한 후에는 안전하게 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-192">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="6a318-193">이 암호 없이는 Azure에서 데이터를 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-193">You are not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="6a318-194">파일 및 폴더 백업</span><span class="sxs-lookup"><span data-stu-id="6a318-194">Back up files and folders</span></span>
<span data-ttu-id="6a318-195">Windows 서버 및 클라이언트에서 Azure 백업으로의 모든 백업은 정책에 따라 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-195">All backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="6a318-196">정책은 세 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-196">The policy comprises three parts:</span></span>

1. <span data-ttu-id="6a318-197">백업을 수행하고 서비스와 동기화해야 할 시기를 지정하는 **백업 일정** .</span><span class="sxs-lookup"><span data-stu-id="6a318-197">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="6a318-198">Azure에 복구 지점을 보존할 기간을 지정하는 **보존 일정** 입니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-198">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="6a318-199">백업해야 할 항목을 지정하는 **파일 포함/제외 사양** .</span><span class="sxs-lookup"><span data-stu-id="6a318-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="6a318-200">이 문서에서는 백업을 자동화하기 때문에 아무것도 구성되지 않은 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="6a318-201">먼저 [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet을 사용하여 새로운 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-201">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="6a318-202">지금은 정책이 비어 있으며 포함하거나 제외시킬 항목, 백업 실행 시기 및 백업이 저장될 위치를 정의하려면 다른 cmdlet이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-202">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="6a318-203">백업 일정 구성</span><span class="sxs-lookup"><span data-stu-id="6a318-203">Configuring the backup schedule</span></span>
<span data-ttu-id="6a318-204">정책의 3부분 중 첫 번째는 백업 일정으로, [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet을 사용하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-204">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="6a318-205">백업 일정은 백업을 수행해야 할 시기를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-205">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="6a318-206">일정을 만들 때는 2개의 입력 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-206">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="6a318-207">**요일** .</span><span class="sxs-lookup"><span data-stu-id="6a318-207">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="6a318-208">백업을 하루만 실행하거나 해당 주의 모든 요일 또는 그 사이의 날짜를 조합하여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-208">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="6a318-209">**시간** .</span><span class="sxs-lookup"><span data-stu-id="6a318-209">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="6a318-210">백업이 트리거되는 시간을 최대 3개까지 서로 다르게 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-210">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="6a318-211">예를 들어, 토요일과 일요일마다 오후 4시에 실행되는 백업 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="6a318-212">백업 일정은 정책과 연결되어야 하며 이 작업은 [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-212">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="6a318-213">보존 정책 구성</span><span class="sxs-lookup"><span data-stu-id="6a318-213">Configuring a retention policy</span></span>
<span data-ttu-id="6a318-214">보존 정책은 백업 작업에서 생성된 복구 지점이 유지되는 기간을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-214">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="6a318-215">[New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet을 사용하여 새 보존 정책을 만들 때 Azure 백업을 사용하여 백업 복구 지점을 유지해야 할 일수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-215">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="6a318-216">다음 예제에서는 7일의 보존 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-216">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="6a318-217">보존 정책은 cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405)를 사용하여 기본 정책과 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-217">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="6a318-218">백업할 파일 포함 및 제외</span><span class="sxs-lookup"><span data-stu-id="6a318-218">Including and excluding files to be backed up</span></span>
<span data-ttu-id="6a318-219">```OBFileSpec``` 개체는 백업에 포함 및 제외시킬 파일을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-219">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="6a318-220">이 개체는 컴퓨터에서 보호된 파일 및 폴더를 자세히 살펴보는 규칙의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-220">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="6a318-221">필요에 따라 원하는 만큼 파일을 포함 또는 제외시키고 정책과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="6a318-222">새 OBFileSpec 개체를 만드는 경우 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="6a318-223">포함시킬 파일 및 폴더 지정</span><span class="sxs-lookup"><span data-stu-id="6a318-223">Specify the files and folders to be included</span></span>
* <span data-ttu-id="6a318-224">제외시킬 파일 및 폴더 지정</span><span class="sxs-lookup"><span data-stu-id="6a318-224">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="6a318-225">폴더의 데이터에 대한 재귀 백업을 지정하거나 지정된 폴더의 최상위 수준 파일만 백업해야 하는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-225">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="6a318-226">후자는 New-OBFileSpec 명령의 -NonRecursive 플래그를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-226">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="6a318-227">아래 예제에서는 C: 및 D: 볼륨을 백업하고 Windows 폴더 및 임시 폴더에 있는 운영 체제 바이너리를 제외시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-227">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="6a318-228">이를 수행하기 위해 [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet을 사용하여 두 개의 파일 사양을 만드는데, 하나는 포함용이고 또 하나는 제외용입니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-228">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="6a318-229">파일 사양을 만들고 나면 [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet을 사용하여 정책과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-229">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-the-policy"></a><span data-ttu-id="6a318-230">정책 적용</span><span class="sxs-lookup"><span data-stu-id="6a318-230">Applying the policy</span></span>
<span data-ttu-id="6a318-231">이제 정책 개체가 완료되었으므로 연결된 백업 일정, 보존 정책 및 파일의 포함/제외 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-231">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="6a318-232">이제는 이 정책을 Azure 백업에 커밋하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-232">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="6a318-233">새로 만든 정책을 적용하기 전에 [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet을 사용하여 서버에 연결된 기존 백업 정책이 없도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-233">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="6a318-234">정책을 제거하면 확인 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-234">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="6a318-235">확인 메시지를 건너뛰려면 ```-Confirm:$false``` 플래그를 cmdlet과 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-235">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="6a318-236">정책 개체 커밋은 [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet을 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-236">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="6a318-237">이 작업에서도 확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-237">This will also ask for confirmation.</span></span> <span data-ttu-id="6a318-238">확인 메시지를 건너뛰려면 ```-Confirm:$false``` 플래그를 cmdlet과 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-238">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want to save this backup policy ? [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

<span data-ttu-id="6a318-239">[Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet을 사용하여 기존 백업 정책에 대한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-239">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="6a318-240">백업 입정에는 [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet, 보존 정책에는 [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet을 사용하면 더욱 상세하게 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-240">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="6a318-241">임시 백업 수행</span><span class="sxs-lookup"><span data-stu-id="6a318-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="6a318-242">백업 정책이 설정되면 일정에 따라 백업이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-242">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="6a318-243">또한 [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet을 사용하여 임시 백업 트리거도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-243">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing the metadata VHD...
Data transfer is in progress. It might take longer since it is the first backup and all data needs to be transferred...
Data transfer completed and all backed up data is in the cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="6a318-244">Azure 백업에서 데이터 복원</span><span class="sxs-lookup"><span data-stu-id="6a318-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="6a318-245">이 섹션에서는 Azure 백업에서 데이터 복구를 자동화하는 방법을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-245">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="6a318-246">다음 단계를 수행하여 작업을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-246">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="6a318-247">원본 볼륨 선택</span><span class="sxs-lookup"><span data-stu-id="6a318-247">Pick the source volume</span></span>
2. <span data-ttu-id="6a318-248">복원할 백업 시점 선택</span><span class="sxs-lookup"><span data-stu-id="6a318-248">Choose a backup point to restore</span></span>
3. <span data-ttu-id="6a318-249">복원할 항목 선택</span><span class="sxs-lookup"><span data-stu-id="6a318-249">Choose an item to restore</span></span>
4. <span data-ttu-id="6a318-250">복원 프로세스 트리거</span><span class="sxs-lookup"><span data-stu-id="6a318-250">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="6a318-251">원본 볼륨 선택</span><span class="sxs-lookup"><span data-stu-id="6a318-251">Picking the source volume</span></span>
<span data-ttu-id="6a318-252">Azure 백업에서 항목을 복원하려면 먼저 항목의 원본을 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-252">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="6a318-253">Windows 서버 또는 Windows 클라이언트의 컨텍스트에서 명령을 실행 중이므로 컴퓨터는 이미 식별된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-253">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="6a318-254">원본을 식별하는 다음 단계는 해당 원본이 포함된 볼륨을 식별하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-254">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="6a318-255">이 컴퓨터에서 백업 중인 볼륨 또는 원본 목록은 [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet을 실행하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-255">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="6a318-256">이 명령은 이 서버/클라이언트에서 백업한 모든 원본의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-256">This command returns an array of all the sources backed up from this server/client.</span></span>

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-to-restore"></a><span data-ttu-id="6a318-257">복원할 백업 시점 선택</span><span class="sxs-lookup"><span data-stu-id="6a318-257">Choosing a backup point from which to restore</span></span>
<span data-ttu-id="6a318-258">[Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet을 적절한 매개 변수와 함께 실행하여 백업 시점 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-258">You retreive a list of backup points by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="6a318-259">이 예제에서는 원본 볼륨 *D:* 의 최신 백업 시점을 선택하고 이 시점을 사용하여 특정 파일을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-259">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
<span data-ttu-id="6a318-260">개체 ```$rps``` 는 백업 시점의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-260">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="6a318-261">첫 번째 요소는 가장 최근 시점이고 n 번째 요소는 가장 오래된 시점입니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-261">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="6a318-262">최근 시점을 선택하려면 ```$rps[0]```을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-262">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="6a318-263">복원할 항목 선택</span><span class="sxs-lookup"><span data-stu-id="6a318-263">Choosing an item to restore</span></span>
<span data-ttu-id="6a318-264">복원할 정확한 파일 또는 폴더를 식별하려면 [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet을 재귀적으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-264">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="6a318-265">이런 방식으로 ```Get-OBRecoverableItem```만 사용하여 폴더 계층 구조를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-265">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="6a318-266">이 예제에서는 *finances.xls* 파일을 복원하려는 경우 개체 ```$filesFolders[1]```을 사용하여 해당 파일을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-266">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

<span data-ttu-id="6a318-267">```Get-OBRecoverableItem``` cmdlet을 사용하여 복원할 항목을 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-267">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="6a318-268">이 예제에서 *finances.xls* 를 검색하려면 다음 명령을 실행하여 파일에 대한 핸들을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-268">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="6a318-269">복원 프로세스 트리거</span><span class="sxs-lookup"><span data-stu-id="6a318-269">Triggering the restore process</span></span>
<span data-ttu-id="6a318-270">복원 프로세스를 트리거하려면 먼저 복구 옵션을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-270">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="6a318-271">이 작업은 [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-271">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="6a318-272">이 예에서는 파일을 *C:\temp*로 복원한다고 가정해 보겠습니다. 또한 대상 폴더 *C:\temp*에 이미 존재하는 파일은 건너뛴다고 가정해 보겠습니다. 해당 복구 옵션을 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-272">For this example, let's assume that we want to restore the files to *C:\temp*. Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*. To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="6a318-273">이제 ```Get-OBRecoverableItem``` cmdlet의 출력에서 선택한 ```$item```에 대해 [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) 명령을 사용하여 복원 프로세스를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-273">Now trigger the restore process by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="6a318-274">Azure 백업 에이전트 제거</span><span class="sxs-lookup"><span data-stu-id="6a318-274">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="6a318-275">Azure 백업 에이전트 제거는 다음 명령을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-275">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="6a318-276">컴퓨터에서 에이전트 이진 파일을 제거하면 고려해야 할 몇 가지 결과가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-276">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="6a318-277">컴퓨터에서 파일 필터를 제거하고 변경 내용 추적이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-277">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="6a318-278">모든 정책 정보가 컴퓨터에서 제거되지만 정책 정보는 서비스에 계속 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-278">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="6a318-279">모든 백업 일정이 제거되고 더 이상 백업이 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="6a318-280">하지만 Azure에 저장된 데이터는 그대로 유지되며 사용자가 설정한 보존 정책에 따라 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-280">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="6a318-281">이전 지점은 시간이 경과하면 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="6a318-282">원격 관리</span><span class="sxs-lookup"><span data-stu-id="6a318-282">Remote management</span></span>
<span data-ttu-id="6a318-283">Azure 백업 에이전트, 정책, 데이터 원본과 관련된 모든 관리는 PowerShell을 통해 원격으로 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-283">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="6a318-284">원격으로 관리될 컴퓨터는 올바르게 준비되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-284">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="6a318-285">기본적으로 WinRM 서비스는 수동 시작으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-285">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="6a318-286">시작 유형은 반드시 *자동* 으로 설정되어야 하며 서비스가 시작되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-286">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="6a318-287">WinRM 서비스가 실행되는지 확인하도록 Status 속성의 값은 *Running*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-287">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="6a318-288">PowerShell을 원격 작업용으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="6a318-289">이제 에이전트 설치부터 시작하여 컴퓨터를 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-289">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="6a318-290">예를 들어, 다음 스크립트는 에이전트를 원격 컴퓨터로 복사하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6a318-290">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="6a318-291">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6a318-291">Next steps</span></span>
<span data-ttu-id="6a318-292">Windows Server/Client용 Azure 백업에 대한 자세한 정보는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a318-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="6a318-293">Azure 백업 소개</span><span class="sxs-lookup"><span data-stu-id="6a318-293">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="6a318-294">Windows 서버 백업</span><span class="sxs-lookup"><span data-stu-id="6a318-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
