---
title: "Azure 배치에서 사용자 계정으로 태스크 실행 | Microsoft Docs"
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
ms.openlocfilehash: d408c0565c0ed81fc97cc2b3976a4fc233e31302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="83de9-103">배치에서 사용자 계정으로 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="83de9-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="83de9-104">Azure 배치의 태스크는 항상 사용자 계정으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="83de9-105">기본적으로 태스크는 관리자 권한 없이 표준 사용자 계정으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="83de9-106">일반적으로는 이러한 기본 사용자 계정 설정만으로 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="83de9-107">그러나 특정 시나리오에서는 태스크를 실행하려는 사용자 계정을 구성하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-107">For certain scenarios, however, it's useful to be able to configure the user account under which you want a task to run.</span></span> <span data-ttu-id="83de9-108">이 문서에서는 사용자 계정의 유형 및 시나리오에 맞게 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-108">This article discusses the types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="83de9-109">사용자 계정의 유형</span><span class="sxs-lookup"><span data-stu-id="83de9-109">Types of user accounts</span></span>

<span data-ttu-id="83de9-110">Azure 배치에서는 태스크 실행을 위해 다음과 같은 두 가지 유형의 사용자 계정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="83de9-111">**자동 사용자 계정.**</span><span class="sxs-lookup"><span data-stu-id="83de9-111">**Auto-user accounts.**</span></span> <span data-ttu-id="83de9-112">자동 사용자 계정은 배치 서비스에 의해 자동으로 생성되는 기본 제공 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-112">Auto-user accounts are built-in user accounts that are created automatically by the Batch service.</span></span> <span data-ttu-id="83de9-113">기본적으로 태스크는 자동 사용자 계정에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="83de9-114">태스크가 실행될 자동 사용자 계정을 나타내도록 태스크에 대한 자동 사용자 지정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-114">You can configure the auto-user specification for a task to indicate under which auto-user account a task should run.</span></span> <span data-ttu-id="83de9-115">자동 사용자 지정을 사용하면 태스크를 실행할 자동 사용자 계정의 권한 상승 수준 및 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-115">The auto-user specification allows you to specify the elevation level and scope of the auto-user account that will run the task.</span></span> 

