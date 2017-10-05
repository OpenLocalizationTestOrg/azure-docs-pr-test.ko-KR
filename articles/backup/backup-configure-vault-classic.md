---
title: "Azure(클래식 모델)에 Windows Server 또는 워크스테이션 백업 | Microsoft Docs"
description: "Azure에서 백업 자격 증명 모음에 Windows Server 또는 클라이언트를 백업합니다. Azure Backup 에이전트를 사용하여 백업 자격 증명 모음에 대한 파일 및 폴더를 보호하는 기본 사항을 알아봅니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "백업 자격 증명 모음, Windows 서버 백업, Windows 백업"
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: a8daa6a4655b72936b6299c0fa5b80459ffa5da3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="back-up-a-windows-server-or-workstation-to-azure-using-the-classic-portal"></a><span data-ttu-id="3c110-105">클래식 포털을 사용하여 Azure에 Windows Server 또는 워크스테이션 백업</span><span class="sxs-lookup"><span data-stu-id="3c110-105">Back up a Windows server or workstation to Azure using the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c110-106">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="3c110-106">Classic portal</span></span>](backup-configure-vault-classic.md)
> * [<span data-ttu-id="3c110-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="3c110-107">Azure portal</span></span>](backup-configure-vault.md)
>
>

<span data-ttu-id="3c110-108">이 문서에서는 환경을 준비하고 Windows Server(또는 워크스테이션)를 Azure에 백업하기 위해 따라야 할 절차를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-108">This article covers the procedures that you need to follow to prepare your environment and back up a Windows server (or workstation) to Azure.</span></span> <span data-ttu-id="3c110-109">또한 백업 솔루션 배포 시 고려 사항에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-109">It also covers considerations for deploying your backup solution.</span></span> <span data-ttu-id="3c110-110">Azure 백업을 처음으로 시도하려는 경우 이 문서를 보면 해당 프로세스에 대한 간단한 지침을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-110">If you're interested in trying Azure Backup for the first time, this article quickly walks you through the process.</span></span>

<span data-ttu-id="3c110-111">Azure는 리소스를 만들고 작업하기 위한 두 가지 배포 모델로 리소스 관리자와 클래식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-111">Azure has two different deployment models for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="3c110-112">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-112">This article covers using the classic deployment model.</span></span> <span data-ttu-id="3c110-113">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-113">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="3c110-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="3c110-114">Before you start</span></span>
<span data-ttu-id="3c110-115">서버 또는 클라이언트를 Azure에 백업하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-115">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="3c110-116">계정이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/free/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-116">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-backup-vault"></a><span data-ttu-id="3c110-117">백업 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="3c110-117">Create a backup vault</span></span>
<span data-ttu-id="3c110-118">서버 또는 클라이언트의 파일과 폴더를 백업하려면 데이터를 저장하려는 지역에 백업 자격 증명 모음을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-118">To back up files and folders from a server or client, you need to create a backup vault in the geographic region where you want to store the data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c110-119">2017년 3월부터는 백업 자격 증명 모음을 만드는 데 더 이상 클래식 포털을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-119">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
>
> <span data-ttu-id="3c110-120">이제 Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-120">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="3c110-121">자세한 내용은 [Recovery Services 자격 증명 모음으로 Backup 자격 증명 모음 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c110-121">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="3c110-122">Backup 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-122">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="3c110-123">**2017년 10월 15일**부터는 PowerShell을 사용하여 Backup 자격 증명 모음을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-123">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="3c110-124">**2017년 11월 1일 시작**:</span><span class="sxs-lookup"><span data-stu-id="3c110-124">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="3c110-125">나머지 모든 Backup 자격 증명 모음은 자동으로 Recovery Services 자격 증명 모음으로 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-125">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="3c110-126">클래식 포털에서는 백업 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-126">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="3c110-127">대신 Azure Portal을 사용하여 Recovery Services 자격 증명 모음에서 백업 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-127">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>


## <a name="download-the-vault-credential-file"></a><span data-ttu-id="3c110-128">자격 증명 모음 자격 증명 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="3c110-128">Download the vault credential file</span></span>
<span data-ttu-id="3c110-129">온-프레미스 컴퓨터는 백업 자격 증명 모음을 인증해야 Azure에 데이터를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-129">The on-premises machine needs to be authenticated with a backup vault before it can back up data to Azure.</span></span> <span data-ttu-id="3c110-130">인증은 *보관 자격 증명*을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-130">The authentication is achieved through *vault credentials*.</span></span> <span data-ttu-id="3c110-131">보관 자격 증명 파일은 클래식 포털에서 보안 채널을 통해 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-131">The vault credential file is downloaded through a secure channel from the classic portal.</span></span> <span data-ttu-id="3c110-132">인증서 개인 키는 포털 또는 서비스에 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-132">The certificate private key does not persist in the portal or the service.</span></span>

### <a name="to-download-the-vault-credential-file-to-a-local-machine"></a><span data-ttu-id="3c110-133">로컬 컴퓨터에 자격 증명 모음 자격 증명 파일을 다운로드하려면</span><span class="sxs-lookup"><span data-stu-id="3c110-133">To download the vault credential file to a local machine</span></span>
1. <span data-ttu-id="3c110-134">왼쪽 탐색 창에서 **복구 서비스**를 클릭한 다음 생성된 백업 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-134">In the left navigation pane, click **Recovery Services**, and then select the backup vault that you created.</span></span>

    ![IR 완료](./media/backup-configure-vault-classic/rs-left-nav.png)
2. <span data-ttu-id="3c110-136">빠른 시작 페이지에서 **자격 증명 모음 자격 증명 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-136">On the Quick Start page, click **Download vault credentials**.</span></span>

   <span data-ttu-id="3c110-137">클래식 포털에서는 자격 증명 모음 이름과 현재 날짜를 조합하여 보관 자격 증명을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-137">The classic portal generates a vault credential by using a combination of the vault name and the current date.</span></span> <span data-ttu-id="3c110-138">자격 증명 모음 자격 증명 파일은 등록 워크플로 중에만 사용되며 48시간 후에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-138">The vault credentials file is used only during the registration workflow and expires after 48 hours.</span></span>

   <span data-ttu-id="3c110-139">자격 증명 모음 자격 증명 파일은 포털에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-139">The vault credential file can be downloaded from the portal.</span></span>
3. <span data-ttu-id="3c110-140">**저장** 을 클릭하여 보관 자격 증명 파일을 로컬 계정의 다운로드 폴더에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-140">Click **Save** to download the vault credential file to the Downloads folder of the local account.</span></span> <span data-ttu-id="3c110-141">**저장** 메뉴에서 **다른 이름으로 저장**을 선택하여 보관 자격 증명 파일에 대한 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-141">You can also select **Save As** from the **Save** menu to specify a location for the vault credential file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c110-142">자격 증명 모음 자격 증명 파일이 컴퓨터에서 액세스할 수 있는 위치에 저장되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-142">Make sure the vault credential file is saved in a location that can be accessed from your machine.</span></span> <span data-ttu-id="3c110-143">파일 공유 또는 서버 메시지 블록에 저장되는 경우 액세스 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-143">If it is stored in a file share or server message block, verify that you have the permissions to access it.</span></span>
   >
   >

## <a name="download-install-and-register-the-backup-agent"></a><span data-ttu-id="3c110-144">Backup 에이전트 다운로드, 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="3c110-144">Download, install, and register the Backup agent</span></span>
<span data-ttu-id="3c110-145">백업 자격 증명 모음을 만들고 자격 증명 모음 자격 증명 파일을 다운로드한 후 각 Windows 컴퓨터에 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-145">After you create the backup vault and download the vault credential file, an agent must be installed on each of your Windows machines.</span></span>

### <a name="to-download-install-and-register-the-agent"></a><span data-ttu-id="3c110-146">에이전트를 다운로드, 설치 및 등록하려면</span><span class="sxs-lookup"><span data-stu-id="3c110-146">To download, install, and register the agent</span></span>
1. <span data-ttu-id="3c110-147">**복구 서비스**를 클릭한 다음 서버에 등록하려는 백업 저장소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-147">Click **Recovery Services**, and then select the backup vault that you want to register with a server.</span></span>
2. <span data-ttu-id="3c110-148">빠른 시작 페이지에서 **Windows Server 또는 System Center Data Protection Manager 또는 Windows 클라이언트용 에이전트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-148">On the Quick Start page, click the agent **Agent for Windows Server or System Center Data Protection Manager or Windows client**.</span></span> <span data-ttu-id="3c110-149">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-149">Then click **Save**.</span></span>

    ![에이전트 저장](./media/backup-configure-vault-classic/agent.png)
3. <span data-ttu-id="3c110-151">MARSagentinstaller.exe 파일 다운로드가 완료되면 **실행**을 클릭하거나 저장된 위치에서 **MARSAgentInstaller.exe**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-151">After the MARSagentinstaller.exe file has downloaded, click **Run** (or double-click **MARSAgentInstaller.exe** from the saved location).</span></span>
4. <span data-ttu-id="3c110-152">에이전트에 필요한 설치 폴더 및 캐시 폴더를 선택한 다음 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-152">Choose the installation folder and cache folder that are required for the agent, and then click **Next**.</span></span> <span data-ttu-id="3c110-153">지정된 캐시 위치에 백업 데이터의 5% 이상에 해당하는 여유 공간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-153">The cache location you specify must have free space equal to at least 5 percent of the backup data.</span></span>
5. <span data-ttu-id="3c110-154">기본 프록시 설정을 통해 인터넷에 계속해서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-154">You can continue to connect to the Internet through the default proxy settings.</span></span>             <span data-ttu-id="3c110-155">프록시 서버를 사용하여 인터넷에 연결하는 경우 프록시 구성 페이지에서 **사용자 지정 프록시 설정 사용** 확인란을 선택한 다음 프록시 서버 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-155">If you use a proxy server to connect to the Internet, on the Proxy Configuration page, select the **Use custom proxy settings** check box, and then enter the proxy server details.</span></span> <span data-ttu-id="3c110-156">인증된 프록시를 사용하는 경우 사용자 이름 및 암호 세부 정보를 입력한 다음 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-156">If you use an authenticated proxy, enter the user name and password details, and then click **Next**.</span></span>
6. <span data-ttu-id="3c110-157">**설치** 를 클릭하여 에이전트 설치를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-157">Click **Install** to begin the agent installation.</span></span> <span data-ttu-id="3c110-158">백업 에이전트가 .NET Framework 4.5 및 Windows PowerShell(아직 설치되지 않은 경우)을 설치하여 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-158">The Backup agent installs .NET Framework 4.5 and Windows PowerShell (if it’s not already installed) to complete the installation.</span></span>
7. <span data-ttu-id="3c110-159">에이전트가 설치되면 **등록 진행** 을 클릭하여 워크플로를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-159">After the agent is installed, click **Proceed to Registration** to continue with the workflow.</span></span>
8. <span data-ttu-id="3c110-160">자격 증명 모음 식별 페이지에서 이전에 다운로드한 자격 증명 모음 자격 증명 파일로 이동하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-160">On the Vault Identification page, browse to and select the vault credential file that you previously downloaded.</span></span>

    <span data-ttu-id="3c110-161">자격 증명 모음 자격 증명 파일은 48시간 동안만 유효합니다(그 이후에는 포털에서 다운로드).</span><span class="sxs-lookup"><span data-stu-id="3c110-161">The vault credential file is valid for only 48 hours after it’s downloaded from the portal.</span></span> <span data-ttu-id="3c110-162">이 페이지에서 오류가 발생할 경우(예: "제공한 자격 증명 모음 자격 증명 파일이 만료되었습니다.") 포털에 로그인하고 자격 증명 모음 자격 증명 파일을 다시 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-162">If you encounter an error on this page (such as “Vault credentials file provided has expired”), sign in to the portal and download the vault credential file again.</span></span>

    <span data-ttu-id="3c110-163">설치 응용 프로그램에서 액세스할 수 있는 위치에 있는 자격 증명 모음 자격 증명 파일인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-163">Ensure that the vault credential file is available in a location that can be accessed by the setup application.</span></span> <span data-ttu-id="3c110-164">액세스 관련 오류가 발생할 경우 동일한 컴퓨터의 임시 위치에 자격 증명 모음 자격 증명 파일을 복사하고 작업을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-164">If you encounter access-related errors, copy the vault credential file to a temporary location on the same machine and retry the operation.</span></span>

    <span data-ttu-id="3c110-165">자격 증명 모음 자격 증명 오류(예: "잘못된 자격 증명 모음 자격 증명을 제공했습니다.")가 발생한 경우 파일이 손상되었거나 복구 서비스와 연결된 최신 자격 증명이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-165">If you encounter a vault credential error such as “Invalid vault credentials provided," the file is damaged or does not have the latest credentials associated with the recovery service.</span></span> <span data-ttu-id="3c110-166">포털에서 새 자격 증명 모음 자격 증명 파일을 다운로드한 후에 작업을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-166">Retry the operation after downloading a new vault credential file from the portal.</span></span> <span data-ttu-id="3c110-167">이 오류는 사용자가 **보관 자격 증명 다운로드** 옵션을 빠르게 연속적으로 여러 번 클릭할 경우에 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-167">This error can also occur if a user clicks the **Download vault credential** option several times in quick succession.</span></span> <span data-ttu-id="3c110-168">이 경우 마지막 자격 증명 모음 자격 증명 파일만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-168">In this case, only the last vault credential file is valid.</span></span>
9. <span data-ttu-id="3c110-169">암호화 설정 페이지에서 암호를 생성하거나 암호를 제공합니다(최소 16자).</span><span class="sxs-lookup"><span data-stu-id="3c110-169">On the Encryption Setting page, you can either generate a passphrase or provide a passphrase (with a minimum of 16 characters).</span></span> <span data-ttu-id="3c110-170">암호를 안전한 위치에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-170">Remember to save the passphrase in a secure location.</span></span>
10. <span data-ttu-id="3c110-171">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-171">Click **Finish**.</span></span> <span data-ttu-id="3c110-172">서버 등록 마법사는 백업에 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-172">The Register Server Wizard registers the server with Backup.</span></span>

    > [!WARNING]
    > <span data-ttu-id="3c110-173">암호를 분실하거나 잊어버린 경우 Microsoft에서 백업 데이터의 복구를 도와드릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-173">If you lose or forget the passphrase, Microsoft cannot help you recover the backup data.</span></span> <span data-ttu-id="3c110-174">사용자는 암호화 암호를 소유하며 Microsoft는 사용자가 사용하는 암호를 전혀 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-174">You own the encryption passphrase, and Microsoft does not have visibility into the passphrase that you use.</span></span> <span data-ttu-id="3c110-175">이 파일은 복구 작업에 필요하므로 안전한 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-175">Save the file in a secure location because it will be required during a recovery operation.</span></span>
    >
    >

11. <span data-ttu-id="3c110-176">암호화 키가 설정되면, **Microsoft Azure 복구 서비스 에이전트 시작** 확인란은 선택된 상태로 둔 다음 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-176">After the encryption key is set, leave the **Launch Microsoft Azure Recovery Services Agent** check box selected, and then click **Close**.</span></span>

## <a name="complete-the-initial-backup"></a><span data-ttu-id="3c110-177">초기 백업 완료</span><span class="sxs-lookup"><span data-stu-id="3c110-177">Complete the initial backup</span></span>
<span data-ttu-id="3c110-178">초기 백업에는 두 가지 주요 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-178">The initial backup includes two key tasks:</span></span>

* <span data-ttu-id="3c110-179">백업 일정 만들기</span><span class="sxs-lookup"><span data-stu-id="3c110-179">Creating the backup schedule</span></span>
* <span data-ttu-id="3c110-180">처음으로 파일 및 폴더 백업</span><span class="sxs-lookup"><span data-stu-id="3c110-180">Backing up files and folders for the first time</span></span>

<span data-ttu-id="3c110-181">백업 정책이 초기 백업을 완료한 후에 데이터를 복구하는 경우 사용할 수 있는 백업 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-181">After the backup policy completes the initial backup, it creates backup points that you can use if you need to recover the data.</span></span> <span data-ttu-id="3c110-182">백업 정책은 정의하는 일정에 따라 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-182">The backup policy does this based on the schedule that you define.</span></span>

### <a name="to-schedule-the-backup"></a><span data-ttu-id="3c110-183">백업을 예약하려면</span><span class="sxs-lookup"><span data-stu-id="3c110-183">To schedule the backup</span></span>
1. <span data-ttu-id="3c110-184">Microsoft Azure 백업 에이전트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-184">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="3c110-185">(서버 등록 마법사를 닫을 때 **Microsoft Azure 복구 서비스 에이전트 시작** 확인란을 선택된 상태로 둔 경우 자동으로 열립니다.) **Microsoft Azure 백업**에 대한 컴퓨터를 검색하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-185">(It will open automatically if you left the **Launch Microsoft Azure Recovery Services Agent** check box selected when you closed the Register Server Wizard.) You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Azure 백업 에이전트 시작](./media/backup-configure-vault-classic/snap-in-search.png)
2. <span data-ttu-id="3c110-187">백업 에이전트에서 **백업 예약**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-187">In the Backup agent, click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. <span data-ttu-id="3c110-189">백업 예약 마법사의 시작 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-189">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="3c110-190">백업할 항목 선택 페이지에서 **항목 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-190">On the Select Items to Backup page, click **Add Items**.</span></span>
5. <span data-ttu-id="3c110-191">백업할 파일 및 폴더를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-191">Select the files and folders that you want to back up, and then click **Okay**.</span></span>
6. <span data-ttu-id="3c110-192">**Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-192">Click **Next**.</span></span>
7. <span data-ttu-id="3c110-193">**백업 일정 지정** 페이지에서 **백업 일정**을 지정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-193">On the **Specify Backup Schedule** page, specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="3c110-194">매일(하루에 최대 속도로 3회) 또는 매주 백업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-194">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server 백업에 대한 항목](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="3c110-196">백업 일정을 지정하는 방법은 [Azure 백업을 사용하여 테이프 인프라 대체](backup-azure-backup-cloud-as-tape.md)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c110-196">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="3c110-197">**보존 정책 선택** 페이지에서 백업 복사본의 **보존 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-197">On the **Select Retention Policy** page, select the **Retention Policy** for the backup copy.</span></span>

    <span data-ttu-id="3c110-198">보존 정책은 백업의 저장 기간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-198">The retention policy specifies the duration for which the backup will be stored.</span></span> <span data-ttu-id="3c110-199">모든 백업 지점에 대한 "일반 정책"을 지정하는 대신 백업이 발생하는 시기에 따라 다른 보존 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-199">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="3c110-200">매일, 매주, 매월 및 매년 보존 정책을 요구 사항에 맞게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-200">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="3c110-201">초기 백업 유형 선택 페이지에서 초기 백업 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-201">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="3c110-202">**네트워크를 통해 자동으로** 옵션이 선택된 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-202">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="3c110-203">네트워크를 통해 자동으로 백업하거나 오프라인으로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-203">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="3c110-204">이 문서의 나머지 부분은 자동 백업 프로세스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-204">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="3c110-205">오프라인 백업을 선호하는 경우 [Azure 백업의 오프라인 백업 워크플로](backup-azure-backup-import-export.md) 문서에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c110-205">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="3c110-206">확인 페이지에서 정보를 검토한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-206">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="3c110-207">마법사가 백업 일정 생성을 완료하면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-207">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling-optional"></a><span data-ttu-id="3c110-208">네트워크 제한 사용(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="3c110-208">Enable network throttling (optional)</span></span>
<span data-ttu-id="3c110-209">백업 에이전트는 네트워크 제한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-209">The Backup agent provides network throttling.</span></span> <span data-ttu-id="3c110-210">제한 기능은 데이터 전송 중에 사용되는 네트워크 대역폭의 양을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-210">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="3c110-211">근무 시간에 데이터를 백업해야 하는데 백업 프로세스가 다른 인터넷 트래픽을 방해하지 말아야 할 때 유용한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-211">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="3c110-212">제한은 백업 및 복원 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-212">Throttling applies to back up and restore activities.</span></span>

<span data-ttu-id="3c110-213">**네트워크 제한을 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="3c110-213">**To enable network throttling**</span></span>

1. <span data-ttu-id="3c110-214">백업 에이전트에서 **속성 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-214">In the Backup agent, click **Change Properties**.</span></span>

    ![속성 변경](./media/backup-configure-vault-classic/change-properties.png)
2. <span data-ttu-id="3c110-216">**제한** 탭에서 **백업 작업에 인터넷 대역폭 사용 제한 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-216">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![네트워크 제한](./media/backup-configure-vault-classic/throttling-dialog.png)
3. <span data-ttu-id="3c110-218">제한을 사용하도록 설정했으면 **근무 시간** 및 **휴무 시간** 중에 백업 데이터 전송에 허용되는 대역폭을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-218">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="3c110-219">대역폭 값은 512Kbps(초당 킬로비트)에서 시작하여 최대 1023MBps(초당 메가바이트)까지 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-219">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="3c110-220">또한 **근무 시간**의 시작 및 완료 시간과 근무일로 간주되는 요일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-220">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="3c110-221">지정된 작업 시간 이외의 시간은 비 작업 시간으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-221">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="3c110-222">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-222">Click **OK**.</span></span>

### <a name="to-back-up-now"></a><span data-ttu-id="3c110-223">지금 백업하려면</span><span class="sxs-lookup"><span data-stu-id="3c110-223">To back up now</span></span>
1. <span data-ttu-id="3c110-224">백업 에이전트에서 **지금 백업** 을 클릭하여 네트워크를 통한 초기 시드 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-224">In the Backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![지금 Windows Server 백업](./media/backup-configure-vault-classic/backup-now.png)
2. <span data-ttu-id="3c110-226">확인 페이지에서 컴퓨터를 백업하는 데 지금 백업 마법사가 사용할 설정을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-226">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="3c110-227">그런 다음 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-227">Then click **Back Up**.</span></span>
3. <span data-ttu-id="3c110-228">**닫기** 를 클릭하여 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-228">Click **Close** to close the wizard.</span></span> <span data-ttu-id="3c110-229">백업 프로세스가 완료되기 전에 이를 수행한 경우 마법사는 백그라운드에서 계속해서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-229">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="3c110-230">초기 백업 작업이 완료되면 백업 콘솔에 **작업 완료** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-230">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR 완료](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a><span data-ttu-id="3c110-232">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c110-232">Next steps</span></span>
* <span data-ttu-id="3c110-233">[무료 Azure 계정](https://azure.microsoft.com/free/)을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3c110-233">Sign up for a [free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="3c110-234">VM 또는 다른 워크로드를 백업하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c110-234">For additional information about backing up VMs or other workloads, see:</span></span>

* [<span data-ttu-id="3c110-235">IaaS VM 백업</span><span class="sxs-lookup"><span data-stu-id="3c110-235">Back up IaaS VMs</span></span>](backup-azure-vms-prepare.md)
* [<span data-ttu-id="3c110-236">Microsoft Azure 백업 서버를 통해 Azure에 워크로드 백업</span><span class="sxs-lookup"><span data-stu-id="3c110-236">Back up workloads to Azure with Microsoft Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)
* [<span data-ttu-id="3c110-237">DPM을 통해 Azure에 워크로드 백업</span><span class="sxs-lookup"><span data-stu-id="3c110-237">Back up workloads to Azure with DPM</span></span>](backup-azure-dpm-introduction.md)
