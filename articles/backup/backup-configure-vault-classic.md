---
title: "Windows 서버 또는 워크스테이션 tooAzure (클래식 모델)을 aaaBack | Microsoft Docs"
description: "Windows 서버 또는 클라이언트 tooa 백업 자격 증명 모음 Azure에 백업 합니다. Hello Azure 백업 에이전트를 사용 하 여 백업 자격 증명 모음 tooa 파일 및 폴더를 보호 하기 위한 기본 이동 합니다."
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
ms.openlocfilehash: c8f2a9bed1e5885f5c272c65b9282ededc05850a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-workstation-tooazure-using-hello-classic-portal"></a><span data-ttu-id="c4766-105">Hello 클래식 포털을 사용 하 여 Windows 서버 또는 워크스테이션 tooAzure 백업</span><span class="sxs-lookup"><span data-stu-id="c4766-105">Back up a Windows server or workstation tooAzure using hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4766-106">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="c4766-106">Classic portal</span></span>](backup-configure-vault-classic.md)
> * [<span data-ttu-id="c4766-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="c4766-107">Azure portal</span></span>](backup-configure-vault.md)
>
>

<span data-ttu-id="c4766-108">이 문서는 사용자 환경 toofollow tooprepare 필요 하 고 Windows 서버 (또는 워크스테이션) tooAzure 백업 hello 절차를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-108">This article covers hello procedures that you need toofollow tooprepare your environment and back up a Windows server (or workstation) tooAzure.</span></span> <span data-ttu-id="c4766-109">또한 백업 솔루션 배포 시 고려 사항에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-109">It also covers considerations for deploying your backup solution.</span></span> <span data-ttu-id="c4766-110">처음으로 hello에 대 한 Azure 백업 시도에 관심이 있다면이 여기서 신속 하 게 과정을 보여 줍니다 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-110">If you're interested in trying Azure Backup for hello first time, this article quickly walks you through hello process.</span></span>

<span data-ttu-id="c4766-111">Azure는 리소스를 만들고 작업하기 위한 두 가지 배포 모델로 리소스 관리자와 클래식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-111">Azure has two different deployment models for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="c4766-112">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-112">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="c4766-113">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c4766-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="c4766-114">Before you start</span></span>
<span data-ttu-id="c4766-115">서버 또는 클라이언트 tooAzure tooback, Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-115">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="c4766-116">계정이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/free/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-116">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-backup-vault"></a><span data-ttu-id="c4766-117">백업 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="c4766-117">Create a backup vault</span></span>
<span data-ttu-id="c4766-118">서버 또는 클라이언트에서 파일 및 폴더를 tooback, toocreate toostore hello 데이터 hello 지리적 지역에 백업 자격 증명 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-118">tooback up files and folders from a server or client, you need toocreate a backup vault in hello geographic region where you want toostore hello data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4766-119">2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-119">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="c4766-120">이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-120">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="c4766-121">자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-121">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="c4766-122">Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-122">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="c4766-123">**2017 년 10 월 15**, 수 toouse PowerShell toocreate 백업 자격 증명 모음은 더 이상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-123">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="c4766-124">**2017년 11월 1일 시작**:</span><span class="sxs-lookup"><span data-stu-id="c4766-124">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="c4766-125">나머지 모든 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-125">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="c4766-126">하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-126">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="c4766-127">대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-127">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>


## <a name="download-hello-vault-credential-file"></a><span data-ttu-id="c4766-128">Hello 자격 증명 모음 자격 증명 파일을 다운로드</span><span class="sxs-lookup"><span data-stu-id="c4766-128">Download hello vault credential file</span></span>
<span data-ttu-id="c4766-129">hello 온-프레미스 컴퓨터 toobe tooAzure 데이터를 백업할 수 전에 백업 자격 증명 인증에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-129">hello on-premises machine needs toobe authenticated with a backup vault before it can back up data tooAzure.</span></span> <span data-ttu-id="c4766-130">hello 인증 누군가가 *자격 증명을 자격 증명 모음*합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-130">hello authentication is achieved through *vault credentials*.</span></span> <span data-ttu-id="c4766-131">hello 클래식 포털에서 보안 채널을 통해 hello 자격 증명 모음 자격 증명 파일이 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-131">hello vault credential file is downloaded through a secure channel from hello classic portal.</span></span> <span data-ttu-id="c4766-132">hello 인증서 개인 키 hello 포털 또는 hello 서비스에 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-132">hello certificate private key does not persist in hello portal or hello service.</span></span>

### <a name="toodownload-hello-vault-credential-file-tooa-local-machine"></a><span data-ttu-id="c4766-133">toodownload hello 자격 증명 모음 자격 증명 파일 tooa 로컬 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="c4766-133">toodownload hello vault credential file tooa local machine</span></span>
1. <span data-ttu-id="c4766-134">Hello 왼쪽된 탐색 창에서 클릭 **복구 서비스**, 한 다음 만든 된 자격 증명 hello 백업 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-134">In hello left navigation pane, click **Recovery Services**, and then select hello backup vault that you created.</span></span>

    ![IR 완료](./media/backup-configure-vault-classic/rs-left-nav.png)
2. <span data-ttu-id="c4766-136">Hello 빠른 시작 페이지에서 클릭 **자격 증명 모음 다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-136">On hello Quick Start page, click **Download vault credentials**.</span></span>

   <span data-ttu-id="c4766-137">hello 클래식 포털에서는 hello 및 hello 자격 증명 모음 이름과 현재 날짜를 조합 하 여 자격 증명 모음 자격 증명을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-137">hello classic portal generates a vault credential by using a combination of hello vault name and hello current date.</span></span> <span data-ttu-id="c4766-138">hello 자격 증명 모음 자격 증명 파일 hello 등록 워크플로 중에 사용 되며 48 시간 후 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-138">hello vault credentials file is used only during hello registration workflow and expires after 48 hours.</span></span>

   <span data-ttu-id="c4766-139">hello 포털에서 hello 자격 증명 모음 자격 증명 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-139">hello vault credential file can be downloaded from hello portal.</span></span>
3. <span data-ttu-id="c4766-140">클릭 **저장** toodownload hello 자격 증명 모음 자격 증명 파일 toohello 다운로드 폴더의 hello 로컬 계정.</span><span class="sxs-lookup"><span data-stu-id="c4766-140">Click **Save** toodownload hello vault credential file toohello Downloads folder of hello local account.</span></span> <span data-ttu-id="c4766-141">선택할 수도 있습니다 **다른 이름으로 저장** hello에서 **저장** 메뉴 toospecify hello 자격 증명 모음 자격 증명 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-141">You can also select **Save As** from hello **Save** menu toospecify a location for hello vault credential file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c4766-142">Hello 자격 증명 모음 자격 증명 파일은 컴퓨터에서 액세스할 수 있는 위치에 저장 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-142">Make sure hello vault credential file is saved in a location that can be accessed from your machine.</span></span> <span data-ttu-id="c4766-143">파일 공유 또는 서버 메시지 블록에 저장 되는지를 hello 권한을 tooaccess 있는지 확인 하기.</span><span class="sxs-lookup"><span data-stu-id="c4766-143">If it is stored in a file share or server message block, verify that you have hello permissions tooaccess it.</span></span>
   >
   >

## <a name="download-install-and-register-hello-backup-agent"></a><span data-ttu-id="c4766-144">다운로드, 설치 및 hello 백업 에이전트를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-144">Download, install, and register hello Backup agent</span></span>
<span data-ttu-id="c4766-145">Hello 백업 자격 증명 모음 및 다운로드 hello 자격 증명 모음 자격 증명 파일을 만든 후 각각의 Windows 컴퓨터에서 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-145">After you create hello backup vault and download hello vault credential file, an agent must be installed on each of your Windows machines.</span></span>

### <a name="toodownload-install-and-register-hello-agent"></a><span data-ttu-id="c4766-146">toodownload, 설치 및 hello 에이전트 등록</span><span class="sxs-lookup"><span data-stu-id="c4766-146">toodownload, install, and register hello agent</span></span>
1. <span data-ttu-id="c4766-147">클릭 **복구 서비스**, 한 다음 원하는 서버와 tooregister hello 백업 자격 증명을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-147">Click **Recovery Services**, and then select hello backup vault that you want tooregister with a server.</span></span>
2. <span data-ttu-id="c4766-148">Hello 빠른 시작 페이지에서 클릭 hello 에이전트 **에이전트에 대 한 Windows Server 또는 System Center Data Protection Manager 또는 Windows client**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-148">On hello Quick Start page, click hello agent **Agent for Windows Server or System Center Data Protection Manager or Windows client**.</span></span> <span data-ttu-id="c4766-149">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-149">Then click **Save**.</span></span>

    ![에이전트 저장](./media/backup-configure-vault-classic/agent.png)
3. <span data-ttu-id="c4766-151">Hello MARSagentinstaller.exe 파일을 다운로드 한 후 클릭 **실행** (두 번 클릭 하거나 **MARSAgentInstaller.exe** hello 저장 위치에서).</span><span class="sxs-lookup"><span data-stu-id="c4766-151">After hello MARSagentinstaller.exe file has downloaded, click **Run** (or double-click **MARSAgentInstaller.exe** from hello saved location).</span></span>
4. <span data-ttu-id="c4766-152">Hello 설치 폴더 및 hello 에이전트에 필요한 캐시 폴더를 선택 하 고 클릭 한 다음 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-152">Choose hello installation folder and cache folder that are required for hello agent, and then click **Next**.</span></span> <span data-ttu-id="c4766-153">지정한 hello 캐시 위치는 hello 백업 데이터의 최소 5% 같은 tooat 여유 공간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-153">hello cache location you specify must have free space equal tooat least 5 percent of hello backup data.</span></span>
5. <span data-ttu-id="c4766-154">Hello 기본 프록시 설정을 통해 tooconnect toohello 인터넷을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-154">You can continue tooconnect toohello Internet through hello default proxy settings.</span></span>             <span data-ttu-id="c4766-155">Hello 프록시 구성 페이지에서 프록시 서버 tooconnect toohello 인터넷을 사용 하는 경우 선택 hello **사용자 지정 프록시 설정을 사용 하 여** 확인란을 선택한 다음 hello 프록시 서버 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-155">If you use a proxy server tooconnect toohello Internet, on hello Proxy Configuration page, select hello **Use custom proxy settings** check box, and then enter hello proxy server details.</span></span> <span data-ttu-id="c4766-156">인증 된 프록시를 사용 하 여 hello 사용자 이름 및 암호 세부 정보를 입력 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-156">If you use an authenticated proxy, enter hello user name and password details, and then click **Next**.</span></span>
6. <span data-ttu-id="c4766-157">클릭 **설치** toobegin hello 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-157">Click **Install** toobegin hello agent installation.</span></span> <span data-ttu-id="c4766-158">hello 백업 에이전트 설치.NET Framework 4.5 및 Windows PowerShell (설치 되어 있지 않음) 하는 경우 toocomplete hello 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-158">hello Backup agent installs .NET Framework 4.5 and Windows PowerShell (if it’s not already installed) toocomplete hello installation.</span></span>
7. <span data-ttu-id="c4766-159">Hello 에이전트를 설치한 후 클릭 **tooRegistration 계속** hello 워크플로와 toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-159">After hello agent is installed, click **Proceed tooRegistration** toocontinue with hello workflow.</span></span>
8. <span data-ttu-id="c4766-160">Hello Id 자격 증명 모음 페이지에서 이전에 다운로드 한 tooand 선택 hello 자격 증명 모음 자격 증명 파일을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-160">On hello Vault Identification page, browse tooand select hello vault credential file that you previously downloaded.</span></span>

    <span data-ttu-id="c4766-161">hello 자격 증명 모음 자격 증명 파일은 hello 포털에서 다운로드 된 후 48 시간 동안만 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-161">hello vault credential file is valid for only 48 hours after it’s downloaded from hello portal.</span></span> <span data-ttu-id="c4766-162">에 오류가 발생 하는 경우 (예: "자격 증명 모음 자격 증명 제공 된 파일이 만료 되었습니다."),이 페이지 toohello 포털에 로그인 하 고 hello 자격 증명 모음 자격 증명 파일을 다시 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-162">If you encounter an error on this page (such as “Vault credentials file provided has expired”), sign in toohello portal and download hello vault credential file again.</span></span>

    <span data-ttu-id="c4766-163">Hello 설치 응용 프로그램에서 액세스할 수 있는 위치에 해당 hello 자격 증명 모음 자격 증명 파일을 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-163">Ensure that hello vault credential file is available in a location that can be accessed by hello setup application.</span></span> <span data-ttu-id="c4766-164">액세스와 관련 된 오류가 발생 하는 경우 복사 hello 자격 증명 모음 자격 증명 파일 tooa 임시 위치에 hello 동일 컴퓨터 하 고 hello 작업을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-164">If you encounter access-related errors, copy hello vault credential file tooa temporary location on hello same machine and retry hello operation.</span></span>

    <span data-ttu-id="c4766-165">"잘못 된 자격 증명 모음 자격 증명을 제공"와 같은 자격 증명 모음 자격 증명 오류가 발생 하면 hello 파일이 손상 되었거나 hello 복구 서비스와 연결 된 최신 자격도 hello가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-165">If you encounter a vault credential error such as “Invalid vault credentials provided," hello file is damaged or does not have hello latest credentials associated with hello recovery service.</span></span> <span data-ttu-id="c4766-166">Hello hello 포털에서 새 자격 증명 모음 자격 증명 파일을 다운로드 한 후 작업을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c4766-166">Retry hello operation after downloading a new vault credential file from hello portal.</span></span> <span data-ttu-id="c4766-167">Hello를 클릭 하는 경우에이 오류가 발생할 수 **자격 증명 모음 다운로드** 연속적으로 여러 번 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-167">This error can also occur if a user clicks hello **Download vault credential** option several times in quick succession.</span></span> <span data-ttu-id="c4766-168">이 경우에 hello 마지막 자격 증명 모음 자격 증명 파일이 유효한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-168">In this case, only hello last vault credential file is valid.</span></span>
9. <span data-ttu-id="c4766-169">Hello 암호화 설정 페이지에서 암호를 생성 하거나 (최소 16 자)와 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-169">On hello Encryption Setting page, you can either generate a passphrase or provide a passphrase (with a minimum of 16 characters).</span></span> <span data-ttu-id="c4766-170">안전한 위치에 toosave hello 암호를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-170">Remember toosave hello passphrase in a secure location.</span></span>
10. <span data-ttu-id="c4766-171">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-171">Click **Finish**.</span></span> <span data-ttu-id="c4766-172">서버 등록 마법사 hello 백업을 사용 하 여 hello 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-172">hello Register Server Wizard registers hello server with Backup.</span></span>

    > [!WARNING]
    > <span data-ttu-id="c4766-173">끊어지거나 hello 암호를 잊은 경우 Microsoft hello 백업 데이터를 복구할 수 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-173">If you lose or forget hello passphrase, Microsoft cannot help you recover hello backup data.</span></span> <span data-ttu-id="c4766-174">소유 하 고 암호화 암호는 hello 및 사용 하는 hello 암호에 대 한 가시성 갖고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-174">You own hello encryption passphrase, and Microsoft does not have visibility into hello passphrase that you use.</span></span> <span data-ttu-id="c4766-175">복구 작업 중 필요한 수 있으므로 hello 파일을 안전한 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-175">Save hello file in a secure location because it will be required during a recovery operation.</span></span>
    >
    >

11. <span data-ttu-id="c4766-176">Hello 암호화 키가 설정 hello 유지 **Microsoft Azure 복구 서비스 에이전트 시작** 확인란을 선택 하 고 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-176">After hello encryption key is set, leave hello **Launch Microsoft Azure Recovery Services Agent** check box selected, and then click **Close**.</span></span>

## <a name="complete-hello-initial-backup"></a><span data-ttu-id="c4766-177">초기 백업을 완료 hello</span><span class="sxs-lookup"><span data-stu-id="c4766-177">Complete hello initial backup</span></span>
<span data-ttu-id="c4766-178">초기 백업을 hello 두 가지 주요 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-178">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="c4766-179">Hello 백업 예약 만들기</span><span class="sxs-lookup"><span data-stu-id="c4766-179">Creating hello backup schedule</span></span>
* <span data-ttu-id="c4766-180">처음으로 파일 및 hello에 대 한 폴더를 백업</span><span class="sxs-lookup"><span data-stu-id="c4766-180">Backing up files and folders for hello first time</span></span>

<span data-ttu-id="c4766-181">백업 정책 hello hello 초기 백업을 완료 된 후 백업 지점을 toorecover hello 데이터 유지 해야 하는 경우 사용할 수 있는 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-181">After hello backup policy completes hello initial backup, it creates backup points that you can use if you need toorecover hello data.</span></span> <span data-ttu-id="c4766-182">hello 백업 정책을 정의 하는 hello 일정에 따라이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-182">hello backup policy does this based on hello schedule that you define.</span></span>

### <a name="tooschedule-hello-backup"></a><span data-ttu-id="c4766-183">tooschedule hello 백업</span><span class="sxs-lookup"><span data-stu-id="c4766-183">tooschedule hello backup</span></span>
1. <span data-ttu-id="c4766-184">Hello Microsoft Azure 백업 에이전트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-184">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="c4766-185">(자동으로 열립니다 hello 두 었으 면 **Microsoft Azure 복구 서비스 에이전트를 시작** hello 서버 등록 마법사를 닫을 때 선택.) **Microsoft Azure 백업**에 대한 컴퓨터를 검색하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-185">(It will open automatically if you left hello **Launch Microsoft Azure Recovery Services Agent** check box selected when you closed hello Register Server Wizard.) You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Hello Azure 백업 에이전트를 시작 합니다.](./media/backup-configure-vault-classic/snap-in-search.png)
2. <span data-ttu-id="c4766-187">Hello 백업 에이전트에서 클릭 **백업 예약**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-187">In hello Backup agent, click **Schedule Backup**.</span></span>

    ![Windows Server 백업 예약](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. <span data-ttu-id="c4766-189">Hello에 시작 hello 백업 예약 마법사의 페이지를 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-189">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="c4766-190">Hello 항목 선택 tooBackup 페이지에서 클릭 **항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-190">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="c4766-191">Hello 파일 및 폴더, tooback 원하는 클릭 한 다음 선택 **알겠습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-191">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="c4766-192">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-192">Click **Next**.</span></span>
7. <span data-ttu-id="c4766-193">Hello에 **백업 일정 지정** 페이지에서 지정 하는 hello **백업 일정** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-193">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="c4766-194">매일(하루에 최대 속도로 3회) 또는 매주 백업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-194">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server 백업에 대한 항목](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="c4766-196">Toospecify 백업 일정을 hello 하는 방법에 대 한 자세한 내용은 hello 문서 참조 [사용 하 여 Azure 백업 tooreplace 테이프 인프라](backup-azure-backup-cloud-as-tape.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-196">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="c4766-197">Hello에 **보존 정책 선택** 페이지, 선택 hello **보존 정책** hello 백업 복사본에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-197">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="c4766-198">hello 보존 정책 hello 백업이 저장 될 hello 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-198">hello retention policy specifies hello duration for which hello backup will be stored.</span></span> <span data-ttu-id="c4766-199">모든 백업 지점에 대 한 "플랫 정책을"를 방금 지정 하는 대신 hello 백업이 발생 하는 경우에 따라 서로 다른 보존 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-199">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="c4766-200">매일, 매주, 매월 및 매년 보존 정책을 toomeet hello 요구에 맞게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-200">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="c4766-201">Hello 초기 백업 유형 선택 페이지에서 hello 초기 백업 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-201">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="c4766-202">Hello 옵션인 **hello 네트워크를 통해 자동으로** 을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-202">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="c4766-203">Hello 네트워크를 통해 자동으로를 백업할 수 있습니다 또는 오프 라인으로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-203">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="c4766-204">이 문서의 나머지 부분에서는 hello 자동으로 백업에 대 한 hello 프로세스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-204">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="c4766-205">오프 라인 백업을 toodo 원한다 면 hello 문서를 검토 [Azure 백업에서 오프 라인 백업 워크플로](backup-azure-backup-import-export.md) 추가 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-205">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="c4766-206">Hello 확인 페이지에서 hello 정보를 검토 한 다음 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-206">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="c4766-207">Hello 마법사 hello 백업 예약 만들기를 완료 한 후 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-207">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling-optional"></a><span data-ttu-id="c4766-208">네트워크 제한 사용(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="c4766-208">Enable network throttling (optional)</span></span>
<span data-ttu-id="c4766-209">네트워크 제한 hello 백업 에이전트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-209">hello Backup agent provides network throttling.</span></span> <span data-ttu-id="c4766-210">제한 기능은 데이터 전송 중에 사용되는 네트워크 대역폭의 양을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-210">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="c4766-211">이 컨트롤 근무 시간 동안 데이터를 tooback 필요 하지만 다른 인터넷 트래픽과 hello 백업 프로세스 toointerfere 하지 않을 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-211">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="c4766-212">제한 tooback를 적용 하 고 복원 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-212">Throttling applies tooback up and restore activities.</span></span>

<span data-ttu-id="c4766-213">**tooenable 네트워크 제한**</span><span class="sxs-lookup"><span data-stu-id="c4766-213">**tooenable network throttling**</span></span>

1. <span data-ttu-id="c4766-214">Hello 백업 에이전트에서 클릭 **속성 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-214">In hello Backup agent, click **Change Properties**.</span></span>

    ![속성 변경](./media/backup-configure-vault-classic/change-properties.png)
2. <span data-ttu-id="c4766-216">Hello에 **제한** 탭, 선택 hello **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-216">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![네트워크 제한](./media/backup-configure-vault-classic/throttling-dialog.png)
3. <span data-ttu-id="c4766-218">제한을 사용 하도록 설정 하는 동안 백업 데이터 전송에 대 한 대역폭을 허용 하는 hello 지정 **근무 시간** 및 **휴무 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-218">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="c4766-219">hello 대역폭 값 (Kbps) 초당 킬로 비트부터 시작 하 고 too1, 023 m b / 초 (MBps) 위로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-219">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="c4766-220">또한 hello 시작을 지정 하 고 완료 수 **근무 시간**, hello 요일을 작업일 수로 간주 되며 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-220">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="c4766-221">지정된 작업 시간 이외의 시간은 비 작업 시간으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-221">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="c4766-222">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-222">Click **OK**.</span></span>

### <a name="tooback-up-now"></a><span data-ttu-id="c4766-223">지금을 tooback</span><span class="sxs-lookup"><span data-stu-id="c4766-223">tooback up now</span></span>
1. <span data-ttu-id="c4766-224">Hello 백업 에이전트에서 클릭 **지금 백업** toocomplete hello 시드 hello 네트워크를 통해 초기 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-224">In hello Backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![지금 Windows Server 백업](./media/backup-configure-vault-classic/backup-now.png)
2. <span data-ttu-id="c4766-226">Hello 확인 페이지에서 지금 백업 마법사 hello hello 설정 검토 tooback hello 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-226">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="c4766-227">그런 다음 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-227">Then click **Back Up**.</span></span>
3. <span data-ttu-id="c4766-228">클릭 **닫기** tooclose hello 마법사.</span><span class="sxs-lookup"><span data-stu-id="c4766-228">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="c4766-229">이렇게 하면 hello 백업 프로세스를 완료 하기 전에 hello 마법사 toorun hello 백그라운드에서 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-229">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="c4766-230">Hello 초기 백업을 완료 되 면 hello **작업을 완료 했지만** hello 백업 콘솔에 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-230">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR 완료](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a><span data-ttu-id="c4766-232">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4766-232">Next steps</span></span>
* <span data-ttu-id="c4766-233">[무료 Azure 계정](https://azure.microsoft.com/free/)을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c4766-233">Sign up for a [free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="c4766-234">VM 또는 다른 워크로드를 백업하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4766-234">For additional information about backing up VMs or other workloads, see:</span></span>

* [<span data-ttu-id="c4766-235">IaaS VM 백업</span><span class="sxs-lookup"><span data-stu-id="c4766-235">Back up IaaS VMs</span></span>](backup-azure-vms-prepare.md)
* [<span data-ttu-id="c4766-236">Microsoft Azure 백업 서버 워크 로드 tooAzure 백업</span><span class="sxs-lookup"><span data-stu-id="c4766-236">Back up workloads tooAzure with Microsoft Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)
* [<span data-ttu-id="c4766-237">Dpm 작업 부하 tooAzure 백업</span><span class="sxs-lookup"><span data-stu-id="c4766-237">Back up workloads tooAzure with DPM</span></span>](backup-azure-dpm-introduction.md)
