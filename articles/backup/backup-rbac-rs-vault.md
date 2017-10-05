---
title: "역할 기반 액세스 제어를 사용하여 백업 관리 | Microsoft Docs"
description: "역할 기반 액세스 제어를 사용하여 Recovery Services 자격 증명 모음의 백업 관리 작업에 대한 액세스를 관리합니다."
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
ms.openlocfilehash: d0b6eb8eea8971eb8f80c6623f9a41a3692241b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-role-based-access-control-to-manage-azure-backup-recovery-points"></a><span data-ttu-id="22aa8-103">역할 기반 액세스 제어를 사용하여 Azure Backup 복구 지점 관리</span><span class="sxs-lookup"><span data-stu-id="22aa8-103">Use Role-Based Access Control to manage Azure Backup recovery points</span></span>
<span data-ttu-id="22aa8-104">Azure RBAC(역할 기반 액세스 제어)를 통해 Azure에 대한 세밀한 액세스 관리가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-104">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="22aa8-105">RBAC를 사용하면 팀 내에서 업무를 분리하고 사용자에게 해당 작업을 수행하는 데 필요한 만큼의 권한만 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-105">Using RBAC, you can segregate duties within your team and grant only the amount of access to users that they need to perform their jobs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22aa8-106">Azure Backup에서 제공하는 역할은 Azure Portal 또는 Recovery Services 자격 증명 모음 PowerShell cmdlet에서 수행할 수 있는 작업으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-106">Roles provided by Azure Backup are limited to actions that can be performed in Azure portal or Recovery Services vault PowerShell cmdlets.</span></span> <span data-ttu-id="22aa8-107">Azure 백업 에이전트 클라이언트 UI, System Center Data Protection Manager UI 또는 Azure Backup Server UI에서 실행되는 작업은 이러한 역할의 제어를 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-107">Actions performed in Azure backup Agent Client UI or System center Data Protection Manager UI or Azure Backup Server UI are out of control of these roles.</span></span>

<span data-ttu-id="22aa8-108">Azure Backup은 백업 관리 작업을 제어할 수 있는 기본 제공 역할을 3개 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-108">Azure Backup provides 3 built-in roles to control backup management operations.</span></span> <span data-ttu-id="22aa8-109">[Azure RBAC 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="22aa8-109">Learn more on [Azure RBAC built-in roles](../active-directory/role-based-access-built-in-roles.md)</span></span>

