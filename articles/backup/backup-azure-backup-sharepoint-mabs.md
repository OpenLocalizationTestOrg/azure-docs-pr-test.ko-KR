---
title: "Azure Backup Server를 사용하여 Azure에 대한 SharePoint 팜 백업 | Microsoft Docs"
description: "Azure Backup Server를 사용하여 SharePoint 데이터를 백업 및 복원합니다. 이 문서에서는 원하는 데이터를 Azure에 저장할 수 있도록 SharePoint 팜을 구성하는 정보를 제공합니다. 디스크 또는 Azure에서 보호된 SharePoint 데이터를 복원할 수 있습니다."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 3ed000affd326eb1bd7c99773ec021ad6e03cc3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a><span data-ttu-id="daedf-105">Azure에 SharePoint 팜 백업</span><span class="sxs-lookup"><span data-stu-id="daedf-105">Back up a SharePoint farm to Azure</span></span>
<span data-ttu-id="daedf-106">SharePoint 팜은 다른 데이터 원본을 백업하는 것과 같은 방법으로 Microsoft Azure Backup Server(MABS)를 사용하여 Microsoft Azure에 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-106">You back up a SharePoint farm to Microsoft Azure by using Microsoft Azure Backup Server (MABS) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="daedf-107">Azure 백업은 일간, 주간, 월간 혹은 연간 백업 지점을 생성하도록 백업 일정에 유연성을 제공하고 다양한 백업 지점에 관한 보존 정책 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-107">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="daedf-108">또한 빠른 복구 시간 목표(RTO)를 위해 로컬 디스크 복사본을 저장하는 기능과 경제적인 장기 보존을 위해 Azure에 사본을 복사하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-108">It also provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="daedf-109">SharePoint가 지원하는 버전 및 관련 보호 시나리오</span><span class="sxs-lookup"><span data-stu-id="daedf-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="daedf-110">DPM의 Azure 백업은 다음 시나리오들을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-110">Azure Backup for DPM supports the following scenarios:</span></span>

