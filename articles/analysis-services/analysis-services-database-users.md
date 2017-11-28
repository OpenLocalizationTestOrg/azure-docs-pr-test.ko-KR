---
title: "aaaManage 데이터베이스 역할 및 Azure Analysis Services의 사용자 | Microsoft Docs"
description: "역할 및 Azure에는 Analysis Services 서버에서 사용자 toomanage 데이터베이스 하는 방법에 대해 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="f534e-103">데이터베이스 역할 및 사용자 관리</span><span class="sxs-lookup"><span data-stu-id="f534e-103">Manage database roles and users</span></span>

<span data-ttu-id="f534e-104">Hello 모델 데이터베이스 수준에서 모든 사용자에 게 tooa 역할을 속해 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-104">At hello model database level, all users must belong tooa role.</span></span> <span data-ttu-id="f534e-105">역할은 hello model 데이터베이스에 대 한 특정 사용 권한이 있는 사용자를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-105">Roles define users with particular permissions for hello model database.</span></span> <span data-ttu-id="f534e-106">모든 사용자 또는 보안 그룹 추가 tooa 역할 hello에 Azure AD 테 넌 트의 계정이 있어야 hello 서버와 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-106">Any user or security group added tooa role must have an account in an Azure AD tenant in hello same subscription as hello server.</span></span>

<span data-ttu-id="f534e-107">역할을 정의 하는 방법에 hello 도구를 사용 하면 다른 따라 않으며 hello 효과 동일 hello는입니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-107">How you define roles is different depending on hello tool you use, but hello effect is hello same.</span></span>

<span data-ttu-id="f534e-108">역할 권한은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-108">Role permissions include:</span></span>
*  <span data-ttu-id="f534e-109">**관리자** -사용자가 있는 hello 데이터베이스에 대 한 모든 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-109">**Administrator** - Users have full permissions for hello database.</span></span> <span data-ttu-id="f534e-110">관리자 권한이 있는 데이터베이스 역할은 서버 관리자와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="f534e-111">**프로세스** -사용자가 tooand 연결할 수 hello 데이터베이스에서 프로세스 작업을 수행 하 고 모델 데이터베이스 데이터를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-111">**Process** - Users can connect tooand perform process operations on hello database, and analyze model database data.</span></span>
*  <span data-ttu-id="f534e-112">**읽기** -는 클라이언트를 사용 하 여 사용자가 응용 프로그램 tooconnect tooand 모델 데이터베이스 데이터를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-112">**Read** -  Users can use a client application tooconnect tooand analyze model database data.</span></span>

