---
title: "Azure에서 aaaUse PowerShell toomanage Windows Server 백업을 | Microsoft Docs"
description: "PowerShell을 사용하여 Windows Server 백업을 배포하고 관리합니다."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="9dafa-103">배포 하 고 PowerShell을 사용 하 여 Windows Server/Windows 클라이언트에 대 한 백업 tooAzure 관리</span><span class="sxs-lookup"><span data-stu-id="9dafa-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9dafa-104">ARM</span><span class="sxs-lookup"><span data-stu-id="9dafa-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="9dafa-105">클래식</span><span class="sxs-lookup"><span data-stu-id="9dafa-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="9dafa-106">이 문서에서는 Windows Server 또는 Windows 워크스테이션 데이터 tooa toouse PowerShell tooback 자격 증명 모음을 백업 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-106">This article explains how toouse PowerShell tooback up Windows Server or Windows workstation data tooa backup vault.</span></span> <span data-ttu-id="9dafa-107">모든 새 배포에 Recovery Services 자격 증명 모음을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="9dafa-108">새 Azure 백업을 사용 하는 구독에서 백업 자격 증명 모음을 만들지 않은 경우 사용 하 여 hello 문서 [배포 및 PowerShell을 사용 하 여 Data Protection Manager 데이터 tooAzure 관리](backup-client-automation.md) 복구 서비스 자격 증명 모음에 데이터를 저장 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9dafa-109">이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="9dafa-110">자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="9dafa-111">Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="9dafa-112">2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="9dafa-113">**2017년 11월 1일까지**:</span><span class="sxs-lookup"><span data-stu-id="9dafa-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="9dafa-114">모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="9dafa-115">하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="9dafa-116">대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="9dafa-117">Azure Powershell 설치</span><span class="sxs-lookup"><span data-stu-id="9dafa-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="9dafa-118">Azure PowerShell 1.0이 2015년 10월에 출시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="9dafa-119">이 릴리스에서 hello 0.9.8 릴리스 성공 못하고 hello hello cmdlet의 이름 지정 패턴의 특히 몇 가지 주요 변경 사항에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-119">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="9dafa-120">1.0 cmdlet에 따라 hello 명명 패턴 {동사}-{명사}; AzureRm 반면 hello 0.9.8 이름 포함 되지 않습니다 **Rm** (예를 들어 새로 만들기-AzureRmResourceGroup 새로 AzureResourceGroup 대신).</span><span class="sxs-lookup"><span data-stu-id="9dafa-120">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="9dafa-121">Hello를 실행 하 여 hello Resource Manager 모드를 먼저 활성화 해야 Azure PowerShell 0.9.8을 사용할 경우 **Switch-azuremode AzureResourceManager** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-121">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="9dafa-122">이 명령은 1.0 이상에서는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="9dafa-123">Toouse hello 1.0 또는 이상 환경에서 hello 0.9.8 환경 용으로 작성 된 스크립트를 원하는 경우 신중 하 게 테스트 해야 hello 스크립트 사전 프로덕션 환경에서 프로덕션 tooavoid에 사용 하기 전에 예기치 않은 영향입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-123">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="9dafa-124">[Hello 최신 PowerShell 릴리스의 다운로드](https://github.com/Azure/azure-powershell/releases) (필요한 최소 버전은: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="9dafa-124">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="9dafa-125">백업 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="9dafa-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="9dafa-126">처음으로 hello에 대 한 Azure 백업을 사용 하는 고객에 대 한 tooregister hello Azure 백업 공급자 toobe 구독 함께 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-126">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="9dafa-127">Hello 다음 명령을 실행 하 여이 작업을 수행할 수 있습니다: 레지스터 AzureProvider-ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="9dafa-127">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="9dafa-128">Hello를 사용 하 여 새 백업 모음을 만들 수 있습니다 **새로 AzureRMBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-128">You can create a new backup vault using hello **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="9dafa-129">hello 백업 자격 증명 모음은 ARM 리소스로 tooplace 있으므로 리소스 그룹 내에서.</span><span class="sxs-lookup"><span data-stu-id="9dafa-129">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="9dafa-130">관리자 권한 Azure PowerShell 콘솔 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-130">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="9dafa-131">사용 하 여 hello **Get AzureRMBackupVault** cmdlet toolist hello 백업 구독에 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-131">Use hello **Get-AzureRMBackupVault** cmdlet toolist hello backup vaults in a subscription.</span></span>

## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="9dafa-132">Hello Azure 백업 에이전트를 설치</span><span class="sxs-lookup"><span data-stu-id="9dafa-132">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="9dafa-133">Hello Azure 백업 에이전트를 설치 하기 전에 다운로드 하 여 Windows 서버 hello에 toohave hello installer가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-133">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="9dafa-134">Hello에서 hello hello installer의 최신 버전을 얻을 수 있습니다 [Microsoft 다운로드 센터](http://aka.ms/azurebackup_agent) 또는 hello 백업 자격 증명 대시보드 페이지에서.</span><span class="sxs-lookup"><span data-stu-id="9dafa-134">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="9dafa-135">Hello 설치 관리자와 같은 tooan 쉽게 액세스할 수 있는 위치를 저장 * C:\Downloads\*합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-135">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="9dafa-136">다음 명령을 관리자 권한 PowerShell 콘솔 hello 실행 tooinstall hello 에이전트:</span><span class="sxs-lookup"><span data-stu-id="9dafa-136">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="9dafa-137">이 모든 hello 기본 옵션으로 hello 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-137">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="9dafa-138">hello 설치 hello 백그라운드에서 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-138">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="9dafa-139">Hello를 지정 하지 않으면 */nu* 옵션 다음 hello **Windows Update** 모든 업데이트에 대 한 hello 설치 toocheck hello 끝나기 전에 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-139">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="9dafa-140">설치 되 면 hello 에이전트 hello 설치 된 프로그램 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-140">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="9dafa-141">설치 된 프로그램 toosee hello 목록이, 너무 이동**제어판** > **프로그램** > **프로그램 및 기능**합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-141">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![에이전트 설치됨](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="9dafa-143">설치 옵션</span><span class="sxs-lookup"><span data-stu-id="9dafa-143">Installation options</span></span>
<span data-ttu-id="9dafa-144">통해 사용할 수 있는 옵션을 hello 모든 toosee 명령줄 hello, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="9dafa-144">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="9dafa-145">hello 사용할 수 있는 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-145">hello available options include:</span></span>