| <span data-ttu-id="daedf-111">워크로드</span><span class="sxs-lookup"><span data-stu-id="daedf-111">Workload</span></span> | <span data-ttu-id="daedf-112">버전</span><span class="sxs-lookup"><span data-stu-id="daedf-112">Version</span></span> | <span data-ttu-id="daedf-113">SharePoint 배포</span><span class="sxs-lookup"><span data-stu-id="daedf-113">SharePoint deployment</span></span> | <span data-ttu-id="daedf-114">보호 및 복구</span><span class="sxs-lookup"><span data-stu-id="daedf-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="daedf-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="daedf-115">SharePoint</span></span> |<span data-ttu-id="daedf-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="daedf-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="daedf-117">SharePoint는 물리적 서버 또는 하이퍼-V/VMware 가상 컴퓨터로 배포됨 </span><span class="sxs-lookup"><span data-stu-id="daedf-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="daedf-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="daedf-118">SQL AlwaysOn</span></span> | <span data-ttu-id="daedf-119">SharePoint 팜 보호 복구 옵션: 복구 팜, 데이터베이스, 및 파일 또는 디스크 복구 지점의 목록 항목 </span><span class="sxs-lookup"><span data-stu-id="daedf-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="daedf-120">Azure 복구 지점에서 팜 및 데이터베이스 복구</span><span class="sxs-lookup"><span data-stu-id="daedf-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="daedf-121">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="daedf-121">Before you start</span></span>
<span data-ttu-id="daedf-122">SharePoint 팜을 Azure에 백업하기 전에 몇 가지 확인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-122">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="daedf-123">필수 조건</span><span class="sxs-lookup"><span data-stu-id="daedf-123">Prerequisites</span></span>
<span data-ttu-id="daedf-124">진행에 앞서, 워크로드를 보호하기 위해 [Azure Backup Server를 설치 및 준비](backup-azure-microsoft-azure-backup.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-124">Before you proceed, make sure that you have [installed and prepared the Azure Backup Server](backup-azure-microsoft-azure-backup.md) to protect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="daedf-125">보호 에이전트</span><span class="sxs-lookup"><span data-stu-id="daedf-125">Protection agent</span></span>
<span data-ttu-id="daedf-126">보호 에이전트가 SharePoint를 실행하는 서버, SQL Server를 실행하는 서버, SharePoint 팜에 속하는 그 밖의 모든 서버에 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-126">The Protection agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="daedf-127">보호 에이전트를 설정하는 방법 대한 자세한 내용은 [보호 에이전트 설치](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="daedf-127">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="daedf-128">유일한 예외는 단일 WFE(웹 프런트엔드) 서버에만 에이전트를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-128">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="daedf-129">DPM은 보호를 위한 진입점 용도로만 단일 WFE 서버의 에이전트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-129">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="daedf-130">Sharepoint 팜</span><span class="sxs-lookup"><span data-stu-id="daedf-130">SharePoint farm</span></span>
<span data-ttu-id="daedf-131">팜의 모든 항목이 천만 개에 이르기 때문에, MABS 폴더의 위치에는 최소 2GB의 공간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-131">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the MABS folder is located.</span></span> <span data-ttu-id="daedf-132">이 공간은 카탈로그를 생성하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-132">This space is required for catalog generation.</span></span> <span data-ttu-id="daedf-133">MABS가 특정 항목(사이트 모음, 사이트, 목록, 문서 라이브러리, 폴더, 개별 문서 및 목록 항목)을 복구할 때 카탈로그 생성이 각 콘텐츠 데이터베이스에 포함된 URL의 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-133">For MABS to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="daedf-134">MABS 관리자 콘솔 안의 **복구** 작업 영역에서 복구 가능한 항목 창의 URL 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-134">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="daedf-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="daedf-135">SQL Server</span></span>
<span data-ttu-id="daedf-136">MABS는 LocalSystem 계정으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="daedf-137">SQL Server 데이터베이스를 백업하려면, MABS에 SQL Server를 실행하는 서버의 해당 계정에 대한 sysadmin 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-137">To back up SQL Server databases, MABS needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="daedf-138">백업하기 전에 SQL Server를 실행하는 서버에서 NT AUTHORITY\SYSTEM을 *sysadmin*으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-138">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="daedf-139">SharePoint 팜에 SQL Server 별칭으로 구성 된 SQL Server 데이터베이스가 있는 경우, MABS가 보호할 프런트엔드 웹 서버에 SQL Server 클라이언트 구성 요소를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-139">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="daedf-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="daedf-140">SharePoint Server</span></span>
<span data-ttu-id="daedf-141">성능은 SharePoint 팜의 크기와 같은 여러 요인에 따라 달라지지만, 일반 지침에 의하면 MABS 하나가 25TB SharePoint 팜을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="daedf-142">지원 되지않는 사항</span><span class="sxs-lookup"><span data-stu-id="daedf-142">What's not supported</span></span>
* <span data-ttu-id="daedf-143">SharePoint 팜을 보호하는 MABS는 검색 인덱스 또는 응용 프로그램 서비스 데이터베이스를 보호하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="daedf-144">이러한 데이터베이스들은 별도로 보호를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-144">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="daedf-145">MABS는 스케일 아웃 파일 서버(SOFS) 공유에 호스트되는 SharePoint SQL Server 데이터베이스의 백업을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="daedf-146">SharePoint 보호 구성</span><span class="sxs-lookup"><span data-stu-id="daedf-146">Configure SharePoint protection</span></span>
<span data-ttu-id="daedf-147">MABS를 사용하여 SharePoint를 보호할 수 있으려면, **ConfigureSharePoint.exe**를 사용하여 SharePoint VSS 기록기 서비스(WSS 기록기 서비스)를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-147">Before you can use MABS to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="daedf-148">**ConfigureSharePoint.exe**는 프런트엔드 웹 서버의 [MABS 설치 경로]\bin 폴더에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-148">You can find **ConfigureSharePoint.exe** in the [MABS Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="daedf-149">이 도구는 SharePoint 팜의 자격 증명을 사용하여 보호 에이전트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-149">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="daedf-150">단일 WFE 서버에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-150">You run it on a single WFE server.</span></span> <span data-ttu-id="daedf-151">WFE 서버가 여러 개인 경우, 보호 그룹을 구성할 때 하나만 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="daedf-152">SharePoint VSS 기록기 서비스를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="daedf-152">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="daedf-153">WFE 서버의 명령 프롬프트에서 [MABS 설치 위치] \bin\으로 이동</span><span class="sxs-lookup"><span data-stu-id="daedf-153">On the WFE server, at a command prompt, go to [MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="daedf-154">ConfigureSharePoint -EnableSharePointProtection을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="daedf-155">팜 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-155">Enter the farm administrator credentials.</span></span> <span data-ttu-id="daedf-156">이 계정은 WFE 서버에서 로컬 관리자 그룹의 구성원 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-156">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="daedf-157">팜 관리자가 로컬 관리자가 아닌 경우, WFE 서버에 다음 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-157">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="daedf-158">DPM 폴더(%Program Files%\Microsoft Azure Backup\DPM)에 WSS_Admin_WPG 그룹 전체 제어 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-158">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="daedf-159">DPM 레지스트리 키 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager)에 WSS_Admin_WPG 그룹 읽기 액세스 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-159">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="daedf-160">SharePoint 팜 관리자 자격 증명의 변경이 있을 때마다 ConfigureSharePoint.exe를 다시 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-160">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="daedf-161">MABS를 사용하여 SharePoint 팜 백업</span><span class="sxs-lookup"><span data-stu-id="daedf-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="daedf-162">이전의 설명에 따라 MABS 및 SharePoint 팜을 구성한 후에는, SharePoint를 MABS로 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-162">After you have configured MABS and the SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="daedf-163">SharePoint 팜을 보호하려면</span><span class="sxs-lookup"><span data-stu-id="daedf-163">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="daedf-164">MABS 관리자 콘솔의 **보호**탭에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-164">From the **Protection** tab of the MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="daedf-165">![새 보호 탭](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="daedf-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="daedf-166">**새 보호 그룹 만들기** 마법사의 **보호 그룹 종류 선택** 페이지에서, **서버**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-166">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![선택하는 보호 그룹 종류](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="daedf-168">**그룹 구성원 선택** 화면에서, 보호할 SharePoint 서버의 확인란을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-168">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>

    ![그룹 구성원 선택](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="daedf-170">보호 에이전트를 설치하면, 마법사에서 서버를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-170">With the protection agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="daedf-171">또한 MABS에서는 해당 구조를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-171">MABS also shows its structure.</span></span> <span data-ttu-id="daedf-172">ConfigureSharePoint.exe를 실행했기 때문에, MABS가 SharePoint VSS 기록기 서비스 및 해당 SQL Server 데이터베이스와 통신하고 SharePoint 팜 구조, 연결된 콘텐츠 데이터베이스 및 모든 해당 항목을 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-172">Because you ran ConfigureSharePoint.exe, MABS communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="daedf-173">**데이터 보호 방법 선택** 페이지에서 **보호 그룹**의 이름을 입력하고 선호하는 *보호 방법*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-173">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="daedf-174">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-174">Click **Next**.</span></span>

    ![데이터 보호 방법 선택](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="daedf-176">디스크 보호 방법은 짧은 복구 시간 목표를 충족하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-176">The disk protection method helps to meet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="daedf-177">**단기 목표 지정** 페이지에서, 원하는 **보존 범위**를 선택하고 백업을 수행할 때를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-177">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>

    ![단기 목표 지정](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="daedf-179">이 예제의 경우, 대부분의 복구가 경과된 지 5일이 안된 데이터에 대해 요구되므로, 디스크의 보존 범위를 5일로 선택했고 백업은 프로덕션 시간을 피해 수행되도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="daedf-180">보호 그룹에 할당된 저장소 풀 디스크 공간을 검토하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-180">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="daedf-181">모든 보호 그룹에 대해 MABS는 복사본을 저장하고 관리하기 위해 디스크 공간을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-181">For every protection group, MABS allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="daedf-182">이 시점에서, MABS는 선택된 데이터의 복사본을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-182">At this point, MABS must create a copy of the selected data.</span></span> <span data-ttu-id="daedf-183">복사본을 만들 방법 및 날짜를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-183">Select how and when you want the replica created, and then click **Next**.</span></span>

    ![복제본 만들기 방법 선택](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="daedf-185">네트워크 트래픽에 영향을 주지 않기 위해, 프로덕션 시간을 피해 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-185">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="daedf-186">MABS는 복사본에서 일관성 확인을 수행하여 데이터 무결성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-186">MABS ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="daedf-187">사용할 수 있는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-187">There are two available options.</span></span> <span data-ttu-id="daedf-188">일관성 확인을 실행하는 일정을 정의하거나 복제본이 일관되지 않을 때마다 DPM이 복제본에 자동으로 일관성 확인을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-188">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="daedf-189">원하는 옵션을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-189">Select your preferred option, and then click **Next**.</span></span>

    ![일관성 확인](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="daedf-191">**온라인 보호 데이터 지정** 페이지에서 보호할 SharePoint 팜을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-191">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="daedf-193">**온라인 백업 일정 지정** 페이지에서 선호하는 일정을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-193">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="daedf-195">MABS는 사용 가능한 최신 디스크 백업 지점에서 Azure에 최대 두 번의 일일 백업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-195">MABS provides a maximum of two daily backups to Azure from the then available latest disk backup point.</span></span> <span data-ttu-id="daedf-196">Azure 백업은 [Azure Backup 네트워크 제한](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling)을 사용하여 사용량이 최고인 시간과 적은 시간의 백업에 사용될 수 있는 WAN 대역폭 양을 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-196">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="daedf-197">선택한 백업 일정에 따라 **온라인 보존 정책을 지정** 페이지에서 매일, 매주, 매월 및 매년 백업 지점에 대한 보존 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-197">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="daedf-199">MABS는 다른 백업 지점에 대해 다른 보전 정책을 사용하는 조부-아버지-아들 보존 체계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="daedf-200">디스크와 마찬가지로, Azure에서 초기 참조 지점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-200">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="daedf-201">Azure에 대한 초기 백업 복사본을 만드는 옵션을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-201">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="daedf-203">**요약** 페이지에서 선택한 설정을 검토하고 **그룹 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-203">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="daedf-204">보호 그룹이 생성된 후에 성공 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-204">You will see a success message after the protection group has been created.</span></span>

    ![요약](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="daedf-206">MABS를 사용하여 디스크에서 SharePoint 항목 복원</span><span class="sxs-lookup"><span data-stu-id="daedf-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="daedf-207">아래 예제에서는 실수로 삭제한 *SharePoint 복구 항목*을 복구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-207">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="daedf-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="daedf-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="daedf-209">**DPM 관리자 콘솔**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-209">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="daedf-210">DPM에서 보호되는 모든 SharePoint 팜이 **보호** 탭에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-210">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="daedf-212">항목 복구를 시작하려면 **복구** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-212">To begin to recover the item, select the **Recovery** tab.</span></span>

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="daedf-214">복구 지점 범위 내에서 와일드카드 기반 검색을 사용하여 *SharePoint 항목을 복구할* SharePoint를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="daedf-216">검색 결과에서 적절한 복구 지점을 선택하고, 마우스 오른쪽 단추로 클릭하여, **복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-216">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="daedf-217">다양한 복구 지점을 살펴보고 복구할 데이터베이스 또는 항목을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-217">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="daedf-218">**날짜 > 복구 시간**을 선택한 다음 올바른 **데이터베이스 > SharePoint 팜 > 복구 지점 > 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-218">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="daedf-220">항목을 마우스 오른쪽 단추로 클릭하고 **복구**를 선택하여 **복구 마법사**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-220">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="daedf-221">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-221">Click **Next**.</span></span>

    ![복구 선택 사항 확인](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="daedf-223">수행할 복구 유형을 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-223">Select the type of recovery that you want to perform, and then click **Next**.</span></span>

    ![복구 유형](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="daedf-225">예제에서는 **원본 사이트에 복구** 를 선택하여, 원본 SharePoint 사이트에 항목이 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-225">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="daedf-226">사용할 **복구 프로세스** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-226">Select the **Recovery Process** that you want to use.</span></span>

   * <span data-ttu-id="daedf-227">SharePoint 팜이 변경되지 않고 복원 중인 복구 지점과 같은 경우 **복구 팜을 사용하지 않고 복구** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-227">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="daedf-228">SharePoint 팜 복구 지점이 생성 된 이후 변경 된 경우 **복구 팜을 사용 하 여 복구** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-228">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>

     ![복구 프로세스](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="daedf-230">임시로 데이터베이스를 복구할 스테이징 SQL Server 인스턴스 위치를 제공하고, 항목을 복구하기 위해 SharePoint를 실행하는 서버 및 MABS에 준비 파일 공유를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-230">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on MABS and the server that's running SharePoint to recover the item.</span></span>

    ![스테이징 위치 1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="daedf-232">MABS는 SharePoint 항목을 호스트하는 콘텐츠 데이터베이스를 임시 SQL Server 인스턴스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-232">MABS attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="daedf-233">콘텐츠 데이터베이스에서, MABS는 항목을 복구하여 MABS의 준비 파일 위치에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-233">From the content database, it recovers the item and puts it on the staging file location on MABS.</span></span> <span data-ttu-id="daedf-234">이제 준비 위치에 있는 복구된 항목을 SharePoint 팜의 준비 위치로 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-234">The recovered item that's on the staging location now needs to be exported to the staging location on the SharePoint farm.</span></span>

    ![스테이징 Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="daedf-236">**복구 옵션 지정**을 선택하고, SharePoint 팜에 보안 설정을 적용하거나 복구 지점의 보안 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-236">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="daedf-237">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-237">Click **Next**.</span></span>

    ![복구 옵션](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="daedf-239">네트워크 대역폭 사용량을 제한 하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-239">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="daedf-240">따라서 프로덕션 시간 동안 프로덕션 서버에 미치는 영향이 최소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-240">This minimizes impact to the production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="daedf-241">요약 정보를 검토하고 **복구** 를 클릭하여 파일 복구를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-241">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>

    ![복구 요약](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="daedf-243">이제 **MABS 관리자 콘솔**의 **모니터링** 탭을 선택하여 복구의 **상태**를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-243">Now select the **Monitoring** tab in the **MABS Administrator Console** to view the **Status** of the recovery.</span></span>

    ![복구 상태](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="daedf-245">이제 파일이 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-245">The file is now restored.</span></span> <span data-ttu-id="daedf-246">복원된 파일을 확인하려면 SharePoint 사이트를 새로 고침하세요.</span><span class="sxs-lookup"><span data-stu-id="daedf-246">You can refresh the SharePoint site to check the restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="daedf-247">DPM을 사용하여 Azure에서 SharePoint 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="daedf-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="daedf-248">SharePoint 콘텐츠 데이터베이스를 복구하려면, 다양한 복구 지점을 살펴보고(이전과 같이), 복원할 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-248">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="daedf-250">SharePoint 복구 지점을 두번 클릭하면 사용할 수 있는 SharePoint 카탈로그 정보가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-250">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="daedf-251">SharePoint 팜은 Azure에서 장기 보존으로 보호되기 때문에 MABS에서 사용할 수 있는 카탈로그 정보(메타데이터)가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-251">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="daedf-252">따라서, 지정 시간 SharePoint 콘텐츠 데이터베이스 복구가 필요할 때마다, SharePoint 팜 카탈로그를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-252">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="daedf-253">**카탈로그 다시 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-253">Click **Re-catalog**.</span></span>

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="daedf-255">**클라우드 카탈로그 다시 만들기** 상태 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-255">The **Cloud Recatalog** status window opens.</span></span>

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="daedf-257">카탈로그 만들기가 완료되면, 상태가 *성공*으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-257">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="daedf-258">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-258">Click **Close**.</span></span>

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="daedf-260">MABS **복구** 탭의 SharePoint 개체를 클릭하여 콘텐츠 데이터베이스 구조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-260">Click the SharePoint object shown in the MABS **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="daedf-261">항목을 마우스 오른쪽 단추로 클릭한 다음 **복구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-261">Right-click the item, and then click **Recover**.</span></span>

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="daedf-263">이 지점에서 [이 문서 앞쪽의 복구 단계](#restore-a-sharepoint-item-from-disk-using-dpm) 를 수행하여 디스크에서 SharePoint 콘텐츠 데이터베이스를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-263">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="daedf-264">FAQ</span><span class="sxs-lookup"><span data-stu-id="daedf-264">FAQs</span></span>
<span data-ttu-id="daedf-265">Q: SharePoint가 SQL AlwaysOn을 사용하여 구성된 경우(디스크 보호를 사용하여), SharePoint 항목을 원본 위치로 복구할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="daedf-265">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="daedf-266">A: 예, 항목을 원본 SharePoint 사이트로 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-266">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="daedf-267">Q: SharePoint가 SQL AlwaysOn을 사용하여 구성된 경우 SharePoint 데이터베이스를 원본 위치로 복구할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="daedf-267">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="daedf-268">A: SharePoint 데이터베이스가 SQL AlwaysOn 에서 구성되었으므로, 가용성 그룹을 제거하지 않으면 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="daedf-269">따라서 MABS는 원래 위치로 데이터베이스를 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-269">As a result, MABS cannot restore a database to the original location.</span></span> <span data-ttu-id="daedf-270">SQL Server 데이터베이스를 다른 SQL Server 인스턴스로 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daedf-270">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daedf-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="daedf-271">Next steps</span></span>
* <span data-ttu-id="daedf-272">SharePoint의 MABS 보호에 대한 자세한 정보는 [SharePoint의 DPM 보호를 위한 비디오 시리즈](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="daedf-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
