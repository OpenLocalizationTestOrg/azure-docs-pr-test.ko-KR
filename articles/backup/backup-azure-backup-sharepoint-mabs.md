---
title: "SharePoint 팜 tooAzure Azure 백업 서버 tooback aaaUse | Microsoft Docs"
description: "Azure 백업 서버 tooback 사용 하 고 SharePoint 데이터를 복원 합니다. 이 문서는 원하는 데이터를 Azure에 저장할 수 있도록 SharePoint 팜을 hello 정보 tooconfigure를 제공 합니다. 디스크 또는 Azure에서 보호된 SharePoint 데이터를 복원할 수 있습니다."
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
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a><span data-ttu-id="fb090-105">SharePoint 팜 tooAzure 백업</span><span class="sxs-lookup"><span data-stu-id="fb090-105">Back up a SharePoint farm tooAzure</span></span>
<span data-ttu-id="fb090-106">SharePoint 백업 팜에 tooMicrosoft Azure 많은 hello에서 Microsoft Azure 백업 서버 (MABS)를 사용 하 여 다른 데이터 소스를 백업 하는 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-106">You back up a SharePoint farm tooMicrosoft Azure by using Microsoft Azure Backup Server (MABS) in much hello same way that you back up other data sources.</span></span> <span data-ttu-id="fb090-107">Azure 백업에서는 손쉽게 hello 백업 일정 toocreate 매일, 매주, 매월 또는 매년 백업 지점 및 다양 한 백업 지점에 대 한 보존 정책 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-107">Azure Backup provides flexibility in hello backup schedule toocreate daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="fb090-108">빠른 복구 시간 목표 (RTO)에 대 한 한 hello 기능 toostore 로컬 디스크 복사본을 제공 하 고 toostore tooAzure 경제적이 고, 장기 보존에 대 한 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-108">It also provides hello capability toostore local disk copies for quick recovery-time objectives (RTO) and toostore copies tooAzure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="fb090-109">SharePoint가 지원하는 버전 및 관련 보호 시나리오</span><span class="sxs-lookup"><span data-stu-id="fb090-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="fb090-110">DPM에 대 한 azure 백업을 hello 다음 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-110">Azure Backup for DPM supports hello following scenarios:</span></span>