| <span data-ttu-id="9dafa-146">옵션</span><span class="sxs-lookup"><span data-stu-id="9dafa-146">Option</span></span> | <span data-ttu-id="9dafa-147">세부 정보</span><span class="sxs-lookup"><span data-stu-id="9dafa-147">Details</span></span> | <span data-ttu-id="9dafa-148">기본값</span><span class="sxs-lookup"><span data-stu-id="9dafa-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9dafa-149">/q</span><span class="sxs-lookup"><span data-stu-id="9dafa-149">/q</span></span> |<span data-ttu-id="9dafa-150">자동 설치</span><span class="sxs-lookup"><span data-stu-id="9dafa-150">Quiet installation</span></span> |- |
| <span data-ttu-id="9dafa-151">/p:"위치"</span><span class="sxs-lookup"><span data-stu-id="9dafa-151">/p:"location"</span></span> |<span data-ttu-id="9dafa-152">Hello Azure 백업 에이전트에 대 한 toohello 설치 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-152">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="9dafa-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="9dafa-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="9dafa-154">/s:"위치"</span><span class="sxs-lookup"><span data-stu-id="9dafa-154">/s:"location"</span></span> |<span data-ttu-id="9dafa-155">Hello Azure 백업 에이전트에 대 한 toohello 캐시 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-155">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="9dafa-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="9dafa-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="9dafa-157">/m</span><span class="sxs-lookup"><span data-stu-id="9dafa-157">/m</span></span> |<span data-ttu-id="9dafa-158">옵트인 tooMicrosoft 업데이트</span><span class="sxs-lookup"><span data-stu-id="9dafa-158">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="9dafa-159">/nu</span><span class="sxs-lookup"><span data-stu-id="9dafa-159">/nu</span></span> |<span data-ttu-id="9dafa-160">설치가 완료된 후 업데이트에 대한 검사 안 함</span><span class="sxs-lookup"><span data-stu-id="9dafa-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="9dafa-161">/d</span><span class="sxs-lookup"><span data-stu-id="9dafa-161">/d</span></span> |<span data-ttu-id="9dafa-162">Microsoft Azure Recovery Services 에이전트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="9dafa-163">/ph</span><span class="sxs-lookup"><span data-stu-id="9dafa-163">/ph</span></span> |<span data-ttu-id="9dafa-164">프록시 호스트 주소</span><span class="sxs-lookup"><span data-stu-id="9dafa-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="9dafa-165">/po</span><span class="sxs-lookup"><span data-stu-id="9dafa-165">/po</span></span> |<span data-ttu-id="9dafa-166">프록시 호스트 포트 번호</span><span class="sxs-lookup"><span data-stu-id="9dafa-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="9dafa-167">/pu</span><span class="sxs-lookup"><span data-stu-id="9dafa-167">/pu</span></span> |<span data-ttu-id="9dafa-168">프록시 호스트 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="9dafa-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="9dafa-169">/pw</span><span class="sxs-lookup"><span data-stu-id="9dafa-169">/pw</span></span> |<span data-ttu-id="9dafa-170">프록시 암호</span><span class="sxs-lookup"><span data-stu-id="9dafa-170">Proxy Password</span></span> |- |

## <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="9dafa-171">Hello Azure 백업 서비스 등록</span><span class="sxs-lookup"><span data-stu-id="9dafa-171">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="9dafa-172">Hello Azure 백업 서비스를 등록 하려면 먼저 tooensure 해당 hello [필수 구성 요소](backup-configure-vault.md) 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-172">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="9dafa-173">다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-173">You must:</span></span>

* <span data-ttu-id="9dafa-174">유효한 Azure 구독이 있어야 함</span><span class="sxs-lookup"><span data-stu-id="9dafa-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="9dafa-175">백업 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="9dafa-175">Have a backup vault</span></span>