<span data-ttu-id="f534e-113">테이블 형식 모델 프로젝트를 만들 때 역할 만들고 SSDT의 역할 관리자를 사용 하 여 사용자 또는 그룹 toothose 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-113">When creating a tabular model project, you create roles and add users or groups toothose roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="f534e-114">배포 된 tooa 서버를 사용 하는 경우 SSMS [Analysis Services PowerShell cmdlet](https://msdn.microsoft.com/library/hh758425.aspx), 또는 [테이블 형식 모델 스크립팅 언어](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd 또는 역할 및 사용자 멤버를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-114">When deployed tooa server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd or remove roles and user members.</span></span>

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="f534e-115">tooadd 또는 역할 및 SSDT의 사용자 관리</span><span class="sxs-lookup"><span data-stu-id="f534e-115">tooadd or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="f534e-116">SSDT > **테이블 형식 모델 탐색기**에서 **역할**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="f534e-117">**역할 관리자**에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="f534e-118">Hello 역할에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-118">Type a name for hello role.</span></span>  
  
     <span data-ttu-id="f534e-119">기본적으로 hello 이름 hello 기본 역할의 각 새 역할에 대해 매겨집니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-119">By default, hello name of hello default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="f534e-120">예를 들어 재무 관리자 또는 인적 자원 전문가 hello 멤버 유형을 분명 하 게 식별 하는 이름을 입력 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-120">It's recommended you type a name that clearly identifies hello member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="f534e-121">다음 권한을 hello 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-121">Select one of hello following permissions:</span></span>  
  
    |<span data-ttu-id="f534e-122">사용 권한</span><span class="sxs-lookup"><span data-stu-id="f534e-122">Permission</span></span>|<span data-ttu-id="f534e-123">설명</span><span class="sxs-lookup"><span data-stu-id="f534e-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="f534e-124">**없음**</span><span class="sxs-lookup"><span data-stu-id="f534e-124">**None**</span></span>|<span data-ttu-id="f534e-125">멤버는 hello 모델 스키마를 수정할 수 없습니다 및 데이터를 쿼리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-125">Members cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="f534e-126">**읽기**</span><span class="sxs-lookup"><span data-stu-id="f534e-126">**Read**</span></span>|<span data-ttu-id="f534e-127">멤버 (행 필터에 기반) 데이터를 쿼리할 수 있지만 hello 모델 스키마를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-127">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="f534e-128">**읽기 및 처리**</span><span class="sxs-lookup"><span data-stu-id="f534e-128">**Read and Process**</span></span>|<span data-ttu-id="f534e-129">멤버는 데이터 (에 따라 행 수준 필터) 및 실행된 처리 및 모두 처리 작업을 쿼리할 수 있지만 hello 모델 스키마를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="f534e-130">**프로세스**</span><span class="sxs-lookup"><span data-stu-id="f534e-130">**Process**</span></span>|<span data-ttu-id="f534e-131">멤버는 처리 및 모두 처리 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="f534e-132">Hello 모델 스키마를 수정할 수 없습니다 및 데이터를 쿼리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-132">Cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="f534e-133">**관리자**</span><span class="sxs-lookup"><span data-stu-id="f534e-133">**Administrator**</span></span>|<span data-ttu-id="f534e-134">멤버는 hello 모델 스키마를 수정 하 고 모든 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-134">Members can modify hello model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="f534e-135">hello 역할 만들기에 대 한 읽기 또는 읽기 및 처리 권한을 DAX 수식을 사용 하 여 행 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-135">If hello role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="f534e-136">Hello 클릭 **행 필터** 탭, 다음 테이블을 클릭 한 다음 hello **DAX 필터** 필드를 선택한 다음 DAX 수식을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-136">Click hello **Row Filters** tab, then select a table, then click hello **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="f534e-137">**멤버** > **외부 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="f534e-138">**외부 멤버 추가**에서 Azure AD 테넌트의 사용자 또는 그룹을 메일 주소로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="f534e-139">[확인]을 클릭하고 [역할 관리자]를 닫으면 역할 및 역할 멤버가 [테이블 형식 모델 탐색기]에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![테이블 형식 모델 탐색기의 역할 및 사용자](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="f534e-141">Tooyour Azure Analysis Services 서버를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-141">Deploy tooyour Azure Analysis Services server.</span></span>


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="f534e-142">tooadd 또는 역할 및 SSMS에서 사용자 관리</span><span class="sxs-lookup"><span data-stu-id="f534e-142">tooadd or manage roles and users in SSMS</span></span>
<span data-ttu-id="f534e-143">역할 및 사용자 tooa tooadd 배포 된 모델 데이터베이스, 서버 관리자 또는 관리자 권한 가진 데이터베이스 역할에 이미 연결 된 toohello 서버 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-143">tooadd roles and users tooa deployed model database, you must be connected toohello server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="f534e-144">개체 탐색기에서 **역할**을 마우스 오른쪽 단추로 클릭 > **새 역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="f534e-145">**역할 만들기**에서 역할 이름 및 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="f534e-146">사용 권한을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-146">Select a permission.</span></span>
   |<span data-ttu-id="f534e-147">사용 권한</span><span class="sxs-lookup"><span data-stu-id="f534e-147">Permission</span></span>|<span data-ttu-id="f534e-148">설명</span><span class="sxs-lookup"><span data-stu-id="f534e-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="f534e-149">**모든 권한(관리자)**</span><span class="sxs-lookup"><span data-stu-id="f534e-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="f534e-150">구성원 hello 모델 스키마를 수정할 수 있습니다, 처리 하 고 모든 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-150">Members can modify hello model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="f534e-151">**데이터베이스 처리**</span><span class="sxs-lookup"><span data-stu-id="f534e-151">**Process database**</span></span>|<span data-ttu-id="f534e-152">멤버는 처리 및 모두 처리 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="f534e-153">Hello 모델 스키마를 수정할 수 없습니다 및 데이터를 쿼리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-153">Cannot modify hello model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="f534e-154">**읽기**</span><span class="sxs-lookup"><span data-stu-id="f534e-154">**Read**</span></span>|<span data-ttu-id="f534e-155">멤버 (행 필터에 기반) 데이터를 쿼리할 수 있지만 hello 모델 스키마를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-155">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
  
