---
title: "aaaAccess 보고-Azure RBAC | Microsoft Docs"
description: "모든 목록에서에서 변경 되는지 액세스 tooyour hello 통해 역할 기반 액세스 제어를 사용한 Azure 구독 지난 90 일 동안 보고서를 생성 합니다."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="cafc8-103">역할 기반 액세스 제어에 대한 액세스 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="cafc8-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="cafc8-104">언제 든 지 다른 사용자 권한을 부여 하거나 구독 내에서 액세스 권한을 취소 hello 변경 내용은 Azure 이벤트에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cafc8-104">Any time someone grants or revokes access within your subscriptions, hello changes get logged in Azure events.</span></span> <span data-ttu-id="cafc8-105">만들 수 있습니다 액세스 변경 기록 보고서 toosee hello에 대 한 모든 변경 내용을 지난 90 일.</span><span class="sxs-lookup"><span data-stu-id="cafc8-105">You can create access change history reports toosee all changes for hello past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="cafc8-106">Azure PowerShell에서 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="cafc8-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="cafc8-107">액세스란 toocreate 변경 기록 보고서에 PowerShell 사용 하 여 hello [Get AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="cafc8-107">toocreate an access change history report in PowerShell, use hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="cafc8-108">이 명령을 호출 하는 경우 원하는 hello 다음 비롯 하 여 나열 된 hello 할당의 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cafc8-108">When you call this command, you can specify which property of hello assignments you want listed, including hello following:</span></span>

| <span data-ttu-id="cafc8-109">속성</span><span class="sxs-lookup"><span data-stu-id="cafc8-109">Property</span></span> | <span data-ttu-id="cafc8-110">설명</span><span class="sxs-lookup"><span data-stu-id="cafc8-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cafc8-111">**작업**</span><span class="sxs-lookup"><span data-stu-id="cafc8-111">**Action**</span></span> |<span data-ttu-id="cafc8-112">액세스를 부여 또는 취소했는지 여부</span><span class="sxs-lookup"><span data-stu-id="cafc8-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="cafc8-113">**Caller**</span><span class="sxs-lookup"><span data-stu-id="cafc8-113">**Caller**</span></span> |<span data-ttu-id="cafc8-114">hello 액세스 담당 hello 소유자 변경</span><span class="sxs-lookup"><span data-stu-id="cafc8-114">hello owner responsible for hello access change</span></span> |
| <span data-ttu-id="cafc8-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="cafc8-115">**PrincipalId**</span></span> | <span data-ttu-id="cafc8-116">hello hello 사용자, 그룹 또는 hello 역할에 할당 된 응용 프로그램의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="cafc8-116">hello unique identifier of hello user, group, or application that was assigned hello role</span></span> |
| <span data-ttu-id="cafc8-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="cafc8-117">**PrincipalName**</span></span> |<span data-ttu-id="cafc8-118">hello 사용자, 그룹 또는 응용 프로그램의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="cafc8-118">hello name of hello user, group, or application</span></span> |
| <span data-ttu-id="cafc8-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="cafc8-119">**PrincipalType**</span></span> |<span data-ttu-id="cafc8-120">사용자, 그룹 또는 응용 프로그램에 대 한 hello 할당 되었는지 여부</span><span class="sxs-lookup"><span data-stu-id="cafc8-120">Whether hello assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="cafc8-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="cafc8-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="cafc8-122">hello 부여 또는 취소 된 hello 역할의 GUID</span><span class="sxs-lookup"><span data-stu-id="cafc8-122">hello GUID of hello role that was granted or revoked</span></span> |
| <span data-ttu-id="cafc8-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="cafc8-123">**RoleName**</span></span> |<span data-ttu-id="cafc8-124">부여 또는 취소 된 hello 역할</span><span class="sxs-lookup"><span data-stu-id="cafc8-124">hello role that was granted or revoked</span></span> |
| <span data-ttu-id="cafc8-125">**범위**</span><span class="sxs-lookup"><span data-stu-id="cafc8-125">**Scope**</span></span> | <span data-ttu-id="cafc8-126">hello 구독, 리소스 그룹 또는 hello 할당 하는 리소스의 고유 식별자 hello 너무 적용</span><span class="sxs-lookup"><span data-stu-id="cafc8-126">hello unique identifier of hello subscription, resource group, or resource that hello assignment applies too</span></span>| 
| <span data-ttu-id="cafc8-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="cafc8-127">**ScopeName**</span></span> |<span data-ttu-id="cafc8-128">hello 구독, 리소스 그룹 또는 리소스의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="cafc8-128">hello name of hello subscription, resource group, or resource</span></span> |
| <span data-ttu-id="cafc8-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="cafc8-129">**ScopeType**</span></span> |<span data-ttu-id="cafc8-130">Hello 구독, 리소스 그룹 또는 리소스 범위에서 hello 할당 되었는지 여부</span><span class="sxs-lookup"><span data-stu-id="cafc8-130">Whether hello assignment was at hello subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="cafc8-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="cafc8-131">**Timestamp**</span></span> |<span data-ttu-id="cafc8-132">액세스 하는 변경 된 hello 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="cafc8-132">hello date and time that access was changed</span></span> |

<span data-ttu-id="cafc8-133">이 예제에서는 명령은 hello 구독 hello에 대 한 모든 액세스 변경 지난 7 일을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="cafc8-133">This example command lists all access changes in hello subscription for hello past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - 스크린샷](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="cafc8-135">Azure CLI에서 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="cafc8-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="cafc8-136">Azure 명령줄 인터페이스 (CLI) hello에 대 한 액세스 변경 기록 보고서 toocreate hello를 사용 하 여 `azure role assignment changelog list` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="cafc8-136">toocreate an access change history report in hello Azure command-line interface (CLI), use hello `azure role assignment changelog list` command.</span></span>

## <a name="export-tooa-spreadsheet"></a><span data-ttu-id="cafc8-137">Tooa 스프레드시트 내보내기</span><span class="sxs-lookup"><span data-stu-id="cafc8-137">Export tooa spreadsheet</span></span>
<span data-ttu-id="cafc8-138">toosave hello 보고서, 데이터 또는 조작 hello를.csv 파일로 내보내기 hello 액세스로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafc8-138">toosave hello report, or manipulate hello data, export hello access changes into a .csv file.</span></span> <span data-ttu-id="cafc8-139">그런 다음 검토를 위해 스프레드시트의 hello 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cafc8-139">You can then view hello report in a spreadsheet for review.</span></span>

![Changelog가 스크린샷으로 표시됨 - 스크린샷](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="cafc8-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cafc8-141">Next steps</span></span>
* <span data-ttu-id="cafc8-142">[Azure RBAC에서 사용자 지정 역할](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="cafc8-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="cafc8-143">자세한 내용은 방법 toomanage [powershell과 함께 Azure RBAC](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="cafc8-143">Learn how toomanage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