<span data-ttu-id="9dafa-176">toodownload hello 자격 증명 모음 자격 증명을 hello 실행 **Get AzureRMBackupVaultCredentials** cmdlet 같은 편리한 위치에는 Azure PowerShell 콘솔 및 저장소에 * C:\Downloads\*합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-176">toodownload hello vault credentials, run hello **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="9dafa-177">Hello 자격 증명 모음 등록 hello 컴퓨터 이루어진다는 hello를 사용 하 여 [Start-obregistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9dafa-177">Registering hello machine with hello vault is done using hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="9dafa-178">상대 경로 toospecify hello 자격 증명 모음 자격 증명 파일을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="9dafa-178">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="9dafa-179">입력된 toohello cmdlet으로는 절대 경로 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-179">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="9dafa-180">네트워킹 서비스</span><span class="sxs-lookup"><span data-stu-id="9dafa-180">Networking settings</span></span>
<span data-ttu-id="9dafa-181">Hello의 hello 연결 Windows 컴퓨터 인터넷 프록시 서버를 통해은 toohello을 때 hello 프록시 설정은 제공할 수도 있습니다 toohello 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-181">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="9dafa-182">이 예제에서는 프록시 서버가 없으므로 프록시와 관련된 모든 정보를 명시적으로 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="9dafa-183">Hello 옵션의 대역폭 사용량을 제어할 수도 있습니다 ```work hour bandwidth``` 및 ```non-work hour bandwidth``` hello 주 중 일의 특정된 집합에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-183">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="9dafa-184">Hello 프록시 및 대역폭 세부 정보를 설정 이루어진다는 hello를 사용 하 여 [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9dafa-184">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="9dafa-185">암호화 설정</span><span class="sxs-lookup"><span data-stu-id="9dafa-185">Encryption settings</span></span>
<span data-ttu-id="9dafa-186">hello 전송 되는 백업 데이터 tooAzure 백업 hello 데이터의 암호화 된 tooprotect hello 기밀입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-186">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="9dafa-187">hello 암호화의 암호는 복원의 hello 시 hello "password" toodecrypt hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-187">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="9dafa-188">설정 되 면 hello 암호 정보를 안전 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-188">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="9dafa-189">이 암호 없이 Azure에서 수 toorestore 데이터 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-189">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="9dafa-190">파일 및 폴더 백업</span><span class="sxs-lookup"><span data-stu-id="9dafa-190">Back up files and folders</span></span>
<span data-ttu-id="9dafa-191">Windows 서버 및 클라이언트 tooAzure 백업에서에서 모든 백업 정책에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-191">All your backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="9dafa-192">hello 정책에는 세 부분으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-192">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="9dafa-193">A **백업 일정** 백업을 toobe 가져오고 hello 서비스와 동기화 해야 하는 경우를 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-193">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="9dafa-194">A **보존 일정** Azure tooretain hello 복구 지점 기간을 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-194">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="9dafa-195">백업해야 할 항목을 지정하는 **파일 포함/제외 사양** .</span><span class="sxs-lookup"><span data-stu-id="9dafa-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="9dafa-196">이 문서에서는 백업을 자동화하기 때문에 아무것도 구성되지 않은 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="9dafa-197">사용 하 여 hello를 사용 하 여 새 백업 정책을 만드는 [New-obpolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet를 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-197">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="9dafa-198">이 시간 hello에서 정책 비어 있고 다른 cmdlet은 필요한 toodefine 포함 되거나 제외 될 항목, 백업이 저장 될 때 백업을 실행 하 고 여기서 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-198">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="9dafa-199">Hello 백업 일정 구성</span><span class="sxs-lookup"><span data-stu-id="9dafa-199">Configuring hello backup schedule</span></span>
<span data-ttu-id="9dafa-200">먼저 hello hello 정책 3 부분이 hello를 사용 하 여 생성 된 백업 일정을 hello [새로 OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-200">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="9dafa-201">백업 일정 hello 백업을 toobe 수행 해야 하는 경우를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-201">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="9dafa-202">일정을 만들 때 2 toospecify 입력된 매개 변수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-202">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="9dafa-203">**Hello 주 중 일** 해당 hello 백업을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-203">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="9dafa-204">Hello만 1 일에서 백업 작업 또는 hello 주 매일 또는 조합을 사이 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-204">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="9dafa-205">**Hello 하루 중 시간** hello 백업 실행 시기입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-205">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="9dafa-206">Too3 시간 hello hello 백업 트리거될 수는 때를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-206">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="9dafa-207">예를 들어, 토요일과 일요일마다 오후 4시에 실행되는 백업 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="9dafa-208">hello 백업 일정을 정책에 연결 된 toobe 되어야 하며 hello를 사용 하 여 이렇게 할 [Set-obschedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-208">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="9dafa-209">보존 정책 구성</span><span class="sxs-lookup"><span data-stu-id="9dafa-209">Configuring a retention policy</span></span>
<span data-ttu-id="9dafa-210">hello 보존 정책은 백업 작업에서 생성 된 지점을 유지 되는 시간 복구를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-210">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="9dafa-211">Hello를 사용 하 여 새 보존 정책을 만들 때 [새로 OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet hello 일 수를 백업 복구 지점을 hello 필요 toobe를 Azure 백업 보존을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-211">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="9dafa-212">다음 예제에서는 hello 보존 정책을 7 일로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-212">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="9dafa-213">hello 보존 정책을 연결 해야 hello cmdlet을 사용 하는 hello 주 정책과 [집합 OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="9dafa-213">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="9dafa-214">포함 및 제외 toobe 파일 백업</span><span class="sxs-lookup"><span data-stu-id="9dafa-214">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="9dafa-215">```OBFileSpec``` hello 파일 toobe 포함 되거나 백업에서 제외 개체를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-215">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="9dafa-216">Hello 아웃 범위는 컴퓨터의 파일 및 폴더 보호 하는 규칙의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-216">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="9dafa-217">필요에 따라 원하는 만큼 파일을 포함 또는 제외시키고 정책과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="9dafa-218">새 OBFileSpec 개체를 만드는 경우 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="9dafa-219">포함 된 hello 파일 및 폴더 toobe 지정</span><span class="sxs-lookup"><span data-stu-id="9dafa-219">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="9dafa-220">Hello 파일 및 폴더 toobe 제외를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-220">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="9dafa-221">재귀 백업 데이터 폴더 (또는) hello 최상위에 있는 파일만 hello 지정 된 폴더를 백업 해야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-221">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="9dafa-222">후자의 hello hello New-obfilespec 명령 hello-비재귀 플래그를 사용 하 여 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-222">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="9dafa-223">Hello 아래의 예제에서는 c: 및 d: 볼륨을 백업 알아보고 hello OS 바이너리 hello Windows 폴더 및 임시 폴더에 제외 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-223">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="9dafa-224">hello를 사용 하 여 두 파일 사양 만들겠습니다 하므로 toodo [New-obfilespec](https://technet.microsoft.com/library/hh770408) cmdlet-포함 및 제외 하나에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-224">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="9dafa-225">Hello를 사용 하 여 hello 정책과 연결 된 자신이 hello 파일 지정을 만든 후 [Add-obfilespec](https://technet.microsoft.com/library/hh770424) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-225">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="9dafa-226">Hello 정책 적용</span><span class="sxs-lookup"><span data-stu-id="9dafa-226">Applying hello policy</span></span>
<span data-ttu-id="9dafa-227">이제 hello 정책 개체가 완료 되 고 연결된 된 백업 일정, 보존 정책 및은 파일 포함/제외 목록.</span><span class="sxs-lookup"><span data-stu-id="9dafa-227">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="9dafa-228">이 정책은 이제 toouse Azure 백업에 대 한 커밋할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-228">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="9dafa-229">새로 만든 hello를 적용 하기 전에 정책을 확인 hello를 사용 하 여 hello 서버와 관련 된 기존 백업 정책이 없으면 [제거 OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-229">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="9dafa-230">Hello 정책 제거 하는 확인 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-230">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="9dafa-231">tooskip hello 확인 hello를 사용 하 여 ```-Confirm:$false``` hello cmdlet과 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-231">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="9dafa-232">커밋 hello 정책 개체 이루어집니다 hello를 사용 하 여 [Set-obpolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-232">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="9dafa-233">이 작업에서도 확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-233">This will also ask for confirmation.</span></span> <span data-ttu-id="9dafa-234">tooskip hello 확인 hello를 사용 하 여 ```-Confirm:$false``` hello cmdlet과 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-234">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
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

<span data-ttu-id="9dafa-235">Hello hello를 사용 하 여 hello 기존 백업 정책 세부 정보를 볼 수 있습니다 [Get-obpolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-235">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="9dafa-236">있습니다 수 드릴 다운 hello를 사용 하 여 자세히 [Get OBSchedule](https://technet.microsoft.com/library/hh770423) hello 백업 일정 및 hello에 대 한 cmdlet [Get OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) hello 보존 정책에 대 한 cmdlet</span><span class="sxs-lookup"><span data-stu-id="9dafa-236">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="9dafa-237">임시 백업 수행</span><span class="sxs-lookup"><span data-stu-id="9dafa-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="9dafa-238">백업 정책을 설정 되 면 hello 백업을 hello 일정에 따라 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-238">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="9dafa-239">임시 백업을 트리거하는 hello를 사용 하 여 가능한도 [시작 OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9dafa-239">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="9dafa-240">Azure 백업에서 데이터 복원</span><span class="sxs-lookup"><span data-stu-id="9dafa-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="9dafa-241">이 섹션에서는 Azure 백업에서 데이터의 복구 자동화에 대 한 hello 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-241">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="9dafa-242">이렇게 하면 hello를 단계를 수행 하므로 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-242">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="9dafa-243">Hello 원본 볼륨 선택</span><span class="sxs-lookup"><span data-stu-id="9dafa-243">Pick hello source volume</span></span>
2. <span data-ttu-id="9dafa-244">백업 지점 toorestore 선택</span><span class="sxs-lookup"><span data-stu-id="9dafa-244">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="9dafa-245">항목 toorestore 선택</span><span class="sxs-lookup"><span data-stu-id="9dafa-245">Choose an item toorestore</span></span>
4. <span data-ttu-id="9dafa-246">트리거 hello 복원 프로세스</span><span class="sxs-lookup"><span data-stu-id="9dafa-246">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="9dafa-247">Hello 원본 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-247">Picking hello source volume</span></span>
<span data-ttu-id="9dafa-248">순서 toorestore Azure 백업에서 항목에에서는 먼저 hello 항목의 tooidentify hello 원본이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-248">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="9dafa-249">Windows Server 또는 Windows 클라이언트의 hello 컨텍스트에서 hello 명령을 실행 하는 것, 이후 hello 컴퓨터는 이미 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-249">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="9dafa-250">hello 소스를 식별 hello 다음 단계에는 포함 하는 tooidentify hello 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-250">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="9dafa-251">Hello를 실행 하 여 검색할 수 있습니다이 컴퓨터에서 백업 중인 볼륨 또는 원본 목록 [Get-obrecoverablesource](https://technet.microsoft.com/library/hh770410) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-251">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="9dafa-252">이 명령은이 서버/클라이언트에서 백업 하는 모든 hello 원본의 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-252">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-toorestore"></a><span data-ttu-id="9dafa-253">백업 지점 toorestore 선택</span><span class="sxs-lookup"><span data-stu-id="9dafa-253">Choosing a backup point toorestore</span></span>
<span data-ttu-id="9dafa-254">hello 백업 지점 목록을 검색할 수 hello를 실행 하 여 [Get-obrecoverableitem](https://technet.microsoft.com/library/hh770399.aspx) 적절 한 매개 변수를 사용 하 여 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-254">hello list of backup points can be retrieved by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="9dafa-255">예에서 hello hello 원본 볼륨에 대 한 최신 백업 지점을 선택 합니다 *d:* toorecover 특정 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-255">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="9dafa-256">hello 개체 ```$rps``` 배열 백업 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-256">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="9dafa-257">첫 번째 요소가 hello hello 최신 시점 고 hello n 번째 요소는 hello 가장 오래 된 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-257">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="9dafa-258">toochoose hello 최신 지점을 사용 하 여 ```$rps[0]```합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-258">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="9dafa-259">항목 toorestore 선택</span><span class="sxs-lookup"><span data-stu-id="9dafa-259">Choosing an item toorestore</span></span>
<span data-ttu-id="9dafa-260">재귀적으로 hello를 사용 하 여 tooidentify hello 정확한 파일 또는 폴더 toorestore [Get-obrecoverableitem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-260">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="9dafa-261">전적으로 hello를 사용 하 여 해당 방식으로 hello 폴더 계층 구조를 찾아볼 수 ```Get-OBRecoverableItem```합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-261">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="9dafa-262">이 예제에서는 toorestore hello 파일 원하는 *finances.xls* 사용 하는 것을 참조할 수 있습니다 hello 개체 ```$filesFolders[1]```합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-262">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="9dafa-263">항목 toorestore hello를 사용 하 여 검색할 수 있습니다 ```Get-OBRecoverableItem``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-263">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="9dafa-264">예제에 대 한 toosearch *finances.xls* 이 명령을 실행 하 여 hello 파일에 대 한 핸들 신속:</span><span class="sxs-lookup"><span data-stu-id="9dafa-264">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="9dafa-265">트리거 hello 복원 프로세스</span><span class="sxs-lookup"><span data-stu-id="9dafa-265">Triggering hello restore process</span></span>
<span data-ttu-id="9dafa-266">tootrigger hello 복원 프로세스를 먼저 필요 toospecify hello 복구 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-266">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="9dafa-267">Hello를 사용 하 여이 작업을 수행할 수 있습니다 [새로 OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dafa-267">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="9dafa-268">이 예에서는 가정 한다고 toorestore hello 파일 너무*C:\temp*합니다. 또한 가정해 hello 대상 폴더에 이미 있는 tooskip 파일 한다고 *C:\temp*. toocreate 같은 복구 옵션을 사용 하 여 다음 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="9dafa-268">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="9dafa-269">이제 hello를 사용 하 여 복원을 트리거하 [Start-obrecovery](https://technet.microsoft.com/library/hh770402.aspx) hello 선택한 명령을 ```$item``` hello의 hello 출력에서 ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9dafa-269">Now trigger restore by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="9dafa-270">Hello Azure 백업 에이전트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-270">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="9dafa-271">다음 명령을 hello를 사용 하 여 hello Azure 백업 에이전트 제거를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-271">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="9dafa-272">Hello 컴퓨터에서 제거 하는 hello 에이전트 이진 파일에 일부 결과 tooconsider가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-272">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="9dafa-273">Hello 컴퓨터에서 hello 파일 필터를 제거 하 고 변경 내용 추적 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-273">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="9dafa-274">Hello 컴퓨터에서 정책 정보를 모두 없어지지만 hello 정책 정보가 hello 서비스에 저장 된 toobe 계속 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-274">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="9dafa-275">모든 백업 일정이 제거되고 더 이상 백업이 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-275">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="9dafa-276">그러나 hello 데이터는 Azure 유지에 저장 하 고 hello 보존 정책 설정에 따라 사용자가 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-276">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="9dafa-277">이전 지점은 시간이 경과하면 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-277">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="9dafa-278">원격 관리</span><span class="sxs-lookup"><span data-stu-id="9dafa-278">Remote management</span></span>
<span data-ttu-id="9dafa-279">Hello Azure 백업 에이전트, 정책 및 데이터 원본 주위의 모든 hello 관리는 PowerShell을 통해 원격으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-279">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="9dafa-280">원격으로 관리 되는 hello 컴퓨터에 제대로 준비 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-280">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="9dafa-281">기본적으로 hello WinRM 서비스를 수동으로 시작 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-281">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="9dafa-282">hello 시작 유형을 너무 설정 해야*자동* hello service를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-282">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="9dafa-283">WinRM 서비스가 hello tooverify 실행 되 고, hello hello Status 속성 값 있어야 *실행*합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-283">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="9dafa-284">PowerShell을 원격 작업용으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-284">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="9dafa-285">hello 컴퓨터 수 이제 원격으로 관리할 수-hello 설치 된 hello 에이전트를에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-285">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="9dafa-286">예를 들어 다음 스크립트는 hello hello 에이전트 toohello 원격 컴퓨터를 복사 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dafa-286">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="9dafa-287">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9dafa-287">Next steps</span></span>
<span data-ttu-id="9dafa-288">Windows Server/Client용 Azure 백업에 대한 자세한 정보는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9dafa-288">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="9dafa-289">소개 tooAzure 백업</span><span class="sxs-lookup"><span data-stu-id="9dafa-289">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="9dafa-290">Windows 서버 백업</span><span class="sxs-lookup"><span data-stu-id="9dafa-290">Back up Windows Servers</span></span>](backup-configure-vault.md)