* <span data-ttu-id="22aa8-110">[Backup 참여자](../active-directory/role-based-access-built-in-roles.md#backup-contributor) - 이 역할은 Recovery Services 자격 증명 모음을 만들고 다른 사용자에 대한 액세스 권한을 제공하는 권한을 제외하고, 백업을 만들고 관리하는 모든 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-110">[Backup Contributor](../active-directory/role-based-access-built-in-roles.md#backup-contributor) - This role has all permissions to create and manage backup except creating Recovery Services vault and giving access to others.</span></span> <span data-ttu-id="22aa8-111">모든 백업 관리 작업을 수행할 수 있는 백업 관리 관리자 역할로 생각하시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-111">Imagine this role as admin of backup management who can do every backup management operation.</span></span>
* <span data-ttu-id="22aa8-112">[Backup 운영자](../active-directory/role-based-access-built-in-roles.md#backup-operator) - 이 역할은 백업을 제거하고 백업 정책을 관리하는 권한을 제외하고, 참여자가 할 수 있는 모든 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-112">[Backup Operator](../active-directory/role-based-access-built-in-roles.md#backup-operator) - This role has permissions to everything a contributor does except removing backup and managing backup policies.</span></span> <span data-ttu-id="22aa8-113">이 역할은 온-프레미스 리소스의 데이터 삭제나 등록 제거를 통해 백업을 중지하는 작업처럼 안전하지 않은 작업을 수행할 수 없다는 점만 빼면 참여자와 똑같습니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-113">This role is equivalent to contributor except it can't perform destructive operations such as stop backup with delete data or remove registration of on-premises resources.</span></span>
* <span data-ttu-id="22aa8-114">[Backup 읽기 권한자](../active-directory/role-based-access-built-in-roles.md#backup-reader) - 이 역할은 모든 백업 관리 작업을 볼 수 있는 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-114">[Backup Reader](../active-directory/role-based-access-built-in-roles.md#backup-reader) - This role has permissions to view all backup management operations.</span></span> <span data-ttu-id="22aa8-115">이 역할을 모니터링 요원으로 생각하시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-115">Imagine this role to be a monitoring person.</span></span>

<span data-ttu-id="22aa8-116">더 많은 제어를 위해 사용자 고유의 역할을 정의하려는 경우 Azure RBAC에서 [사용자 지정 역할을 빌드](../active-directory/role-based-access-control-custom-roles.md)하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22aa8-116">If you're looking to define your own roles for even more control, see how to [build Custom roles](../active-directory/role-based-access-control-custom-roles.md) in Azure RBAC.</span></span>



## <a name="mapping-backup-built-in-roles-to-backup-management-actions"></a><span data-ttu-id="22aa8-117">Backup 기본 제공 역할을 관리 작업에 매핑</span><span class="sxs-lookup"><span data-stu-id="22aa8-117">Mapping Backup built-in roles to backup management actions</span></span>
<span data-ttu-id="22aa8-118">다음 테이블은 Backup 관리 작업과 해당 작업을 수행하는 데 필요한 최소 RBAC 역할을 캡처한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-118">The following table captures the Backup management actions and corresponding minimum RBAC role required to perform that operation.</span></span>

| <span data-ttu-id="22aa8-119">관리 작업</span><span class="sxs-lookup"><span data-stu-id="22aa8-119">Management Operation</span></span> | <span data-ttu-id="22aa8-120">필요한 최소 RBAC 역할</span><span class="sxs-lookup"><span data-stu-id="22aa8-120">Minimum RBAC role required</span></span> |
| --- | --- |
| <span data-ttu-id="22aa8-121">Recovery Services 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="22aa8-121">Create Recovery Services vault</span></span> | <span data-ttu-id="22aa8-122">자격 증명 모음 리소스 그룹의 참여자</span><span class="sxs-lookup"><span data-stu-id="22aa8-122">Contributor on Resource group of vault</span></span> |
| <span data-ttu-id="22aa8-123">Azure VM의 백업 활성화</span><span class="sxs-lookup"><span data-stu-id="22aa8-123">Enable backup of Azure VMs</span></span> | <span data-ttu-id="22aa8-124">자격 증명 모음의 Backup 운영자, VM의 가상 컴퓨터 참여자</span><span class="sxs-lookup"><span data-stu-id="22aa8-124">Backup Operator on vault, Virtual machine contributor on VMs</span></span> |
| <span data-ttu-id="22aa8-125">VM의 주문형 백업</span><span class="sxs-lookup"><span data-stu-id="22aa8-125">On-demand backup of VM</span></span> | <span data-ttu-id="22aa8-126">Backup 운영자</span><span class="sxs-lookup"><span data-stu-id="22aa8-126">Backup operator</span></span> |
| <span data-ttu-id="22aa8-127">VM 복원</span><span class="sxs-lookup"><span data-stu-id="22aa8-127">Restore VM</span></span> | <span data-ttu-id="22aa8-128">Backup 운영자, VM 및 Vnet이 배포될 리소스 그룹 참여자</span><span class="sxs-lookup"><span data-stu-id="22aa8-128">Backup operator, Resource group contributor in which VM and Vnets are going to get deployed</span></span> |
| <span data-ttu-id="22aa8-129">디스크, VM 백업의 개별 파일 복원</span><span class="sxs-lookup"><span data-stu-id="22aa8-129">Restore disks, individual files from VM backup</span></span> | <span data-ttu-id="22aa8-130">Backup 운영자</span><span class="sxs-lookup"><span data-stu-id="22aa8-130">Backup operator</span></span> |
| <span data-ttu-id="22aa8-131">Azure VM 백업에 대한 백업 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="22aa8-131">Create backup policy for Azure VM backup</span></span> | <span data-ttu-id="22aa8-132">Backup 참여자</span><span class="sxs-lookup"><span data-stu-id="22aa8-132">Backup contributor</span></span> |
| <span data-ttu-id="22aa8-133">Azure VM 백업의 백업 정책 수정</span><span class="sxs-lookup"><span data-stu-id="22aa8-133">Modify backup policy of Azure VM backup</span></span> | <span data-ttu-id="22aa8-134">Backup 참여자</span><span class="sxs-lookup"><span data-stu-id="22aa8-134">Backup contributor</span></span> |
| <span data-ttu-id="22aa8-135">Azure VM 백업의 백업 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="22aa8-135">Delete backup policy of Azure VM backup</span></span> | <span data-ttu-id="22aa8-136">Backup 참여자</span><span class="sxs-lookup"><span data-stu-id="22aa8-136">Backup contributor</span></span> |
| <span data-ttu-id="22aa8-137">VM 백업에서 백업 중지(데이터 보존 또는 데이터 삭제를 통해)</span><span class="sxs-lookup"><span data-stu-id="22aa8-137">Stop backup (with retain data or delete data) on VM backup</span></span> | <span data-ttu-id="22aa8-138">Backup 참여자</span><span class="sxs-lookup"><span data-stu-id="22aa8-138">Backup contributor</span></span> |
| <span data-ttu-id="22aa8-139">온-프레미스 Windows 서버/클라이언트/SCDPM 또는 Azure Backup Server 등록</span><span class="sxs-lookup"><span data-stu-id="22aa8-139">Register on-premises Windows Server/client/SCDPM or Azure Backup Server</span></span> | <span data-ttu-id="22aa8-140">Backup 운영자</span><span class="sxs-lookup"><span data-stu-id="22aa8-140">Backup operator</span></span> |
| <span data-ttu-id="22aa8-141">등록된 온-프레미스 Windows 서버/클라이언트/SCDPM 또는 Azure Backup Server 삭제</span><span class="sxs-lookup"><span data-stu-id="22aa8-141">Delete registered on-premises Windows Server/client/SCDPM or Azure Backup Server</span></span> | <span data-ttu-id="22aa8-142">Backup 참여자</span><span class="sxs-lookup"><span data-stu-id="22aa8-142">Backup contributor</span></span> |

## <a name="next-steps"></a><span data-ttu-id="22aa8-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22aa8-143">Next steps</span></span>
* <span data-ttu-id="22aa8-144">[역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md): Azure 포털에서 RBAC를 통해 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-144">[Role Based Access Control](../active-directory/role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="22aa8-145">다음을 사용하여 액세스를 관리하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-145">Learn how to manage access with:</span></span>
  * [<span data-ttu-id="22aa8-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22aa8-146">PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="22aa8-147">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="22aa8-147">Azure CLI</span></span>](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="22aa8-148">REST API</span><span class="sxs-lookup"><span data-stu-id="22aa8-148">REST API</span></span>](../active-directory/role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="22aa8-149">[역할 기반 액세스 제어 문제 해결](../active-directory/role-based-access-control-troubleshooting.md): 일반적인 문제를 수정하기 위한 제안 사항을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="22aa8-149">[Role-Based Access Control troubleshooting](../active-directory/role-based-access-control-troubleshooting.md): Get suggestions for fixing common issues.</span></span>
