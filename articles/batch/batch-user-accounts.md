---
title: "Azure 일괄 처리에서 사용자 계정 aaaRun 작업 | Microsoft Docs"
description: "Azure 배치에서 태스크를 실행하기 위해 사용자 계정 구성"
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="e0fc3-103">배치에서 사용자 계정으로 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="e0fc3-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="e0fc3-104">Azure 배치의 태스크는 항상 사용자 계정으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="e0fc3-105">기본적으로 태스크는 관리자 권한 없이 표준 사용자 계정으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="e0fc3-106">일반적으로는 이러한 기본 사용자 계정 설정만으로 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="e0fc3-107">그러나 특정 시나리오에 대 한 유용한 toobe 수 tooconfigure hello 사용자 계정 작업 toorun 원하는 것.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-107">For certain scenarios, however, it's useful toobe able tooconfigure hello user account under which you want a task toorun.</span></span> <span data-ttu-id="e0fc3-108">이 문서에서는 hello 유형의 사용자 계정 및 구성 하는 방법으로 시나리오에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-108">This article discusses hello types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="e0fc3-109">사용자 계정의 유형</span><span class="sxs-lookup"><span data-stu-id="e0fc3-109">Types of user accounts</span></span>

<span data-ttu-id="e0fc3-110">Azure 배치에서는 태스크 실행을 위해 다음과 같은 두 가지 유형의 사용자 계정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="e0fc3-111">**자동 사용자 계정.**</span><span class="sxs-lookup"><span data-stu-id="e0fc3-111">**Auto-user accounts.**</span></span> <span data-ttu-id="e0fc3-112">자동 사용자 계정은 기본 제공 사용자 하는 계정 hello 일괄 처리 서비스에서 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-112">Auto-user accounts are built-in user accounts that are created automatically by hello Batch service.</span></span> <span data-ttu-id="e0fc3-113">기본적으로 태스크는 자동 사용자 계정에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="e0fc3-114">자동-사용자 계정 작업을 실행할 작업 tooindicate에 대 한 자동 사용자 사양이 hello를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-114">You can configure hello auto-user specification for a task tooindicate under which auto-user account a task should run.</span></span> <span data-ttu-id="e0fc3-115">hello 자동 사용자 사양에는 toospecify hello 상승 수준 및 범위 hello 작업을 실행 하는 hello 자동 사용자 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-115">hello auto-user specification allows you toospecify hello elevation level and scope of hello auto-user account that will run hello task.</span></span> 