- <span data-ttu-id="83de9-116">**명명된 사용자 계정.**</span><span class="sxs-lookup"><span data-stu-id="83de9-116">**A named user account.**</span></span> <span data-ttu-id="83de9-117">풀을 만들 때 풀에 대해 하나 이상의 명명된 사용자 계정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-117">You can specify one or more named user accounts for a pool when you create the pool.</span></span> <span data-ttu-id="83de9-118">각 사용자 계정은 풀의 각 노드에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-118">Each user account is created on each node of the pool.</span></span> <span data-ttu-id="83de9-119">계정 이름 외에도 계정 암호, 권한 상승 수준을 지정할 수 있으며, Linux 풀의 경우에는 SSH 개인 키도 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-119">In addition to the account name, you specify the user account password, elevation level, and, for Linux pools, the SSH private key.</span></span> <span data-ttu-id="83de9-120">태스크를 추가할 때 해당 태스크를 실행할 명명된 사용자 계정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-120">When you add a task, you can specify the named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="83de9-121">배치 서비스 버전 2017-01-01.4.0에서는 해당 버전을 호출하기 위해 코드를 업데이트해야 하는 주요 변경 내용이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-121">The Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code to call that version.</span></span> <span data-ttu-id="83de9-122">이전 버전의 배치에서 코드를 마이그레이션하는 경우 REST API 또는 배치 클라이언트 라이브러리에서 **runElevated** 속성이 더 이상 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-122">If you are migrating code from an older version of Batch, note that the **runElevated** property is no longer supported in the REST API or Batch client libraries.</span></span> <span data-ttu-id="83de9-123">태스크의 새로운 **userIdentity** 속성을 사용하여 권한 상승 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-123">Use the new **userIdentity** property of a task to specify elevation level.</span></span> <span data-ttu-id="83de9-124">클라이언트 라이브러리 중 하나를 사용하는 경우 배치 코드를 업데이트하기 위한 빠른 지침을 보려면 [최신 배치 클라이언트 라이브러리로 코드 업데이트](#update-your-code-to-the-latest-batch-client-library) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83de9-124">See the section titled [Update your code to the latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of the client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="83de9-125">이 문서에서 설명하는 사용자 계정은 보안상의 이유로 RDP(원격 데스크톱 프로토콜) 또는 SSH(보안 셸)을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-125">The user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="83de9-126">SSH를 통해 Linux 가상 컴퓨터 구성을 실행하는 노드에 연결하려면 [Azure에서 Linux VM에 대해 원격 데스크톱 사용](../virtual-machines/virtual-machines-linux-use-remote-desktop.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83de9-126">To connect to a node running the Linux virtual machine configuration via SSH, see [Use Remote Desktop to a Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="83de9-127">RDP를 통해 Windows를 실행하는 노드에 연결하려면 [Windows Server VM에 연결](../virtual-machines/windows/connect-logon.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83de9-127">To connect to nodes running Windows via RDP, see [Connect to a Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="83de9-128">RDP를 통해 클라우드 서비스 구성을 실행하는 노드에 연결하려면 [Azure Cloud Services의 역할에 대해 원격 데스크톱 연결 사용](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83de9-128">To connect to a node running the cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-to-files-and-directories"></a><span data-ttu-id="83de9-129">파일 및 디렉터리에 대한 사용자 계정 액세스</span><span class="sxs-lookup"><span data-stu-id="83de9-129">User account access to files and directories</span></span>

<span data-ttu-id="83de9-130">자동 사용자 계정 및 명명된 사용자 계정 둘 다 태스크의 작업 디렉터리, 공유 디렉터리 및 다중 인스턴스 태스크 디렉터리에 대해 읽기/쓰기 액세스 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-130">Both an auto-user account and a named user account have read/write access to the task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="83de9-131">두 가지 유형의 계정 모두 시작 및 작업 준비 디렉터리에 대해 읽기 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-131">Both types of accounts have read access to the startup and job preparation directories.</span></span>

<span data-ttu-id="83de9-132">태스크가 시작 태스크를 실행하는 데 사용된 것과 동일한 계정에서 실행되는 경우 태스크에는 시작 태스크 디렉터리에 대한 읽기/쓰기 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-132">If a task runs under the same account that was used for running a start task, the task has read-write access to the start task directory.</span></span> <span data-ttu-id="83de9-133">마찬가지로 태스크가 작업 준비 태스크를 실행하는 데 사용된 것과 동일한 계정에서 실행되는 경우 태스크에는 작업 준비 태스크 디렉터리에 대한 읽기/쓰기 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-133">Similarly, if a task runs under the same account that was used for running a job preparation task, the task has read-write access to the job preparation task directory.</span></span> <span data-ttu-id="83de9-134">태스크가 시작 태스크 또는 작업 준비 태스크와는 다른 계정에서 실행될 경우 태스크는 해당 디렉터리에 대해 읽기 액세스 권한만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-134">If a task runs under a different account than the start task or job preparation task, then the task has only read access to the respective directory.</span></span>

<span data-ttu-id="83de9-135">태스크에서 파일 및 디렉터리 액세스에 대한 자세한 내용은 [배치를 사용하여 대규모 병렬 계산 솔루션 개발](batch-api-basics.md#files-and-directories)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83de9-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="83de9-136">태스크에 대한 관리자 권한 액세스</span><span class="sxs-lookup"><span data-stu-id="83de9-136">Elevated access for tasks</span></span> 

<span data-ttu-id="83de9-137">사용자 계정의 권한 상승 수준은 태스크가 관리자 액세스 권한으로 실행되는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-137">The user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="83de9-138">자동 사용자 계정 및 명명된 사용자 계정 모두 관리자 권한 액세스로 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="83de9-139">권한 상승 수준의 두 가지 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-139">The two options for elevation level are:</span></span>

- <span data-ttu-id="83de9-140">**NonAdmin:** 태스크가 관리자 액세스 권한이 없는 표준 사용자로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-140">**NonAdmin:** The task runs as a standard user without elevated access.</span></span> <span data-ttu-id="83de9-141">배치 사용자 계정에 대한 기본 권한 상승 수준은 항상 **NonAdmin**입니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-141">The default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="83de9-142">**Admin:** 태스크가 관리자 액세스 권한이 있는 사용자로 실행되고 모든 관리자 권한으로 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-142">**Admin:** The task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="83de9-143">자동 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="83de9-143">Auto-user accounts</span></span>

<span data-ttu-id="83de9-144">기본적으로 태스크는 자동 사용자 계정에서 배치로, 관리자 액세스 권한이 없는 표준 사용자로, 태스크 범위를 사용해서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="83de9-145">태스크 범위에 대해 자동 사용자 지정이 구성되면 배치 서비스는 해당 태스크에 대해서만 자동 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-145">When the auto-user specification is configured for task scope, the Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="83de9-146">태스크 범위 대신 풀 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-146">The alternative to task scope is pool scope.</span></span> <span data-ttu-id="83de9-147">태스크에 대한 자동 사용자 지정이 풀 범위에 대해 구성되면 태스크는 풀의 모든 태스크에서 사용할 수 있는 자동 사용자 계정으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-147">When the auto-user specification for a task is configured for pool scope, the task runs under an auto-user account that is available to any task in the pool.</span></span> <span data-ttu-id="83de9-148">풀 범위에 대한 자세한 내용은 [풀 범위를 갖는 자동 사용자로 태스크 실행](#run-a-task-as-the-autouser-with-pool-scope) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83de9-148">For more information about pool scope, see the section titled [Run a task as the auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="83de9-149">기본 범위는 Windows 및 Linux 노드에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-149">The default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="83de9-150">Windows 노드에서 태스크는 기본적으로 태스크 범위 내에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="83de9-151">Linux 노드는 항상 풀 범위에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="83de9-152">자동 사용자 지정에는 각각 고유한 자동 사용자 계정에 해당하는 4개의 구성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-152">There are four possible configurations for the auto-user specification, each of which corresponds to a unique auto-user account:</span></span>

- <span data-ttu-id="83de9-153">태스크 범위를 사용하는 비관리자 액세스(기본 자동 사용자 지정)</span><span class="sxs-lookup"><span data-stu-id="83de9-153">Non-admin access with task scope (the default auto-user specification)</span></span>
- <span data-ttu-id="83de9-154">태스크 범위를 사용하는 관리자(상승된 권한) 액세스</span><span class="sxs-lookup"><span data-stu-id="83de9-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="83de9-155">풀 범위를 사용하는 비관리자 액세스</span><span class="sxs-lookup"><span data-stu-id="83de9-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="83de9-156">풀 범위를 사용하는 관리자 액세스</span><span class="sxs-lookup"><span data-stu-id="83de9-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="83de9-157">태스크 범위 내에서 실행되는 태스크는 실제로 노드의 다른 태스트에 대해 액세스 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-157">Tasks running under task scope do not have de facto access to other tasks on a node.</span></span> <span data-ttu-id="83de9-158">그러나 계정에 액세스할 수 있는 악의적인 사용자는 관리자 권한으로 실행되고 다른 태스크 디렉터리에 액세스하는 태스크를 제출하여 이러한 제한을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-158">However, a malicious user with access to the account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="83de9-159">또한 악의적인 사용자는 RDP 또는 SSH를 사용하여 노드에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-159">A malicious user could also use RDP or SSH to connect to a node.</span></span> <span data-ttu-id="83de9-160">이러한 시나리오를 방지하기 위해서는 배치 계정 키에 대한 액세스를 보호하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-160">It's important to protect access to your Batch account keys to prevent such a scenario.</span></span> <span data-ttu-id="83de9-161">계정이 노출이 의심되는 경우에 키를 다시 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-161">If you suspect your account may have been compromised, be sure to regenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="83de9-162">관리자 액세스 권한이 있는 자동 사용자로 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="83de9-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="83de9-163">관리자 액세스 권한으로 태스크를 실행해야 하는 경우 관리자 권한에 대한 자동 사용자 지정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-163">You can configure the auto-user specification for administrator privileges when you need to run a task with elevated access.</span></span> <span data-ttu-id="83de9-164">예를 들어 시작 태스크는 노드에 소프트웨어를 설치하기 위해 관리자 액세스 권한이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-164">For example, a start task may need elevated access to install software on the node.</span></span>

> [!NOTE] 
> <span data-ttu-id="83de9-165">일반적으로 관리자 액세스 권한은 필요한 경우에만 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-165">In general, it's best to use elevated access only when necessary.</span></span> <span data-ttu-id="83de9-166">모범 사례는 원하는 결과를 달성하는 데 필요한 최소 권한을 부여하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-166">Best practices recommend granting the minimum privilege necessary to achieve the desired outcome.</span></span> <span data-ttu-id="83de9-167">예를 들어 시작 태스크가 모든 사용자가 아닌 현재 사용자에 대해 소프트웨어를 설치하는 경우 태스크에 관리자 권한 액세스를 부여하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-167">For example, if a start task installs software for the current user, instead of for all users, you may be able to avoid granting elevated access to tasks.</span></span> <span data-ttu-id="83de9-168">시작 태스크를 포함하여 동일한 계정으로 실행해야 하는 모든 태스트에 대해 풀 범위 및 비관리자 액세스 권한에 대한 자동 사용자 지정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-168">You can configure the auto-user specification for pool scope and non-admin access for all tasks that need to run under the same account, including the start task.</span></span> 
>
>

<span data-ttu-id="83de9-169">다음 코드 조각은 자동 사용자 지정을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-169">The following code snippets show how to configure the auto-user specification.</span></span> <span data-ttu-id="83de9-170">예제에서는 권한 상승 수준을 `Admin`으로 설정하고 범위를 `Task`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-170">The examples set the elevation level to `Admin` and the scope to `Task`.</span></span> <span data-ttu-id="83de9-171">태스크 범위가 기본 설정이지만 여기에는 예제를 위해 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-171">Task scope is the default setting, but is included here for the sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="83de9-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="83de9-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="83de9-173">Batch Java</span><span class="sxs-lookup"><span data-stu-id="83de9-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="83de9-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="83de9-174">Batch Python</span></span>

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="83de9-175">풀 범위가 지정된 자동 사용자로 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="83de9-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="83de9-176">노드가 프로비전될 때 풀의 각 노드에서 관리자 액세스 권한을 갖는 풀 전체 자동 사용자 계정과 이러한 권한을 갖지 않는 계정이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in the pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="83de9-177">자동 사용자의 범위를 지정된 태스크에 대한 풀 범위로 설정하면 태스크는 이러한 2개의 풀 전체 자동 사용자 계정 중 하나에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-177">Setting the auto-user's scope to pool scope for a given task runs the task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="83de9-178">자동 사용자에 대해 풀 범위를 지정하면 관리자 액세스 권한으로 실행되는 모든 태스크가 동일한 풀 전체 자동 사용자 계정에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-178">When you specify pool scope for the auto-user, all tasks that run with administrator access run under the same pool-wide auto-user account.</span></span> <span data-ttu-id="83de9-179">마찬가지로 관리자 권한 없이 실행되는 태스크도 단일 풀 전체 자동 사용자 계정에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="83de9-180">2개의 풀 전체 자동 사용자 계정은 별도 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-180">The two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="83de9-181">풀 전체 관리 계정에서 실행되는 태스크는 표준 계정으로 실행되는 태스크와 데이터를 공유할 수 없으며 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-181">Tasks running under the pool-wide administrative account cannot share data with tasks running under the standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="83de9-182">동일한 자동 사용자 계정에서 실행될 때의 장점은 태스크가 동일한 노드에서 실행 중인 다른 태스크와 데이터를 공유할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-182">The advantage to running under the same auto-user account is that tasks are able to share data with other tasks running on the same node.</span></span>

<span data-ttu-id="83de9-183">태스크 간에 암호를 공유하는 것은 두 풀 전체 자동 사용자 계정 중 하나에서 태스크를 실행하는 것이 유용한 하나의 시나리오에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-183">Sharing secrets between tasks is one scenario where running tasks under one of the two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="83de9-184">예를 들어 시작 태스크가 해당 태스크에서 사용할 수 있는 노드에 암호를 프로비전해야 한다고 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-184">For example, suppose a start task needs to provision a secret onto the node that other tasks can use.</span></span> <span data-ttu-id="83de9-185">Windows DPAPI(데이터 보호 API)를 사용할 수 있지만 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-185">You could use the Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="83de9-186">대신 사용자 수준에서 암호를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-186">Instead, you can protect the secret at the user level.</span></span> <span data-ttu-id="83de9-187">동일한 사용자 계정에서 실행되는 태스크는 관리자 액세스 권한 없이도 암호에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-187">Tasks running under the same user account can access the secret without elevated access.</span></span>

<span data-ttu-id="83de9-188">풀 범위를 갖는 자동 사용자 계정에서 태스크를 실행하려는 또 다른 시나리오는 MPI(Message Passing Interface) 파일 공유입니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-188">Another scenario where you may want to run tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="83de9-189">MPI 파일 공유는 MPI 태스크의 노드가 동일한 파일 데이터에 작동해야 하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-189">An MPI file share is useful when the nodes in the MPI task need to work on the same file data.</span></span> <span data-ttu-id="83de9-190">헤드 노드는 자식 노드가 동일한 자동 사용자 계정에서 실행되는 경우 자식 노드가 액세스할 수 있는 파일 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-190">The head node creates a file share that the child nodes can access if they are running under the same auto-user account.</span></span> 

<span data-ttu-id="83de9-191">다음 코드 조각은 Batch .NET에서 태스크에 대해 자동 사용자 범위를 풀 범위로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-191">The following code snippet sets the auto-user's scope to pool scope for a task in Batch .NET.</span></span> <span data-ttu-id="83de9-192">권한 상승 수준이 생략되므로 태스크는 표준 풀 전체 자동 사용자 계정에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-192">The elevation level is omitted, so the task runs under the standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="83de9-193">명명된 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="83de9-193">Named user accounts</span></span>

<span data-ttu-id="83de9-194">풀을 만들 때 명명된 사용자 계정을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="83de9-195">명명된 사용자 계정에는 사용자가 제공하는 이름 및 암호가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="83de9-196">명명된 사용자 계정에 대해 권한 상승 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-196">You can specify the elevation level for a named user account.</span></span> <span data-ttu-id="83de9-197">Linux 노드의 경우 SSH 개인 키를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="83de9-198">명명된 사용자 계정은 풀의 모든 노드에 존재하며 해당 노드에서 실행되는 모든 태스크에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-198">A named user account exists on all nodes in the pool and is available to all tasks running on those nodes.</span></span> <span data-ttu-id="83de9-199">풀에 대해 원하는 수의 명명된 사용자를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="83de9-200">태스크 또는 태스크 컬렉션을 추가할 때 태스크가 풀에 대해 정의된 명명된 사용자 계정 중 하나에서 실행되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-200">When you add a task or task collection, you can specify that the task runs under one of the named user accounts defined on the pool.</span></span>

<span data-ttu-id="83de9-201">명명된 사용자 계정은 동일한 사용자 계정에서 작업의 모든 태스크를 실행하려고 하지만 동시에 다른 작업에서 실행되는 태스크와 격리하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-201">A named user account is useful when you want to run all tasks in a job under the same user account, but isolate them from tasks running in other jobs at the same time.</span></span> <span data-ttu-id="83de9-202">예를 들어 각 작업에 대해 명명된 사용자를 만들고 해당 명명된 사용자 계정에서 각 작업의 태스크를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="83de9-203">그런 후 각 작업은 자체 태스크와 암호를 공유할 수 있지만 다른 작업에서 실행되는 태스크와는 암호를 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="83de9-204">또한 명명된 사용자 계정을 사용하여 파일 공유와 같은 외부 리소스에 대해 권한을 설정하는 태스크도 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-204">You can also use a named user account to run a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="83de9-205">명명된 사용자 계정을 사용하여 사용자 ID를 제어하고 해당 사용자 ID를 사용하여 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-205">With a named user account, you control the user identity and can use that user identity to set permissions.</span></span>  

<span data-ttu-id="83de9-206">명명된 사용자 계정은 Linux 노드 간에 암호 없는 SSH를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="83de9-207">다중 인스턴스 태스크를 실행해야 하는 Linux 노드에 명명된 사용자 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-207">You can use a named user account with Linux nodes that need to run multi-instance tasks.</span></span> <span data-ttu-id="83de9-208">풀의 각 노드는 전체 풀에 정의된 사용자 계정에서 태스크를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-208">Each node in the pool can run tasks under a user account defined on the whole pool.</span></span> <span data-ttu-id="83de9-209">다중 인스턴스 태스크에 대한 자세한 내용은 [다중\- 인스턴스 태스크를 사용하여 MPI 응용 프로그램 실행](batch-mpi.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83de9-209">For more information about multi-instance tasks, see [Use multi\-instance tasks to run MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="83de9-210">명명된 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="83de9-210">Create named user accounts</span></span>

<span data-ttu-id="83de9-211">배치에서 명명된 사용자 계정을 만들려면 풀에 사용자 계정의 컬렉션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-211">To create named user accounts in Batch, add a collection of user accounts to the pool.</span></span> <span data-ttu-id="83de9-212">다음 코드 조각에서는 .NET, Java 및 Python에서 명명된 사용자 계정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-212">The following code snippets show how to create named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="83de9-213">이러한 코드 조각에서는 풀에 관리자 및 비관리자 명명된 계정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-213">These code snippets show how to create both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="83de9-214">예제에서는 클라우드 서비스 구성을 사용하여 풀을 만들지만 가상 컴퓨터 구성을 사용하여 Windows 또는 Linux 풀을 만들 때도 같은 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-214">The examples create pools using the cloud service configuration, but you use the same approach when creating a Windows or Linux pool using the virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="83de9-215">Batch .NET 예제(Windows)</span><span class="sxs-lookup"><span data-stu-id="83de9-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using the cloud service configuration.
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

// Commit the pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="83de9-216">Batch .NET 예제(Linux)</span><span class="sxs-lookup"><span data-stu-id="83de9-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the virtual machine configuration to use to create the pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create the unbound pool.
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

// Commit the pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="83de9-217">Batch Java 예제</span><span class="sxs-lookup"><span data-stu-id="83de9-217">Batch Java example</span></span>

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

#### <a name="batch-python-example"></a><span data-ttu-id="83de9-218">Batch Python 예제</span><span class="sxs-lookup"><span data-stu-id="83de9-218">Batch Python example</span></span>

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="83de9-219">관리자 액세스 권한을 갖는 명명된 사용자 계정에서 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="83de9-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="83de9-220">관리자 권한 사용자로 태스크를 실행하려면 태스크의 **UserIdentity** 속성을 해당 **ElevationLevel** 속성을 `Admin`으로 설정한 상태로 만든 명명된 사용자 계정으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-220">To run a task as an elevated user, set the task's **UserIdentity** property to a named user account that was created with its **ElevationLevel** property set to `Admin`.</span></span>

<span data-ttu-id="83de9-221">이 코드 조각은 태스크가 명명된 사용자 계정으로 실행되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-221">This code snippet specifies that the task should run under a named user account.</span></span> <span data-ttu-id="83de9-222">이 명명된 사용자 계정은 풀이 만들어질 때 풀에 정의된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-222">This named user account was defined on the pool when the pool was created.</span></span> <span data-ttu-id="83de9-223">이 경우 명명된 사용자 계정은 다음 관리자 권한으로 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-223">In this case, the named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-to-the-latest-batch-client-library"></a><span data-ttu-id="83de9-224">최신 배치 클라이언트 라이브러리로 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="83de9-224">Update your code to the latest Batch client library</span></span>

<span data-ttu-id="83de9-225">2017-01-01.4.0의 배치 서비스 버전에는 중요한 변경 내용이 추가되었으며 이전 버전에서 사용할 수 있던 **runElevated** 속성이 **userIdentity** 속성으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-225">The Batch service version 2017-01-01.4.0 introduces a breaking change, replacing the **runElevated** property available in earlier versions with the **userIdentity** property.</span></span> <span data-ttu-id="83de9-226">다음 표에서는 이전 버전의 클라이언트 라이브러리에서 코드를 업데이트하는 데 사용할 수 있는 간단한 매핑을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-226">The following tables provide a simple mapping that you can use to update your code from earlier versions of the client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="83de9-227">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="83de9-227">Batch .NET</span></span>

| <span data-ttu-id="83de9-228">코드에서 사용되는 원본...</span><span class="sxs-lookup"><span data-stu-id="83de9-228">If your code uses...</span></span>                  | <span data-ttu-id="83de9-229">업데이트 대상...</span><span class="sxs-lookup"><span data-stu-id="83de9-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="83de9-230">`CloudTask.RunElevated`가 지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="83de9-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="83de9-231">업데이트 필요 없음</span><span class="sxs-lookup"><span data-stu-id="83de9-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="83de9-232">Batch Java</span><span class="sxs-lookup"><span data-stu-id="83de9-232">Batch Java</span></span>

| <span data-ttu-id="83de9-233">코드에서 사용되는 원본...</span><span class="sxs-lookup"><span data-stu-id="83de9-233">If your code uses...</span></span>                      | <span data-ttu-id="83de9-234">업데이트 대상...</span><span class="sxs-lookup"><span data-stu-id="83de9-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="83de9-235">`CloudTask.withRunElevated`가 지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="83de9-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="83de9-236">업데이트 필요 없음</span><span class="sxs-lookup"><span data-stu-id="83de9-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="83de9-237">Batch Python</span><span class="sxs-lookup"><span data-stu-id="83de9-237">Batch Python</span></span>

| <span data-ttu-id="83de9-238">코드에서 사용되는 원본...</span><span class="sxs-lookup"><span data-stu-id="83de9-238">If your code uses...</span></span>                      | <span data-ttu-id="83de9-239">업데이트 대상...</span><span class="sxs-lookup"><span data-stu-id="83de9-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="83de9-240">`user_identity=user`</span><span class="sxs-lookup"><span data-stu-id="83de9-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="83de9-241">`user_identity=user`</span><span class="sxs-lookup"><span data-stu-id="83de9-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="83de9-242">`run_elevated`가 지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="83de9-242">`run_elevated` not specified</span></span> | <span data-ttu-id="83de9-243">업데이트 필요 없음</span><span class="sxs-lookup"><span data-stu-id="83de9-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="83de9-244">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83de9-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="83de9-245">배치 포럼</span><span class="sxs-lookup"><span data-stu-id="83de9-245">Batch Forum</span></span>

<span data-ttu-id="83de9-246">MSDN의 [Azure 배치 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch)은 배치를 설명하고 서비스에 대한 질문을 하는 데 많은 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-246">The [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="83de9-247">유용한 고정 게시물을 참조하고 배치 솔루션을 빌드하는 동안 질문이 생기면 즉시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="83de9-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>