4. <span data-ttu-id="f534e-156">**멤버 자격**을 클릭한 다음 Azure AD 테넌트의 사용자나 그룹을 메일 주소로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![사용자 추가](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="f534e-158">만들려는 hello 역할에 읽기 권한이 있는 경우에 DAX 수식을 사용 하 여 행 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-158">If hello role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="f534e-159">클릭 **행 필터**테이블을 선택 하 고 hello에서 DAX 수식을 입력 합니다 **DAX 필터** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-159">Click **Row Filters**, select a table, and then type a DAX formula in hello **DAX Filter** field.</span></span> 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="f534e-160">tooadd 역할 및 TMSL 스크립트를 사용 하 여 사용자</span><span class="sxs-lookup"><span data-stu-id="f534e-160">tooadd roles and users by using a TMSL script</span></span>
<span data-ttu-id="f534e-161">SSMS에서 또는 PowerShell을 사용 하 여 hello XMLA 창에 TMSL 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-161">You can run a TMSL script in hello XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="f534e-162">사용 하 여 hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) 명령과 hello [역할](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-162">Use hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and hello [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="f534e-163">**샘플 TMSL 스크립트**</span><span class="sxs-lookup"><span data-stu-id="f534e-163">**Sample TMSL script**</span></span>

<span data-ttu-id="f534e-164">이 샘플에서는 B2B 외부 사용자와 그룹 hello SalesBI 데이터베이스에 대 한 읽기 권한 가진 toohello 분석가 역할을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-164">In this sample, a B2B external user and a group are added toohello Analyst role with Read permissions for hello SalesBI database.</span></span> <span data-ttu-id="f534e-165">둘 다 hello 외부 사용자 및 그룹 같은 Azure AD 테 넌 트에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-165">Both hello external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a><span data-ttu-id="f534e-166">tooadd 역할 및 PowerShell을 사용 하 여 사용자</span><span class="sxs-lookup"><span data-stu-id="f534e-166">tooadd roles and users by using PowerShell</span></span>
<span data-ttu-id="f534e-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) 모듈은 작업 별로 데이터베이스 관리 cmdlet 및 hello 범용 Invoke-ascmd cmdlet 스크립팅 언어 TMSL (Tabular Model) 쿼리 또는 스크립트를 허용 하를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and hello general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="f534e-168">hello cmdlet을 다음 데이터베이스 역할 및 사용자 관리에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-168">hello following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="f534e-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="f534e-169">Cmdlet</span></span>|<span data-ttu-id="f534e-170">설명</span><span class="sxs-lookup"><span data-stu-id="f534e-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="f534e-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="f534e-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="f534e-172">Tooa 데이터베이스 역할 구성원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-172">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="f534e-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="f534e-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="f534e-174">데이터베이스 역할에서 구성원을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="f534e-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="f534e-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="f534e-176">TMSL 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="f534e-177">행 필터</span><span class="sxs-lookup"><span data-stu-id="f534e-177">Row filters</span></span>  
<span data-ttu-id="f534e-178">행 필터는 특정 역할의 멤버가 쿼리할 수 있는 테이블의 행을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="f534e-179">행 필터는 DAX 수식을 사용하여 모델의 각 테이블에 대해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="f534e-180">행 필터는 읽기와 읽기 및 처리 권한이 있는 역할에 대해서만 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="f534e-181">기본적으로 특정 테이블에 대 한 행 필터 정의 되지 않은 경우 다른 테이블에서 교차 필터링이 적용 하지 않는 한 멤버 hello 테이블의 모든 행에 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-181">By default, if a row filter is not defined for a particular table, members  can query all rows in hello table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="f534e-182">행 필터 tooa TRUE/FALSE 값, 해당 역할의 멤버가 쿼리할 수 있는 toodefine hello 행을 평가 해야 하는 DAX 수식을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-182">Row filters require a DAX formula, which must evaluate tooa TRUE/FALSE value, toodefine hello rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="f534e-183">Hello DAX 수식에에서 포함 되지 않은 행을 쿼리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-183">Rows not included in hello DAX formula cannot be queried.</span></span> <span data-ttu-id="f534e-184">예를 들어 다음 행 필터 식은 hello로 Customers 테이블을 hello *고객 [Country] = = "미국"*, hello Sales 역할의 멤버인 hello USA의에서 고객만 볼만 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-184">For example, hello Customers table with hello following row filters expression, *=Customers [Country] = “USA”*, members of hello Sales role can only see customers in hello USA.</span></span>  
  
<span data-ttu-id="f534e-185">행 필터 적용 toohello 지정 된 행과 관련 된 행입니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-185">Row filters apply toohello specified rows and related rows.</span></span> <span data-ttu-id="f534e-186">테이블에 여러 관계가 있는 경우 필터는 hello는 활성 관계에 대 한 보안을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-186">When a table has multiple relationships, filters apply security for hello relationship that is active.</span></span> <span data-ttu-id="f534e-187">행 필터는 관련 테이블에 대해 정의된 다른 행 필터와 교차됩니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="f534e-188">테이블</span><span class="sxs-lookup"><span data-stu-id="f534e-188">Table</span></span>|<span data-ttu-id="f534e-189">DAX 식</span><span class="sxs-lookup"><span data-stu-id="f534e-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="f534e-190">지역</span><span class="sxs-lookup"><span data-stu-id="f534e-190">Region</span></span>|<span data-ttu-id="f534e-191">=Region[Country]=”USA”</span><span class="sxs-lookup"><span data-stu-id="f534e-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="f534e-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="f534e-192">ProductCategory</span></span>|<span data-ttu-id="f534e-193">=ProductCategory[Name]=”Bicycles”</span><span class="sxs-lookup"><span data-stu-id="f534e-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="f534e-194">트랜잭션</span><span class="sxs-lookup"><span data-stu-id="f534e-194">Transactions</span></span>|<span data-ttu-id="f534e-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="f534e-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="f534e-196">hello 순수 효과 멤버를 hello 고객이 hello 미국에, hello 제품 범주, bicycles 이며 hello year가 2016 데이터 행을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-196">hello net effect is members can query rows of data where hello customer is in hello USA, hello product category is bicycles, and hello year is 2016.</span></span> <span data-ttu-id="f534e-197">사용자가 되지 않은 트랜잭션은 자전거나 트랜잭션을 하지 2016에는 이러한 권한을 부여 하는 다른 역할의 멤버가 아닌 hello 미국 이외의 국가에서 발생을 쿼리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-197">Users cannot query transactions outside of hello USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="f534e-198">Hello 필터를 사용할 수 있습니다 *=FALSE()*, 전체 테이블에 대 한 toodeny 액세스 tooall 행입니다.</span><span class="sxs-lookup"><span data-stu-id="f534e-198">You can use hello filter, *=FALSE()*, toodeny access tooall rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f534e-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f534e-199">Next steps</span></span>
  <span data-ttu-id="f534e-200">[서버 관리자 관리](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="f534e-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="f534e-201">PowerShell을 사용하여 Azure Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="f534e-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="f534e-202">TMSL(테이블 형식 모델 스크립트 언어) 참조</span><span class="sxs-lookup"><span data-stu-id="f534e-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

