---
title: "역할 기반 액세스 제어를 사용하여 백업 관리 | Microsoft Docs"
description: "복구 서비스 자격 증명 모음에 역할 기반 액세스 제어 toomanage 액세스 toobackup 관리 작업을 사용 합니다."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 3bd46b97-4b29-47a5-b5ac-ac174dd36760
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: trinadhk;markgal
ms.openlocfilehash: 26d034d152f9b77fc6d5b2ffd5ef2648b1797f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-backup-recovery-points"></a><span data-ttu-id="39113-103">역할 기반 액세스 제어 toomanage Azure 백업 복구 지점을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="39113-103">Use Role-Based Access Control toomanage Azure Backup recovery points</span></span>
<span data-ttu-id="39113-104">Azure RBAC(역할 기반 액세스 제어)를 통해 Azure에 대한 세밀한 액세스 관리가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="39113-104">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="39113-105">RBAC를 사용 하 여 팀 내에서 업무를 구분할 수 있으며 필요 하다는 tooperform 업무 hello 양의 데이터만 toousers 액세스 권한을 부여 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39113-105">Using RBAC, you can segregate duties within your team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39113-106">Azure 백업에서 제공 하는 역할은 Azure 포털에서 수행할 수 있는 제한 tooactions 또는 복구 서비스 자격 증명 모음에 PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="39113-106">Roles provided by Azure Backup are limited tooactions that can be performed in Azure portal or Recovery Services vault PowerShell cmdlets.</span></span> <span data-ttu-id="39113-107">Azure 백업 에이전트 클라이언트 UI, System Center Data Protection Manager UI 또는 Azure Backup Server UI에서 실행되는 작업은 이러한 역할의 제어를 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39113-107">Actions performed in Azure backup Agent Client UI or System center Data Protection Manager UI or Azure Backup Server UI are out of control of these roles.</span></span>

<span data-ttu-id="39113-108">Azure 백업 3 기본 제공 역할 toocontrol 백업 관리 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39113-108">Azure Backup provides 3 built-in roles toocontrol backup management operations.</span></span> <span data-ttu-id="39113-109">[Azure RBAC 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="39113-109">Learn more on [Azure RBAC built-in roles](../active-directory/role-based-access-built-in-roles.md)</span></span>