| <span data-ttu-id="fb090-111">워크로드</span><span class="sxs-lookup"><span data-stu-id="fb090-111">Workload</span></span> | <span data-ttu-id="fb090-112">버전</span><span class="sxs-lookup"><span data-stu-id="fb090-112">Version</span></span> | <span data-ttu-id="fb090-113">SharePoint 배포</span><span class="sxs-lookup"><span data-stu-id="fb090-113">SharePoint deployment</span></span> | <span data-ttu-id="fb090-114">보호 및 복구</span><span class="sxs-lookup"><span data-stu-id="fb090-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="fb090-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="fb090-115">SharePoint</span></span> |<span data-ttu-id="fb090-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="fb090-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="fb090-117">SharePoint는 물리적 서버 또는 하이퍼-V/VMware 가상 컴퓨터로 배포됨 </span><span class="sxs-lookup"><span data-stu-id="fb090-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="fb090-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="fb090-118">SQL AlwaysOn</span></span> | <span data-ttu-id="fb090-119">SharePoint 팜 보호 복구 옵션: 복구 팜, 데이터베이스, 및 파일 또는 디스크 복구 지점의 목록 항목 </span><span class="sxs-lookup"><span data-stu-id="fb090-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="fb090-120">Azure 복구 지점에서 팜 및 데이터베이스 복구</span><span class="sxs-lookup"><span data-stu-id="fb090-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="fb090-121">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="fb090-121">Before you start</span></span>
<span data-ttu-id="fb090-122">몇 가지 방법으로 SharePoint 팜 tooAzure를 백업 하기 전에 tooconfirm 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-122">There are a few things you need tooconfirm before you back up a SharePoint farm tooAzure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fb090-123">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fb090-123">Prerequisites</span></span>
<span data-ttu-id="fb090-124">계속 진행 하기 전에 확인 했는지 [설치 하 고 hello Azure 백업 서버를 준비](backup-azure-microsoft-azure-backup.md) tooprotect 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-124">Before you proceed, make sure that you have [installed and prepared hello Azure Backup Server](backup-azure-microsoft-azure-backup.md) tooprotect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="fb090-125">보호 에이전트</span><span class="sxs-lookup"><span data-stu-id="fb090-125">Protection agent</span></span>
<span data-ttu-id="fb090-126">SharePoint, SQL Server를 실행 하는 hello 서버 및 다른 모든 서버 hello SharePoint 팜에 속하는 실행 하는 hello 서버의 hello 보호 에이전트를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-126">hello Protection agent must be installed on hello server that's running SharePoint, hello servers that are running SQL Server, and all other servers that are part of hello SharePoint farm.</span></span> <span data-ttu-id="fb090-127">방법에 대 한 자세한 내용은 hello 보호 에이전트를 tooset 참조 [보호 에이전트 설치](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-127">For more information about how tooset up hello protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="fb090-128">hello 한 가지 예외는 단일 웹 WFE (프런트 엔드) 서버에만 hello 에이전트를 설치 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-128">hello one exception is that you install hello agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="fb090-129">DPM 보호에 대 한 hello 진입점으로 하나의 WFE 서버만 tooserve hello 에이전트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-129">DPM needs hello agent on one WFE server only tooserve as hello entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="fb090-130">Sharepoint 팜</span><span class="sxs-lookup"><span data-stu-id="fb090-130">SharePoint farm</span></span>
<span data-ttu-id="fb090-131">Hello 팜의 모든 10 백만 항목에 대 한 최소 2GB의은 hello MABS 폴더가 있는 hello 볼륨에 공간 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-131">For every 10 million items in hello farm, there must be at least 2 GB of space on hello volume where hello MABS folder is located.</span></span> <span data-ttu-id="fb090-132">이 공간은 카탈로그를 생성하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-132">This space is required for catalog generation.</span></span> <span data-ttu-id="fb090-133">MABS toorecover 특정 항목 (사이트 모음, 사이트, 목록, 문서 라이브러리, 폴더, 개별 문서 및 목록 항목)에 대 한 카탈로그를 생성할 hello Url 각 콘텐츠 데이터베이스에 포함 된 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-133">For MABS toorecover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of hello URLs that are contained within each content database.</span></span> <span data-ttu-id="fb090-134">Hello에 hello 복구 가능한 항목 창에서 Url hello 목록을 볼 수 있습니다 **복구** 작업 MABS 관리자 콘솔의 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-134">You can view hello list of URLs in hello recoverable item pane in hello **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="fb090-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="fb090-135">SQL Server</span></span>
<span data-ttu-id="fb090-136">MABS는 LocalSystem 계정으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="fb090-137">SQL Server 데이터베이스를 tooback, MABS SQL Server를 실행 하는 hello 서버에 대 한 해당 계정에 대 한 sysadmin 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-137">tooback up SQL Server databases, MABS needs sysadmin privileges on that account for hello server that's running SQL Server.</span></span> <span data-ttu-id="fb090-138">NT AUTHORITY\SYSTEM을 너무 설정*sysadmin* 하기 전에 SQL Server를 실행 하는 hello 서버를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-138">Set NT AUTHORITY\SYSTEM too*sysadmin* on hello server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="fb090-139">Hello SharePoint 팜을 SQL Server 별칭으로 구성 된 SQL Server 데이터베이스에 있으면 MABS를 보호 하는 hello 프런트 엔드 웹 서버 hello SQL Server 클라이언트 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-139">If hello SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install hello SQL Server client components on hello front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="fb090-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="fb090-140">SharePoint Server</span></span>
<span data-ttu-id="fb090-141">성능은 SharePoint 팜의 크기와 같은 여러 요인에 따라 달라지지만, 일반 지침에 의하면 MABS 하나가 25TB SharePoint 팜을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="fb090-142">지원 되지않는 사항</span><span class="sxs-lookup"><span data-stu-id="fb090-142">What's not supported</span></span>
* <span data-ttu-id="fb090-143">SharePoint 팜을 보호하는 MABS는 검색 인덱스 또는 응용 프로그램 서비스 데이터베이스를 보호하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="fb090-144">개별적으로 이러한 데이터베이스의 tooconfigure hello 보호를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-144">You will need tooconfigure hello protection of these databases separately.</span></span>
* <span data-ttu-id="fb090-145">MABS는 스케일 아웃 파일 서버(SOFS) 공유에 호스트되는 SharePoint SQL Server 데이터베이스의 백업을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="fb090-146">SharePoint 보호 구성</span><span class="sxs-lookup"><span data-stu-id="fb090-146">Configure SharePoint protection</span></span>
<span data-ttu-id="fb090-147">사용 하 여 hello SharePoint VSS 기록기 서비스 (WSS 기록기 서비스)를 구성 해야 MABS tooprotect SharePoint를 사용 하려면 먼저 **ConfigureSharePoint.exe**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-147">Before you can use MABS tooprotect SharePoint, you must configure hello SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="fb090-148">찾을 수 있습니다 **ConfigureSharePoint.exe** hello 프런트 엔드 웹 서버 hello [MABS 설치 경로] \bin 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-148">You can find **ConfigureSharePoint.exe** in hello [MABS Installation Path]\bin folder on hello front-end web server.</span></span> <span data-ttu-id="fb090-149">이 도구는 hello SharePoint 팜에 대 한 hello 자격 증명으로 hello 보호 에이전트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-149">This tool provides hello protection agent with hello credentials for hello SharePoint farm.</span></span> <span data-ttu-id="fb090-150">단일 WFE 서버에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-150">You run it on a single WFE server.</span></span> <span data-ttu-id="fb090-151">WFE 서버가 여러 개인 경우, 보호 그룹을 구성할 때 하나만 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a><span data-ttu-id="fb090-152">tooconfigure hello SharePoint VSS 기록기 서비스</span><span class="sxs-lookup"><span data-stu-id="fb090-152">tooconfigure hello SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="fb090-153">명령 프롬프트에서 hello WFE 서버에서 이동 너무 [MABS 설치 위치] \bin\\</span><span class="sxs-lookup"><span data-stu-id="fb090-153">On hello WFE server, at a command prompt, go too[MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="fb090-154">ConfigureSharePoint -EnableSharePointProtection을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="fb090-155">Hello 팜 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-155">Enter hello farm administrator credentials.</span></span> <span data-ttu-id="fb090-156">이 계정은 hello hello WFE 서버에서 로컬 관리자 그룹의 구성원 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-156">This account should be a member of hello local Administrator group on hello WFE server.</span></span> <span data-ttu-id="fb090-157">팜 관리자에 게 다음 권한을 hello WFE 서버에서 로컬 관리자가 부여 hello 않다면,</span><span class="sxs-lookup"><span data-stu-id="fb090-157">If hello farm administrator isn’t a local admin grant hello following permissions on hello WFE server:</span></span>
   * <span data-ttu-id="fb090-158">Hello WSS_Admin_WPG 그룹 모든 권한 toohello DPM 폴더 (% Program Files%\Microsoft Azure Backup\DPM)을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-158">Grant hello WSS_Admin_WPG group full control toohello DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="fb090-159">Hello WSS_Admin_WPG 그룹 읽기 액세스 toohello DPM 레지스트리 키 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager)을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-159">Grant hello WSS_Admin_WPG group read access toohello DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="fb090-160">Hello SharePoint 팜 관리자 자격 증명이 변경 될 때마다 toorerun ConfigureSharePoint.exe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-160">You’ll need toorerun ConfigureSharePoint.exe whenever there’s a change in hello SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="fb090-161">MABS를 사용하여 SharePoint 팜 백업</span><span class="sxs-lookup"><span data-stu-id="fb090-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="fb090-162">MABS 및 hello 이전에 설명 된 대로 SharePoint 팜 구성 하 고 나면 MABS에서 SharePoint은 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-162">After you have configured MABS and hello SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="tooprotect-a-sharepoint-farm"></a><span data-ttu-id="fb090-163">SharePoint 팜에 tooprotect</span><span class="sxs-lookup"><span data-stu-id="fb090-163">tooprotect a SharePoint farm</span></span>
1. <span data-ttu-id="fb090-164">Hello에서 **보호** hello MABS 관리자 콘솔의 탭을 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-164">From hello **Protection** tab of hello MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="fb090-165">![새 보호 탭](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="fb090-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="fb090-166">Hello에 **보호 그룹 종류 선택** hello 페이지 **새 보호 그룹 만들기** 마법사, 선택 **서버**, 클릭 하 고 **다음** .</span><span class="sxs-lookup"><span data-stu-id="fb090-166">On hello **Select Protection Group Type** page of hello **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![선택하는 보호 그룹 종류](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="fb090-168">Hello에 **그룹 구성원 선택** 화면, 누르고 원하는 tooprotect hello SharePoint 서버에 대 한 확인란을 선택 하는 hello **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-168">On hello **Select Group Members** screen, select hello check box for hello SharePoint server you want tooprotect and click **Next**.</span></span>

    ![그룹 구성원 선택](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="fb090-170">Hello 보호 에이전트 설치를 사용 하면 hello 서버 hello 마법사에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-170">With hello protection agent installed, you can see hello server in hello wizard.</span></span> <span data-ttu-id="fb090-171">또한 MABS에서는 해당 구조를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-171">MABS also shows its structure.</span></span> <span data-ttu-id="fb090-172">ConfigureSharePoint.exe를 실행 하기 때문에 MABS hello SharePoint VSS 기록기 서비스와 해당 SQL Server 데이터베이스와 통신 하 고 hello SharePoint 팜 구조를 인식, hello 콘텐츠 데이터베이스 및 해당 항목에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-172">Because you ran ConfigureSharePoint.exe, MABS communicates with hello SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes hello SharePoint farm structure, hello associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="fb090-173">Hello에 **데이터 보호 방법 선택** 페이지의 hello hello 이름을 입력 **보호 그룹**, 원하는 선택 *보호 방법을*합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-173">On hello **Select Data Protection Method** page, enter hello name of hello **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="fb090-174">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-174">Click **Next**.</span></span>

    ![데이터 보호 방법 선택](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="fb090-176">hello 디스크 보호 방법 toomeet 짧은 복구 시간 목표를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-176">hello disk protection method helps toomeet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="fb090-177">Hello에 **단기 목표 지정** 페이지에서 원하는 **보존 범위** 백업을 toooccur 하려는 경우를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-177">On hello **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups toooccur.</span></span>

    ![단기 목표 지정](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="fb090-179">때문에 복구 가장 자주 5 일 보다 작은 데이터에 필요한, म 디스크에 5 일의 보존 범위를 선택 하 고이 예제에 대 한 비-프로덕션 시간 동안 발생 하는 hello 백업 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that hello backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="fb090-180">Hello 보호 그룹에 할당 된 hello 저장소 풀 디스크 공간을 검토 하 고 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-180">Review hello storage pool disk space allocated for hello protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="fb090-181">모든 보호 그룹에 대해 MABS 디스크 공간 toostore 할당 하 고 복제본을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-181">For every protection group, MABS allocates disk space toostore and manage replicas.</span></span> <span data-ttu-id="fb090-182">이 시점에서 MABS hello 선택한 데이터의 복사본을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-182">At this point, MABS must create a copy of hello selected data.</span></span> <span data-ttu-id="fb090-183">선택 방법 및 시기를 만든 hello 복제본을 클릭 한 다음 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-183">Select how and when you want hello replica created, and then click **Next**.</span></span>

    ![복제본 만들기 방법 선택](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="fb090-185">네트워크 트래픽에 영향을 받지 않습니다, 있는지 toomake 프로덕션 시간 외 시간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-185">toomake sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="fb090-186">MABS는 hello 복제본에 일관성 검사를 수행 하 여 데이터 무결성을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-186">MABS ensures data integrity by performing consistency checks on hello replica.</span></span> <span data-ttu-id="fb090-187">사용할 수 있는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-187">There are two available options.</span></span> <span data-ttu-id="fb090-188">정의한 일정 toorun 일관성 검사, 또는 DPM이 일관 되지 않을 때마다 hello 복제본에서 자동으로 일관성 확인을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-188">You can define a schedule toorun consistency checks, or DPM can run consistency checks automatically on hello replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="fb090-189">원하는 옵션을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-189">Select your preferred option, and then click **Next**.</span></span>

    ![일관성 확인](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="fb090-191">Hello에 **온라인 보호 데이터 지정** hello SharePoint 팜에 tooprotect를 원하고 클릭 한 다음 페이지에서 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-191">On hello **Specify Online Protection Data** page, select hello SharePoint farm that you want tooprotect, and then click **Next**.</span></span>

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="fb090-193">Hello에 **온라인 백업 일정 지정** 페이지 원하는 일정을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-193">On hello **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="fb090-195">MABS는 hello 최신 사용 가능한 디스크 백업 시점에서 두 개의 일별 백업 tooAzure 최대를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-195">MABS provides a maximum of two daily backups tooAzure from hello then available latest disk backup point.</span></span> <span data-ttu-id="fb090-196">Azure 백업 hello를 사용 하 여 최고 및 사용량이 적은 시간에 백업에 사용할 수 있는 WAN 대역폭 양을 제어할 수 [Azure 백업 네트워크 제한](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling)합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-196">Azure Backup can also control hello amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="fb090-197">Hello hello에서 선택한 백업 일정에 따라 **온라인 보존 정책 지정** 매일, 매주, 매월 및 매년 백업 지점에 대 한 보존 정책 선택 hello 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-197">Depending on hello backup schedule that you selected, on hello **Specify Online Retention Policy** page, select hello retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="fb090-199">MABS는 다른 백업 지점에 대해 다른 보전 정책을 사용하는 조부-아버지-아들 보존 체계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="fb090-200">비슷한 toodisk 초기 참조 지점 복제 데이터베이스를 Azure에서 만든 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-200">Similar toodisk, an initial reference point replica needs toobe created in Azure.</span></span> <span data-ttu-id="fb090-201">사용자 기본 설정된 옵션 toocreate 초기 백업 복사본이 tooAzure를 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-201">Select your preferred option toocreate an initial backup copy tooAzure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="fb090-203">Hello에서 선택한 설정을 검토 **요약** 페이지를 선택한 다음 클릭 **그룹 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-203">Review your selected settings on hello **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="fb090-204">Hello 보호 그룹을 만든 후 성공 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-204">You will see a success message after hello protection group has been created.</span></span>

    ![요약](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="fb090-206">MABS를 사용하여 디스크에서 SharePoint 항목 복원</span><span class="sxs-lookup"><span data-stu-id="fb090-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="fb090-207">다음 예제는 hello에서 hello *SharePoint 복구 항목* 실수로 삭제 하 고 복구 toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-207">In hello following example, hello *Recovering SharePoint item* has been accidentally deleted and needs toobe recovered.</span></span>
<span data-ttu-id="fb090-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="fb090-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="fb090-209">열기 hello **DPM 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-209">Open hello **DPM Administrator Console**.</span></span> <span data-ttu-id="fb090-210">DPM에서 보호 되는 모든 SharePoint 팜 hello에 표시 된 **보호** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-210">All SharePoint farms that are protected by DPM are shown in hello **Protection** tab.</span></span>

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="fb090-212">toobegin toorecover hello 항목을 선택 하는 hello **복구** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-212">toobegin toorecover hello item, select hello **Recovery** tab.</span></span>

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="fb090-214">복구 지점 범위 내에서 와일드카드 기반 검색을 사용하여 *SharePoint 항목을 복구할* SharePoint를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="fb090-216">Hello 검색 결과에서 hello 적절 한 복구 지점을 선택 hello 항목을 마우스 오른쪽 단추로 클릭 하 고 다음 선택 **복구**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-216">Select hello appropriate recovery point from hello search results, right-click hello item, and then select **Recover**.</span></span>
5. <span data-ttu-id="fb090-217">다양 한 복구 지점을 찾아보거나 수 있고 데이터베이스 또는 항목 toorecover 선택 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-217">You can also browse through various recovery points and select a database or item toorecover.</span></span> <span data-ttu-id="fb090-218">선택 **날짜 > 복구 시간**를 선택한 후 올바른 hello **데이터베이스 > SharePoint 팜에 > 복구 지점 > 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-218">Select **Date > Recovery time**, and then select hello correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="fb090-220">Hello 항목을 마우스 오른쪽 단추로 클릭 한 다음 선택 **복구** tooopen hello **복구 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-220">Right-click hello item, and then select **Recover** tooopen hello **Recovery Wizard**.</span></span> <span data-ttu-id="fb090-221">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-221">Click **Next**.</span></span>

    ![복구 선택 사항 확인](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="fb090-223">Hello 유형의 recovery tooperform를 선택 하 고 클릭 한 다음 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-223">Select hello type of recovery that you want tooperform, and then click **Next**.</span></span>

    ![복구 유형](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="fb090-225">선택 hello **toooriginal 복구** hello의 예제는 hello 항목 toohello 원래 SharePoint 사이트를 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-225">hello selection of **Recover toooriginal** in hello example recovers hello item toohello original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="fb090-226">선택 hello **복구 프로세스** toouse 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-226">Select hello **Recovery Process** that you want toouse.</span></span>

   * <span data-ttu-id="fb090-227">선택 **복구 팜을 사용 하지 않고 복구** hello SharePoint 팜에 변경 되지 않은 경우 및 해당 하는 지점 hello 복구 동일 hello 복원 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-227">Select **Recover without using a recovery farm** if hello SharePoint farm has not changed and is hello same as hello recovery point that is being restored.</span></span>
   * <span data-ttu-id="fb090-228">선택 **복구 팜을 사용 하 여 복구** hello SharePoint 팜에 hello 복구 지점이 만들어진 후 변경 된 경우.</span><span class="sxs-lookup"><span data-stu-id="fb090-228">Select **Recover using a recovery farm** if hello SharePoint farm has changed since hello recovery point was created.</span></span>

     ![복구 프로세스](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="fb090-230">준비 SQL Server 인스턴스 위치 toorecover hello 데이터베이스를 일시적으로 제공 하 고 SharePoint toorecover hello 항목을 실행 하는 MABS 및 hello 서버에 파일 공유 준비를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-230">Provide a staging SQL Server instance location toorecover hello database temporarily, and provide a staging file share on MABS and hello server that's running SharePoint toorecover hello item.</span></span>

    ![스테이징 위치 1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="fb090-232">MABS는 hello SharePoint 항목 toohello 임시 SQL Server 인스턴스를 호스팅하는 hello 콘텐츠 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-232">MABS attaches hello content database that is hosting hello SharePoint item toohello temporary SQL Server instance.</span></span> <span data-ttu-id="fb090-233">Hello 콘텐츠 데이터베이스에서이 클래스는 hello 항목을 복구 하 hello 스테이징 MABS에서 파일 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-233">From hello content database, it recovers hello item and puts it on hello staging file location on MABS.</span></span> <span data-ttu-id="fb090-234">hello 요구 내보낸 toobe toohello 스테이징 위치 hello SharePoint 팜에서 hello 이제 스테이징 위치에 있는 항목을 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-234">hello recovered item that's on hello staging location now needs toobe exported toohello staging location on hello SharePoint farm.</span></span>

    ![스테이징 Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="fb090-236">선택 **복구 옵션 지정**, 및 보안 설정을 toohello SharePoint 팜에 적용 또는 hello 복구 지점의 hello 보안 설정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-236">Select **Specify recovery options**, and apply security settings toohello SharePoint farm or apply hello security settings of hello recovery point.</span></span> <span data-ttu-id="fb090-237">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-237">Click **Next**.</span></span>

    ![복구 옵션](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="fb090-239">Toothrottle hello 네트워크 대역폭 사용을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-239">You can choose toothrottle hello network bandwidth usage.</span></span> <span data-ttu-id="fb090-240">이 영향 toohello 프로덕션 서버 프로덕션 많은 시간을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-240">This minimizes impact toohello production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="fb090-241">Hello 요약 정보를 검토 한 다음 클릭 **복구** hello 파일의 toobegin 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-241">Review hello summary information, and then click **Recover** toobegin recovery of hello file.</span></span>

    ![복구 요약](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="fb090-243">이제 선택 하는 hello **모니터링** hello 탭 **MABS 관리자 콘솔** tooview hello **상태** hello 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-243">Now select hello **Monitoring** tab in hello **MABS Administrator Console** tooview hello **Status** of hello recovery.</span></span>

    ![복구 상태](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="fb090-245">이제 hello 파일 복원 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-245">hello file is now restored.</span></span> <span data-ttu-id="fb090-246">Hello SharePoint 사이트 toocheck hello 복원 파일을 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-246">You can refresh hello SharePoint site toocheck hello restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="fb090-247">DPM을 사용하여 Azure에서 SharePoint 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="fb090-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="fb090-248">SharePoint 콘텐츠 데이터베이스 toorecover 다양 한 복구 지점 (이전에 표시)으로, toorestore 원하는 hello 복구 지점을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-248">toorecover a SharePoint content database, browse through various recovery points (as shown previously), and select hello recovery point that you want toorestore.</span></span>

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="fb090-250">Hello SharePoint 복구 지점 tooshow hello 사용 가능한 SharePoint 카탈로그 정보를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-250">Double-click hello SharePoint recovery point tooshow hello available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fb090-251">Azure에서 장기 보존을 위해 hello SharePoint 팜에서 보호 되므로 카탈로그 비워진 (메타 데이터)를 MABS 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-251">Because hello SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="fb090-252">결과적으로, 지정 시간 SharePoint 콘텐츠 데이터베이스 복구 toobe, 필요할 때마다 있습니다 toocatalog hello SharePoint 팜에 다시 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-252">As a result, whenever a point-in-time SharePoint content database needs toobe recovered, you need toocatalog hello SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="fb090-253">**카탈로그 다시 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-253">Click **Re-catalog**.</span></span>

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="fb090-255">hello **클라우드 카탈로그를 다시** 상태 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-255">hello **Cloud Recatalog** status window opens.</span></span>

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="fb090-257">Hello 상태가 너무 변경 카탈로그 만들기를 완료 한 후*성공*합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-257">After cataloging is finished, hello status changes too*Success*.</span></span> <span data-ttu-id="fb090-258">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-258">Click **Close**.</span></span>

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="fb090-260">MABS hello에 표시 되는 hello SharePoint 개체 클릭 **복구** tooget hello 콘텐츠 데이터베이스 구조를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-260">Click hello SharePoint object shown in hello MABS **Recovery** tab tooget hello content database structure.</span></span> <span data-ttu-id="fb090-261">Hello 항목을 마우스 오른쪽 단추로 누른 **복구**합니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-261">Right-click hello item, and then click **Recover**.</span></span>

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="fb090-263">이 시점에서 hello에 따라 [이 문서의 앞부분에서 복구 단계](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover 디스크에서 SharePoint 콘텐츠 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-263">At this point, follow hello [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="fb090-264">FAQ</span><span class="sxs-lookup"><span data-stu-id="fb090-264">FAQs</span></span>
<span data-ttu-id="fb090-265">Q: 수 복구 SharePoint 항목 toohello 원래 위치 (디스크 보호)로 SQL AlwaysOn을 사용 하 여 SharePoint를 구성한 경우?</span><span class="sxs-lookup"><span data-stu-id="fb090-265">Q: Can I recover a SharePoint item toohello original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="fb090-266">A: 예, hello 항목 복구 된 toohello 원래 SharePoint 사이트 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-266">A: Yes, hello item can be recovered toohello original SharePoint site.</span></span>

<span data-ttu-id="fb090-267">Q: 수 복구 SharePoint 데이터베이스 toohello 원래 위치로 SQL AlwaysOn을 사용 하 여 SharePoint를 구성한 경우?</span><span class="sxs-lookup"><span data-stu-id="fb090-267">Q: Can I recover a SharePoint database toohello original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="fb090-268">A: 하기 때문에 SharePoint 데이터베이스는 SQL AlwaysOn으로 구성 된 hello 가용성 그룹을 제거 하지 않으면 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless hello availability group is removed.</span></span> <span data-ttu-id="fb090-269">결과적으로, MABS 데이터베이스 toohello 원래 위치를 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-269">As a result, MABS cannot restore a database toohello original location.</span></span> <span data-ttu-id="fb090-270">SQL Server 데이터베이스 tooanother SQL Server 인스턴스를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb090-270">You can recover a SQL Server database tooanother SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb090-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fb090-271">Next steps</span></span>
* <span data-ttu-id="fb090-272">SharePoint의 MABS 보호에 대한 자세한 정보는 [SharePoint의 DPM 보호를 위한 비디오 시리즈](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb090-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
