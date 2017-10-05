---
title: "Azure Analysis Services의 서버 관리자 관리 | Microsoft Docs"
description: "Azure에서 Analysis Services 서버 관리자를 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: a1b58125dafdf73f245b6a8cd0f4917513b22ea9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="11654-103">서버 관리자 관리</span><span class="sxs-lookup"><span data-stu-id="11654-103">Manage server administrators</span></span>
<span data-ttu-id="11654-104">서버 관리자는 서버가 상주하는 테넌트의 Azure AD(Azure Active Directory)에서 유효한 사용자 또는 그룹이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11654-104">Server administrators must be a valid user or group in the Azure Active Directory (Azure AD) for the tenant in which the server resides.</span></span> <span data-ttu-id="11654-105">Azure Portal 또는 SSMS의 서버 속성에서 서버에 대한 제어 블레이드의 **Analysis Services 관리자**를 사용하면 서버 관리자를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11654-105">You can use **Analysis Services Admins** in the control blade for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span></span> 

## <a name="to-add-server-administrators-by-using-azure-portal"></a><span data-ttu-id="11654-106">Azure Portal을 사용하여 서버 관리자를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="11654-106">To add server administrators by using Azure portal</span></span>
1. <span data-ttu-id="11654-107">서버에 대한 제어 블레이드에서 **Analysis Services 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11654-107">In the control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="11654-108">**\<서버 이름> - Analysis Services 관리자** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11654-108">In the **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="11654-109">**서버 관리자 추가** 블레이드에서 Azure AD의 사용자 계정을 선택하거나 이메일 주소를 통해 외부 사용자를 초대합니다.</span><span class="sxs-lookup"><span data-stu-id="11654-109">In the **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Azure Portal의 서버 관리자](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="to-add-server-administrators-by-using-ssms"></a><span data-ttu-id="11654-111">SSMS를 사용하여 서버 관리자를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="11654-111">To add server administrators by using SSMS</span></span>
1. <span data-ttu-id="11654-112">서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="11654-112">Right-click the server > **Properties**.</span></span>
2. <span data-ttu-id="11654-113">**Analysis Server 속성**에서 **보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11654-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="11654-114">**추가**를 클릭한 다음 Azure AD에 있는 사용자 또는 그룹의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="11654-114">Click **Add**, and then enter the email address for a user or group in your Azure AD.</span></span>
   
    ![SSMS에서 서버 관리자 추가](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="11654-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11654-116">Next steps</span></span> 
[<span data-ttu-id="11654-117">인증 및 사용자 권한</span><span class="sxs-lookup"><span data-stu-id="11654-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="11654-118">데이터베이스 역할 및 사용자 관리</span><span class="sxs-lookup"><span data-stu-id="11654-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="11654-119">역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="11654-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