* <span data-ttu-id="39113-110">[참가자 백업](../active-directory/role-based-access-built-in-roles.md#backup-contributor) -이 역할에 모든 권한을 toocreate 및 백업 복구 서비스 자격 증명 모음 만들기 및 액세스 tooothers 제공 제외 하 고 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="39113-110">[Backup Contributor](../active-directory/role-based-access-built-in-roles.md#backup-contributor) - This role has all permissions toocreate and manage backup except creating Recovery Services vault and giving access tooothers.</span></span> <span data-ttu-id="39113-111">모든 백업 관리 작업을 수행할 수 있는 백업 관리 관리자 역할로 생각하시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39113-111">Imagine this role as admin of backup management who can do every backup management operation.</span></span>
* <span data-ttu-id="39113-112">[연산자 백업](../active-directory/role-based-access-built-in-roles.md#backup-operator) -이 역할에 사용 권한을 tooeverything 백업 하 고 관리할 백업 정책 제거는 참가자는 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="39113-112">[Backup Operator](../active-directory/role-based-access-built-in-roles.md#backup-operator) - This role has permissions tooeverything a contributor does except removing backup and managing backup policies.</span></span> <span data-ttu-id="39113-113">온-프레미스 리소스의 등록을 제거 또는 삭제 데이터와 함께 백업 중지 등의 삭제 작업을 수행할 수 없습니다 것이 역할 해당 toocontributor는 합니다.</span><span class="sxs-lookup"><span data-stu-id="39113-113">This role is equivalent toocontributor except it can't perform destructive operations such as stop backup with delete data or remove registration of on-premises resources.</span></span>
* <span data-ttu-id="39113-114">[판독기 백업](../active-directory/role-based-access-built-in-roles.md#backup-reader) -이 역할에 사용 권한을 tooview 모든 백업 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="39113-114">[Backup Reader](../active-directory/role-based-access-built-in-roles.md#backup-reader) - This role has permissions tooview all backup management operations.</span></span> <span data-ttu-id="39113-115">이 역할 toobe 모니터링 사람을 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="39113-115">Imagine this role toobe a monitoring person.</span></span>

<span data-ttu-id="39113-116">찾고 있는 경우 toodefine 더 많은 컨트롤에 대 한 사용자 역할, 참조 방법을 너무[빌드 사용자 지정 역할](../active-directory/role-based-access-control-custom-roles.md) Azure RBAC에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39113-116">If you're looking toodefine your own roles for even more control, see how too[build Custom roles](../active-directory/role-based-access-control-custom-roles.md) in Azure RBAC.</span></span>



## <a name="mapping-backup-built-in-roles-toobackup-management-actions"></a><span data-ttu-id="39113-117">백업 기본 제공 역할 toobackup 관리 작업 매핑</span><span class="sxs-lookup"><span data-stu-id="39113-117">Mapping Backup built-in roles toobackup management actions</span></span>
<span data-ttu-id="39113-118">다음 표에서 hello hello 백업 관리 작업을 캡처하고 해당 최소 RBAC 역할 필요한 tooperform 해당 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="39113-118">hello following table captures hello Backup management actions and corresponding minimum RBAC role required tooperform that operation.</span></span>

| <span data-ttu-id="39113-119">관리 작업</span><span class="sxs-lookup"><span data-stu-id="39113-119">Management Operation</span></span> | <span data-ttu-id="39113-120">필요한 최소 RBAC 역할</span><span class="sxs-lookup"><span data-stu-id="39113-120">Minimum RBAC role required</span></span> |
| --- | --- |
| <span data-ttu-id="39113-121">Recovery Services 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="39113-121">Create Recovery Services vault</span></span> | <span data-ttu-id="39113-122">자격 증명 모음 리소스 그룹의 참여자</span><span class="sxs-lookup"><span data-stu-id="39113-122">Contributor on Resource group of vault</span></span> |
| <span data-ttu-id="39113-123">Azure VM의 백업 활성화</span><span class="sxs-lookup"><span data-stu-id="39113-123">Enable backup of Azure VMs</span></span> | <span data-ttu-id="39113-124">자격 증명 모음의 Backup 운영자, VM의 가상 컴퓨터 참여자</span><span class="sxs-lookup"><span data-stu-id="39113-124">Backup Operator on vault, Virtual machine contributor on VMs</span></span> |
| <span data-ttu-id="39113-125">VM의 주문형 백업</span><span class="sxs-lookup"><span data-stu-id="39113-125">On-demand backup of VM</span></span> | <span data-ttu-id="39113-126">Backup 운영자</span><span class="sxs-lookup"><span data-stu-id="39113-126">Backup operator</span></span> |
| <span data-ttu-id="39113-127">VM 복원</span><span class="sxs-lookup"><span data-stu-id="39113-127">Restore VM</span></span> | <span data-ttu-id="39113-128">백업 운영자, 리소스 그룹 참가자는 VM 및 Vnet에 배포 하는 진행 중인 tooget 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39113-128">Backup operator, Resource group contributor in which VM and Vnets are going tooget deployed</span></span> |
| <span data-ttu-id="39113-129">디스크, VM 백업의 개별 파일 복원</span><span class="sxs-lookup"><span data-stu-id="39113-129">Restore disks, individual files from VM backup</span></span> | <span data-ttu-id="39113-130">Backup 운영자</span><span class="sxs-lookup"><span data-stu-id="39113-130">Backup operator</span></span> |
| <span data-ttu-id="39113-131">Azure VM 백업에 대한 백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="39113-131">Create backup policy for Azure VM backup</span></span> | <span data-ttu-id="39113-132">Backup 참여자</span><span class="sxs-lookup"><span data-stu-id="39113-132">Backup contributor</span></span> |
| <span data-ttu-id="39113-133">Azure VM 백업의 백업 정책 수정</span><span class="sxs-lookup"><span data-stu-id="39113-133">Modify backup policy of Azure VM backup</span></span> | <span data-ttu-id="39113-134">Backup 참여자</span><span class="sxs-lookup"><span data-stu-id="39113-134">Backup contributor</span></span> |
| <span data-ttu-id="39113-135">Azure VM 백업의 백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="39113-135">Delete backup policy of Azure VM backup</span></span> | <span data-ttu-id="39113-136">Backup 참여자</span><span class="sxs-lookup"><span data-stu-id="39113-136">Backup contributor</span></span> |
| <span data-ttu-id="39113-137">VM 백업에서 백업 중지(데이터 보존 또는 데이터 삭제를 통해)</span><span class="sxs-lookup"><span data-stu-id="39113-137">Stop backup (with retain data or delete data) on VM backup</span></span> | <span data-ttu-id="39113-138">Backup 참여자</span><span class="sxs-lookup"><span data-stu-id="39113-138">Backup contributor</span></span> |
| <span data-ttu-id="39113-139">온-프레미스 Windows 서버/클라이언트/SCDPM 또는 Azure Backup Server 등록</span><span class="sxs-lookup"><span data-stu-id="39113-139">Register on-premises Windows Server/client/SCDPM or Azure Backup Server</span></span> | <span data-ttu-id="39113-140">Backup 운영자</span><span class="sxs-lookup"><span data-stu-id="39113-140">Backup operator</span></span> |
| <span data-ttu-id="39113-141">등록된 온-프레미스 Windows 서버/클라이언트/SCDPM 또는 Azure Backup Server 삭제</span><span class="sxs-lookup"><span data-stu-id="39113-141">Delete registered on-premises Windows Server/client/SCDPM or Azure Backup Server</span></span> | <span data-ttu-id="39113-142">Backup 참여자</span><span class="sxs-lookup"><span data-stu-id="39113-142">Backup contributor</span></span> |

## <a name="next-steps"></a><span data-ttu-id="39113-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39113-143">Next steps</span></span>
* <span data-ttu-id="39113-144">[역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md): RBAC hello Azure 포털을에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="39113-144">[Role Based Access Control](../active-directory/role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="39113-145">Toomanage로 액세스 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="39113-145">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="39113-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="39113-146">PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="39113-147">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="39113-147">Azure CLI</span></span>](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="39113-148">REST API</span><span class="sxs-lookup"><span data-stu-id="39113-148">REST API</span></span>](../active-directory/role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="39113-149">[역할 기반 액세스 제어 문제 해결](../active-directory/role-based-access-control-troubleshooting.md): 일반적인 문제를 수정하기 위한 제안 사항을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="39113-149">[Role-Based Access Control troubleshooting](../active-directory/role-based-access-control-troubleshooting.md): Get suggestions for fixing common issues.</span></span>
