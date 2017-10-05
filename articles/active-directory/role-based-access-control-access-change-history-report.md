---
title: "액세스 보고 - Azure RBAC | Microsoft Docs"
description: "지난 90일 동안 역할 기반 액세스 제어와 함께 Azure 구독 액세스에 대한 모든  변경 내용을 나열하는 보고서를 생성합니다."
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
ms.openlocfilehash: 4e8028ab43ed02ef0c0a1374326b07f72f97d9d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="fe82d-103">역할 기반 액세스 제어에 대한 액세스 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="fe82d-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="fe82d-104">언제든지 누군가가 구독 내부의 액세스를 부여하거나 취소하면 변경 내용이 Azure 이벤트에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe82d-104">Any time someone grants or revokes access within your subscriptions, the changes get logged in Azure events.</span></span> <span data-ttu-id="fe82d-105">지난 90일 동안 모든 변경 내용을 보려면 액세스 변경 기록 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe82d-105">You can create access change history reports to see all changes for the past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="fe82d-106">Azure PowerShell에서 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="fe82d-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="fe82d-107">PowerShell에서 액세스 변경 기록 보고서를 만들려면 [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe82d-107">To create an access change history report in PowerShell, use the [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="fe82d-108">이 명령을 호출하는 경우 다음을 비롯하여 나열하려는 할당의 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe82d-108">When you call this command, you can specify which property of the assignments you want listed, including the following:</span></span>

| <span data-ttu-id="fe82d-109">속성</span><span class="sxs-lookup"><span data-stu-id="fe82d-109">Property</span></span> | <span data-ttu-id="fe82d-110">설명</span><span class="sxs-lookup"><span data-stu-id="fe82d-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe82d-111">**작업**</span><span class="sxs-lookup"><span data-stu-id="fe82d-111">**Action**</span></span> |<span data-ttu-id="fe82d-112">액세스를 부여 또는 취소했는지 여부</span><span class="sxs-lookup"><span data-stu-id="fe82d-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="fe82d-113">**Caller**</span><span class="sxs-lookup"><span data-stu-id="fe82d-113">**Caller**</span></span> |<span data-ttu-id="fe82d-114">액세스 변경을 담당하는 소유자</span><span class="sxs-lookup"><span data-stu-id="fe82d-114">The owner responsible for the access change</span></span> |
| <span data-ttu-id="fe82d-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="fe82d-115">**PrincipalId**</span></span> | <span data-ttu-id="fe82d-116">역할이 할당된 사용자, 그룹 또는 응용 프로그램의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="fe82d-116">The unique identifier of the user, group, or application that was assigned the role</span></span> |
| <span data-ttu-id="fe82d-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="fe82d-117">**PrincipalName**</span></span> |<span data-ttu-id="fe82d-118">사용자, 그룹 또는 응용 프로그램의 이름</span><span class="sxs-lookup"><span data-stu-id="fe82d-118">The name of the user, group, or application</span></span> |
| <span data-ttu-id="fe82d-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="fe82d-119">**PrincipalType**</span></span> |<span data-ttu-id="fe82d-120">사용자, 그룹 또는 응용 프로그램에 대한 할당인지 여부</span><span class="sxs-lookup"><span data-stu-id="fe82d-120">Whether the assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="fe82d-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="fe82d-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="fe82d-122">부여되었거나 해지된 역할의 GUID</span><span class="sxs-lookup"><span data-stu-id="fe82d-122">The GUID of the role that was granted or revoked</span></span> |
| <span data-ttu-id="fe82d-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="fe82d-123">**RoleName**</span></span> |<span data-ttu-id="fe82d-124">부여되었거나 해지된 역할</span><span class="sxs-lookup"><span data-stu-id="fe82d-124">The role that was granted or revoked</span></span> |
| <span data-ttu-id="fe82d-125">**범위**</span><span class="sxs-lookup"><span data-stu-id="fe82d-125">**Scope**</span></span> | <span data-ttu-id="fe82d-126">할당이 적용되는 구독, 리소스 그룹 또는 리소스의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="fe82d-126">The unique identifier of the subscription, resource group, or resource that the assignment applies to</span></span> | 
| <span data-ttu-id="fe82d-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="fe82d-127">**ScopeName**</span></span> |<span data-ttu-id="fe82d-128">구독, 리소스 그룹 또는 리소스의 이름</span><span class="sxs-lookup"><span data-stu-id="fe82d-128">The name of the subscription, resource group, or resource</span></span> |
| <span data-ttu-id="fe82d-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="fe82d-129">**ScopeType**</span></span> |<span data-ttu-id="fe82d-130">할당이 구독, 리소스 그룹 또는 리소스 범위에서 이루어졌는지 여부</span><span class="sxs-lookup"><span data-stu-id="fe82d-130">Whether the assignment was at the subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="fe82d-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="fe82d-131">**Timestamp**</span></span> |<span data-ttu-id="fe82d-132">액세스가 변경된 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="fe82d-132">The date and time that access was changed</span></span> |

<span data-ttu-id="fe82d-133">이 예제 명령은 지난 7일 동안 구독에서 발생한 모든 액세스 변경 내용을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fe82d-133">This example command lists all access changes in the subscription for the past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - 스크린샷](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="fe82d-135">Azure CLI에서 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="fe82d-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="fe82d-136">Azure 명령줄 인터페이스(CLI)에서 액세스 변경 기록 보고서를 만들려면 `azure role assignment changelog list` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe82d-136">To create an access change history report in the Azure command-line interface (CLI), use the `azure role assignment changelog list` command.</span></span>

## <a name="export-to-a-spreadsheet"></a><span data-ttu-id="fe82d-137">스프레드시트로 내보내기</span><span class="sxs-lookup"><span data-stu-id="fe82d-137">Export to a spreadsheet</span></span>
<span data-ttu-id="fe82d-138">보고서를 저장하거나 데이터를 조작하거나 액세스 변경을 .csv 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe82d-138">To save the report, or manipulate the data, export the access changes into a .csv file.</span></span> <span data-ttu-id="fe82d-139">그런 다음 검토를 위해 스프레드시트에서 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe82d-139">You can then view the report in a spreadsheet for review.</span></span>

![Changelog가 스크린샷으로 표시됨 - 스크린샷](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="fe82d-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe82d-141">Next steps</span></span>
* <span data-ttu-id="fe82d-142">[Azure RBAC에서 사용자 지정 역할](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="fe82d-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="fe82d-143">[PowerShell을 사용하여 Azure RBAC](role-based-access-control-manage-access-powershell.md)를 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fe82d-143">Learn how to manage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