- <span data-ttu-id="e0fc3-116">**명명된 사용자 계정.**</span><span class="sxs-lookup"><span data-stu-id="e0fc3-116">**A named user account.**</span></span> <span data-ttu-id="e0fc3-117">하나 이상의 명명 된 사용자 계정 풀에 대 한 hello 풀을 만들 때 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-117">You can specify one or more named user accounts for a pool when you create hello pool.</span></span> <span data-ttu-id="e0fc3-118">각 사용자 계정이 hello 풀의 각 노드에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-118">Each user account is created on each node of hello pool.</span></span> <span data-ttu-id="e0fc3-119">Toohello 계정 이름 또한 수준에서는, Linux 풀, hello SSH 개인 키에 대 한 상승 hello 사용자 계정 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-119">In addition toohello account name, you specify hello user account password, elevation level, and, for Linux pools, hello SSH private key.</span></span> <span data-ttu-id="e0fc3-120">작업을 추가 하는 경우 해당 태스크를 실행 하는 사용자 계정 이라는 hello를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-120">When you add a task, you can specify hello named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e0fc3-121">hello 일괄 처리 서비스 버전 2017-01-01.4.0 업데이트 하 여 코드 toocall 해당 버전을 필요로 하는 주요 변경 내용를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-121">hello Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code toocall that version.</span></span> <span data-ttu-id="e0fc3-122">일괄 처리의 이전 버전에서 마이그레이션 코드 인 경우 해당 hello 참고 **runElevated** 속성은 더 이상 hello REST API 또는 일괄 처리 클라이언트 라이브러리에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-122">If you are migrating code from an older version of Batch, note that hello **runElevated** property is no longer supported in hello REST API or Batch client libraries.</span></span> <span data-ttu-id="e0fc3-123">새 사용 하 여 hello **userIdentity** 작업 toospecify 상승 수준의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-123">Use hello new **userIdentity** property of a task toospecify elevation level.</span></span> <span data-ttu-id="e0fc3-124">Hello 단원을 참조 [코드 toohello 최신 일괄 처리 클라이언트 라이브러리 업데이트](#update-your-code-to-the-latest-batch-client-library) hello 클라이언트 라이브러리 중 하나를 사용 하는 경우 일괄 처리 코드를 업데이트 하는 것에 대 한 빠른 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-124">See hello section titled [Update your code toohello latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of hello client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="e0fc3-125">이 문서에서 설명 하는 hello 사용자 계정을 보안상의 이유로 프로토콜 RDP (원격 데스크톱) 또는 SSH (보안 셸)를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-125">hello user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="e0fc3-126">tooconnect tooa 노드 실행 중인 hello Linux 가상 컴퓨터 구성, SSH 통해 참조 [원격 데스크톱을 사용 하 여 Azure에서 Linux VM tooa](../virtual-machines/virtual-machines-linux-use-remote-desktop.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-126">tooconnect tooa node running hello Linux virtual machine configuration via SSH, see [Use Remote Desktop tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="e0fc3-127">RDP를 통해 Windows를 실행 하는 tooconnect toonodes 참조 [tooa Windows Server VM을 연결](../virtual-machines/windows/connect-logon.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-127">tooconnect toonodes running Windows via RDP, see [Connect tooa Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="e0fc3-128">tooconnect tooa 노드 실행 중인 hello 클라우드 서비스 구성 RDP 통해 참조 [Azure 클라우드 서비스에서 역할에 대 한 원격 데스크톱 연결을 사용 하도록 설정](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-128">tooconnect tooa node running hello cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-toofiles-and-directories"></a><span data-ttu-id="e0fc3-129">사용자 계정 액세스 toofiles 및 디렉터리</span><span class="sxs-lookup"><span data-stu-id="e0fc3-129">User account access toofiles and directories</span></span>

<span data-ttu-id="e0fc3-130">자동 사용자 계정을 명명 된 사용자 계정에는 읽기/쓰기 액세스 toohello 작업의 작업 디렉터리, 공유 디렉터리 및 다중 인스턴스 작업 디렉터리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-130">Both an auto-user account and a named user account have read/write access toohello task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="e0fc3-131">두 종류의 계정에 대 한 읽기 액세스 toohello 시작 및 작업 준비 디렉터리가 있을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-131">Both types of accounts have read access toohello startup and job preparation directories.</span></span>

<span data-ttu-id="e0fc3-132">Hello 작업이 실행 되는 경우 시작 작업, hello 작업을 실행 하는 데 사용 된 동일한 계정에 읽기 / 쓰기 액세스 toohello 시작 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-132">If a task runs under hello same account that was used for running a start task, hello task has read-write access toohello start task directory.</span></span> <span data-ttu-id="e0fc3-133">마찬가지로, 작업으로 실행 되 면 hello 동일한 태스크를 준비 하는 작업, hello 작업을 실행 하는 데 사용 된 계정에 읽기 / 쓰기 액세스 toohello 작업 준비 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-133">Similarly, if a task runs under hello same account that was used for running a job preparation task, hello task has read-write access toohello job preparation task directory.</span></span> <span data-ttu-id="e0fc3-134">Hello 시작 태스크 또는 태스크를 준비 하는 작업 보다 다른 계정에서 실행 되는 작업 하는 경우 hello 작업에만 읽기 toohello 해당 디렉터리에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-134">If a task runs under a different account than hello start task or job preparation task, then hello task has only read access toohello respective directory.</span></span>

<span data-ttu-id="e0fc3-135">태스크에서 파일 및 디렉터리 액세스에 대한 자세한 내용은 [배치를 사용하여 대규모 병렬 계산 솔루션 개발](batch-api-basics.md#files-and-directories)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="e0fc3-136">태스크에 대한 관리자 권한 액세스</span><span class="sxs-lookup"><span data-stu-id="e0fc3-136">Elevated access for tasks</span></span> 

<span data-ttu-id="e0fc3-137">hello 사용자 계정의 권한 상승을 수준 작업 액세스 권한으로 실행 되는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-137">hello user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="e0fc3-138">자동 사용자 계정 및 명명된 사용자 계정 모두 관리자 권한 액세스로 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="e0fc3-139">권한 상승 수준 hello 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-139">hello two options for elevation level are:</span></span>

- <span data-ttu-id="e0fc3-140">**NonAdmin:** hello 작업 상승 된 액세스 권한이 없는 표준 사용자로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-140">**NonAdmin:** hello task runs as a standard user without elevated access.</span></span> <span data-ttu-id="e0fc3-141">일괄 처리 사용자 계정에 대 한 기본 권한 상승 수준 hello는 항상 **NonAdmin**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-141">hello default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="e0fc3-142">**Admin:** hello 작업 상승 된 액세스 권한이 있는 사용자로 실행 하 고 모든 관리자 권한을 사용 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-142">**Admin:** hello task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="e0fc3-143">자동 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="e0fc3-143">Auto-user accounts</span></span>

<span data-ttu-id="e0fc3-144">기본적으로 태스크는 자동 사용자 계정에서 배치로, 관리자 액세스 권한이 없는 표준 사용자로, 태스크 범위를 사용해서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="e0fc3-145">Hello 자동 사용자 사양 작업 범위를 구성 된 경우 hello 일괄 처리 서비스에만 해당 작업에 대 한 자동 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-145">When hello auto-user specification is configured for task scope, hello Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="e0fc3-146">hello 대체 tootask 범위는 풀 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-146">hello alternative tootask scope is pool scope.</span></span> <span data-ttu-id="e0fc3-147">풀 범위에 대해 구성 된 작업에 대 한 자동 사용자 사양이 hello hello 작업 hello 풀에서 사용할 수 있는 tooany 작업은 자동 사용자 계정에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-147">When hello auto-user specification for a task is configured for pool scope, hello task runs under an auto-user account that is available tooany task in hello pool.</span></span> <span data-ttu-id="e0fc3-148">풀 범위에 대 한 자세한 내용은 hello 섹션을 참조 하십시오. [hello 풀 범위를 갖는 자동 사용자 작업 실행](#run-a-task-as-the-autouser-with-pool-scope)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-148">For more information about pool scope, see hello section titled [Run a task as hello auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="e0fc3-149">hello 기본 범위는 Windows 및 Linux 노드에 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-149">hello default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="e0fc3-150">Windows 노드에서 태스크는 기본적으로 태스크 범위 내에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="e0fc3-151">Linux 노드는 항상 풀 범위에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="e0fc3-152">Hello 자동 사용자 지정을 대응 tooa 고유한 자동 사용자 계정에 대 한 4 가지 가능한 구성이 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-152">There are four possible configurations for hello auto-user specification, each of which corresponds tooa unique auto-user account:</span></span>

- <span data-ttu-id="e0fc3-153">작업 범위 (hello 기본 자동 사용자 사양)를 갖는 non-admin 인 액세스</span><span class="sxs-lookup"><span data-stu-id="e0fc3-153">Non-admin access with task scope (hello default auto-user specification)</span></span>
- <span data-ttu-id="e0fc3-154">태스크 범위를 사용하는 관리자(상승된 권한) 액세스</span><span class="sxs-lookup"><span data-stu-id="e0fc3-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="e0fc3-155">풀 범위를 사용하는 비관리자 액세스</span><span class="sxs-lookup"><span data-stu-id="e0fc3-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="e0fc3-156">풀 범위를 사용하는 관리자 액세스</span><span class="sxs-lookup"><span data-stu-id="e0fc3-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e0fc3-157">작업 범위에서 실행 되는 작업의 실제 액세스 tooother 작업 노드에서 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-157">Tasks running under task scope do not have de facto access tooother tasks on a node.</span></span> <span data-ttu-id="e0fc3-158">그러나 액세스 toohello 계정 사용 하 여 악의적인 사용자는 관리자 권한으로 실행 되 고 다른 작업 디렉터리에 액세스 하는 작업을 제출 하 여이 제한을 해결할 작동 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-158">However, a malicious user with access toohello account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="e0fc3-159">악의적인 사용자가 RDP 또는 SSH tooconnect tooa 노드를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-159">A malicious user could also use RDP or SSH tooconnect tooa node.</span></span> <span data-ttu-id="e0fc3-160">중요 한 tooprotect 액세스 tooyour 일괄 처리 계정 키 tooprevent 이러한 시나리오는</span><span class="sxs-lookup"><span data-stu-id="e0fc3-160">It's important tooprotect access tooyour Batch account keys tooprevent such a scenario.</span></span> <span data-ttu-id="e0fc3-161">사용자의 계정이 노출 의심 되는 경우 있는지 tooregenerate 키 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-161">If you suspect your account may have been compromised, be sure tooregenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="e0fc3-162">관리자 액세스 권한이 있는 자동 사용자로 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="e0fc3-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="e0fc3-163">관리자 권한에 대 한 자동 사용자 사양 hello toorun 상승 된 액세스 권한이 있는 작업을 할 때 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-163">You can configure hello auto-user specification for administrator privileges when you need toorun a task with elevated access.</span></span> <span data-ttu-id="e0fc3-164">예를 들어 시작 태스크 hello 노드에서 tooinstall 소프트웨어 상승 된 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-164">For example, a start task may need elevated access tooinstall software on hello node.</span></span>

> [!NOTE] 
> <span data-ttu-id="e0fc3-165">일반적으로 것이 가장 좋습니다 toouse 더 높은 필요한 경우에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-165">In general, it's best toouse elevated access only when necessary.</span></span> <span data-ttu-id="e0fc3-166">최적의는 hello 최소 권한 필요한 tooachieve hello 원하는 결과 부여 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-166">Best practices recommend granting hello minimum privilege necessary tooachieve hello desired outcome.</span></span> <span data-ttu-id="e0fc3-167">예를 들어 시작 태스크가 모든 사용자를 대신 hello 현재 사용자에 대 한 소프트웨어를 설치 하는 경우에 tootasks 상승 된 액세스를 부여 하는 수 tooavoid을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-167">For example, if a start task installs software for hello current user, instead of for all users, you may be able tooavoid granting elevated access tootasks.</span></span> <span data-ttu-id="e0fc3-168">풀 범위와 관리자가 아닌 toorun hello hello 시작 태스크를 포함 하 여 동일한 계정에서 필요로 하는 모든 작업에 대 한 액세스에 대 한 자동 사용자 사양이 hello를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-168">You can configure hello auto-user specification for pool scope and non-admin access for all tasks that need toorun under hello same account, including hello start task.</span></span> 
>
>

<span data-ttu-id="e0fc3-169">다음 코드 조각 hello tooconfigure 자동 사용자 사양 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-169">hello following code snippets show how tooconfigure hello auto-user specification.</span></span> <span data-ttu-id="e0fc3-170">hello 예제 설정 hello 상승 수준 너무`Admin` 범위를 너무 hello 및`Task`합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-170">hello examples set hello elevation level too`Admin` and hello scope too`Task`.</span></span> <span data-ttu-id="e0fc3-171">작업 범위는 hello 기본 설정 이지만 여기 예제의 hello 위해서 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-171">Task scope is hello default setting, but is included here for hello sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="e0fc3-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="e0fc3-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="e0fc3-173">Batch Java</span><span class="sxs-lookup"><span data-stu-id="e0fc3-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="e0fc3-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="e0fc3-174">Batch Python</span></span>

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="e0fc3-175">풀 범위가 지정된 자동 사용자로 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="e0fc3-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="e0fc3-176">노드를 프로 비전 하는 경우 두 개의 풀 전체의 자동 사용자 계정은 hello 풀의 각 노드에, 관리자 권한 액세스를 사용 하 여 권한이 상승된 액세스 하지 않고에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in hello pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="e0fc3-177">지정된 된 태스크에 대 한 hello 자동-사용자의 범위 toopool 범위 설정가 이러한 두 풀 전체의 자동 사용자 계정 중 하나로 hello 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-177">Setting hello auto-user's scope toopool scope for a given task runs hello task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="e0fc3-178">Hello에서 관리자 권한으로 실행 하는 모든 작업 실행 hello 자동 사용자에 대 한 풀 범위를 지정 하면 동일한 풀 전체의 자동-사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-178">When you specify pool scope for hello auto-user, all tasks that run with administrator access run under hello same pool-wide auto-user account.</span></span> <span data-ttu-id="e0fc3-179">마찬가지로 관리자 권한 없이 실행되는 태스크도 단일 풀 전체 자동 사용자 계정에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="e0fc3-180">hello 두 풀 전체의 자동 사용자 계정이 별도 계정이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-180">hello two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="e0fc3-181">Hello 풀 전체의 관리 계정에서 실행 되는 작업은 그 반대의 hello 표준 계정으로 실행 되는 작업으로 데이터를 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-181">Tasks running under hello pool-wide administrative account cannot share data with tasks running under hello standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="e0fc3-182">동일한 자동 사용자 계정이 사용 되는 작업 hello에서 실행 중인 다른 작업을 사용 하 여 수 tooshare 데이터 hello에서 장점은 toorunning hello 동일한 노드.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-182">hello advantage toorunning under hello same auto-user account is that tasks are able tooshare data with other tasks running on hello same node.</span></span>

<span data-ttu-id="e0fc3-183">작업 간에 비밀을 공유 실행 중인 작업 2 hello 풀 전체의 자동-사용자 계정 중 하나는 유용 시나리오 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-183">Sharing secrets between tasks is one scenario where running tasks under one of hello two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="e0fc3-184">예를 들어 시작 작업 tooprovision hello 노드에 다른 작업에서 사용할 수 있는 암호 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-184">For example, suppose a start task needs tooprovision a secret onto hello node that other tasks can use.</span></span> <span data-ttu-id="e0fc3-185">Windows API DPAPI (데이터 보호), hello를 사용할 수 있지만 이러한은 관리자 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-185">You could use hello Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="e0fc3-186">대신, hello 비밀 hello 사용자 수준에서 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-186">Instead, you can protect hello secret at hello user level.</span></span> <span data-ttu-id="e0fc3-187">동일한 사용자 계정에 액세스할 수 hello에서 실행 되는 작업 hello 상승 된 액세스 권한 없이 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-187">Tasks running under hello same user account can access hello secret without elevated access.</span></span>

<span data-ttu-id="e0fc3-188">풀 범위를 갖는 자동 사용자 계정으로 toorun 작업 인터페이스 MPI (Message Passing) 파일은 사용할 수 있는 또 다른 시나리오를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-188">Another scenario where you may want toorun tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="e0fc3-189">MPI 파일 공유에서 MPI 작업 필요 toowork hello에에서 hello 노드 hello 파일 데이터를 동일한 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-189">An MPI file share is useful when hello nodes in hello MPI task need toowork on hello same file data.</span></span> <span data-ttu-id="e0fc3-190">hello 헤드 노드를 만듭니다 hello 자식 노드가 hello에서 실행 하는 경우 액세스할 수 있는 파일 공유 같은 자동 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-190">hello head node creates a file share that hello child nodes can access if they are running under hello same auto-user account.</span></span> 

<span data-ttu-id="e0fc3-191">다음 코드 조각 hello 일괄 처리.NET의 작업에 대 한 hello 자동-사용자의 범위 toopool 범위를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-191">hello following code snippet sets hello auto-user's scope toopool scope for a task in Batch .NET.</span></span> <span data-ttu-id="e0fc3-192">hello 상승 수준을 생략 하면 hello 작업 hello 표준 풀 전체의 자동 사용자 계정으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-192">hello elevation level is omitted, so hello task runs under hello standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="e0fc3-193">명명된 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="e0fc3-193">Named user accounts</span></span>

<span data-ttu-id="e0fc3-194">풀을 만들 때 명명된 사용자 계정을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="e0fc3-195">명명된 사용자 계정에는 사용자가 제공하는 이름 및 암호가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="e0fc3-196">명명 된 사용자 계정에 대 한 hello 상승 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-196">You can specify hello elevation level for a named user account.</span></span> <span data-ttu-id="e0fc3-197">Linux 노드의 경우 SSH 개인 키를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="e0fc3-198">명명 된 사용자 계정이 hello 풀의 모든 노드에서 있고은 사용할 수 있는 tooall 작업이 실행 되 고 해당 노드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-198">A named user account exists on all nodes in hello pool and is available tooall tasks running on those nodes.</span></span> <span data-ttu-id="e0fc3-199">풀에 대해 원하는 수의 명명된 사용자를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="e0fc3-200">작업 또는 작업 컬렉션에 추가 하면 해당 hello 작업 hello 라는 hello 풀에 정의 된 사용자 계정 중 하나에서 실행을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-200">When you add a task or task collection, you can specify that hello task runs under one of hello named user accounts defined on hello pool.</span></span>

<span data-ttu-id="e0fc3-201">명명 된 사용자 계정 유용 toorun 하려는 경우 작업의 모든 작업에서 동일한 사용자 계정 hello 하지만 hello에서 다른 작업에서 실행 되는 작업에서 격리 하 고 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-201">A named user account is useful when you want toorun all tasks in a job under hello same user account, but isolate them from tasks running in other jobs at hello same time.</span></span> <span data-ttu-id="e0fc3-202">예를 들어 각 작업에 대해 명명된 사용자를 만들고 해당 명명된 사용자 계정에서 각 작업의 태스크를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="e0fc3-203">그런 후 각 작업은 자체 태스크와 암호를 공유할 수 있지만 다른 작업에서 실행되는 태스크와는 암호를 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="e0fc3-204">명명 된 사용자 계정 toorun 파일 공유와 같은 외부 리소스에 사용 권한을 설정 하는 작업을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-204">You can also use a named user account toorun a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="e0fc3-205">명명 된 사용자 계정을 사용 하 여 hello 사용자 id를 제어 하 고 해당 사용자 id tooset 권한을 צ ְ ײ 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-205">With a named user account, you control hello user identity and can use that user identity tooset permissions.</span></span>  

<span data-ttu-id="e0fc3-206">명명된 사용자 계정은 Linux 노드 간에 암호 없는 SSH를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="e0fc3-207">Toorun 다중 인스턴스 작업을 필요로 하는 Linux 노드에 있는 명명 된 사용자 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-207">You can use a named user account with Linux nodes that need toorun multi-instance tasks.</span></span> <span data-ttu-id="e0fc3-208">Hello 풀의 각 노드에 hello 전체 풀에 정의 된 사용자 계정으로 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-208">Each node in hello pool can run tasks under a user account defined on hello whole pool.</span></span> <span data-ttu-id="e0fc3-209">다중 인스턴스 작업에 대 한 자세한 내용은 참조 [다중을 사용 하 여\-인스턴스 toorun MPI 응용 프로그램 작업](batch-mpi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-209">For more information about multi-instance tasks, see [Use multi\-instance tasks toorun MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="e0fc3-210">명명된 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e0fc3-210">Create named user accounts</span></span>

<span data-ttu-id="e0fc3-211">toocreate 일괄 처리에서 사용자 계정을 명명 된 사용자 계정 toohello 풀의 컬렉션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-211">toocreate named user accounts in Batch, add a collection of user accounts toohello pool.</span></span> <span data-ttu-id="e0fc3-212">hello 다음 코드 조각 표시 toocreate.NET, Java, 및 Python에서 사용자 계정 이름을 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-212">hello following code snippets show how toocreate named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="e0fc3-213">다음 코드 조각 표시 방법을 코드 toocreate 관리자와 비관리자 계정 풀에 이라는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-213">These code snippets show how toocreate both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="e0fc3-214">hello 예제 hello 클라우드 서비스 구성을 사용 하 여 풀 만들지만 hello 가상 컴퓨터 구성을 사용 하 여 Windows 또는 Linux 풀을 만들 때 동일한 접근 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-214">hello examples create pools using hello cloud service configuration, but you use hello same approach when creating a Windows or Linux pool using hello virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="e0fc3-215">Batch .NET 예제(Windows)</span><span class="sxs-lookup"><span data-stu-id="e0fc3-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="e0fc3-216">Batch .NET 예제(Linux)</span><span class="sxs-lookup"><span data-stu-id="e0fc3-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="e0fc3-217">Batch Java 예제</span><span class="sxs-lookup"><span data-stu-id="e0fc3-217">Batch Java example</span></span>

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a><span data-ttu-id="e0fc3-218">Batch Python 예제</span><span class="sxs-lookup"><span data-stu-id="e0fc3-218">Batch Python example</span></span>

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="e0fc3-219">관리자 액세스 권한을 갖는 명명된 사용자 계정에서 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="e0fc3-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="e0fc3-220">상승 된 권한으로 집합 hello 작업의 작업 toorun **UserIdentity** 속성 tooa 사용자 계정을 사용 하 여 만든 명명 된 해당 **ElevationLevel** 속성이 너무 설정`Admin`합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-220">toorun a task as an elevated user, set hello task's **UserIdentity** property tooa named user account that was created with its **ElevationLevel** property set too`Admin`.</span></span>

<span data-ttu-id="e0fc3-221">이 코드 조각은 hello 작업 명명 된 사용자 계정으로 실행할지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-221">This code snippet specifies that hello task should run under a named user account.</span></span> <span data-ttu-id="e0fc3-222">Hello 풀을 만들 때이 명명 된 사용자 계정 풀 hello에 정의 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-222">This named user account was defined on hello pool when hello pool was created.</span></span> <span data-ttu-id="e0fc3-223">이 경우 사용자 계정 이라는 hello은 관리자 권한으로 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-223">In this case, hello named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a><span data-ttu-id="e0fc3-224">코드 toohello 최신 일괄 처리 클라이언트 라이브러리를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-224">Update your code toohello latest Batch client library</span></span>

<span data-ttu-id="e0fc3-225">2017-01-01.4.0 hello 교체는 주요 변경 사항이 도입 hello 일괄 처리 서비스 버전 **runElevated** hello로 이전 버전에서 사용할 수 있는 속성 **userIdentity** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-225">hello Batch service version 2017-01-01.4.0 introduces a breaking change, replacing hello **runElevated** property available in earlier versions with hello **userIdentity** property.</span></span> <span data-ttu-id="e0fc3-226">다음 표에서 hello 매핑을 해당 하는 간단한 צ ְ ײ tooupdate hello client 라이브러리의 이전 버전에서 코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-226">hello following tables provide a simple mapping that you can use tooupdate your code from earlier versions of hello client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="e0fc3-227">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="e0fc3-227">Batch .NET</span></span>

| <span data-ttu-id="e0fc3-228">코드에서 사용되는 원본...</span><span class="sxs-lookup"><span data-stu-id="e0fc3-228">If your code uses...</span></span>                  | <span data-ttu-id="e0fc3-229">업데이트 대상...</span><span class="sxs-lookup"><span data-stu-id="e0fc3-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="e0fc3-230">`CloudTask.RunElevated`가 지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="e0fc3-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="e0fc3-231">업데이트 필요 없음</span><span class="sxs-lookup"><span data-stu-id="e0fc3-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="e0fc3-232">Batch Java</span><span class="sxs-lookup"><span data-stu-id="e0fc3-232">Batch Java</span></span>

| <span data-ttu-id="e0fc3-233">코드에서 사용되는 원본...</span><span class="sxs-lookup"><span data-stu-id="e0fc3-233">If your code uses...</span></span>                      | <span data-ttu-id="e0fc3-234">업데이트 대상...</span><span class="sxs-lookup"><span data-stu-id="e0fc3-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="e0fc3-235">`CloudTask.withRunElevated`가 지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="e0fc3-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="e0fc3-236">업데이트 필요 없음</span><span class="sxs-lookup"><span data-stu-id="e0fc3-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="e0fc3-237">Batch Python</span><span class="sxs-lookup"><span data-stu-id="e0fc3-237">Batch Python</span></span>

| <span data-ttu-id="e0fc3-238">코드에서 사용되는 원본...</span><span class="sxs-lookup"><span data-stu-id="e0fc3-238">If your code uses...</span></span>                      | <span data-ttu-id="e0fc3-239">업데이트 대상...</span><span class="sxs-lookup"><span data-stu-id="e0fc3-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="e0fc3-240">`user_identity=user`</span><span class="sxs-lookup"><span data-stu-id="e0fc3-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="e0fc3-241">`user_identity=user`</span><span class="sxs-lookup"><span data-stu-id="e0fc3-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="e0fc3-242">`run_elevated`가 지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="e0fc3-242">`run_elevated` not specified</span></span> | <span data-ttu-id="e0fc3-243">업데이트 필요 없음</span><span class="sxs-lookup"><span data-stu-id="e0fc3-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="e0fc3-244">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0fc3-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="e0fc3-245">배치 포럼</span><span class="sxs-lookup"><span data-stu-id="e0fc3-245">Batch Forum</span></span>

<span data-ttu-id="e0fc3-246">hello [Azure 배치 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) 는 좋은 toodiscuss 일괄 처리를 놓고 hello 서비스에 대 한 질문은 msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-246">hello [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="e0fc3-247">유용한 고정 게시물을 참조하고 배치 솔루션을 빌드하는 동안 질문이 생기면 즉시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e0fc3-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>
