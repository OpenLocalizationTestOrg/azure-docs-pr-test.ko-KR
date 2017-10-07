---
title: "Azure Analysis Services에서 서버 관리자 aaaManage | Microsoft Docs"
description: "자세한 내용은 방법 Azure에서 Analysis Services 서버에 대 한 toomanage 서버 관리자입니다."
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
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a>서버 관리자 관리
서버 관리자는 hello 서버 있는 hello 테 넌 트에 대 한 유효한 사용자 또는 그룹 hello Azure Active Directory (Azure AD)에 있어야 합니다. 사용할 수 있습니다 **Analysis Services 관리자** Azure 포털에서 사용자 서버 또는 SSMS toomanage 서버 관리자에서 서버 속성에 대 한 hello 제어 블레이드에서 합니다. 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a>Azure 포털을 사용 하 여 tooadd 서버 관리자
1. 서버에 대 한 제어 블레이드에서 hello 클릭 **Analysis Services 관리자**합니다.
2. Hello에  **\<서버 이름 >-Analysis Services 관리자** 블레이드에서 클릭 **추가**합니다.
3. Hello에 **서버 관리자 추가** 블레이드를 Azure AD에서 사용자 계정을 선택 하거나 전자 메일 주소를 통해 외부 사용자를 초대 합니다.

    ![Azure Portal의 서버 관리자](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a>SSMS를 사용 하 여 tooadd 서버 관리자
1. Hello 서버를 마우스 오른쪽 단추로 클릭 > **속성**합니다.
2. **Analysis Server 속성**에서 **보안**을 클릭합니다.
3. 클릭 **추가**, Azure AD에 사용자 또는 그룹에 대 한 hello 전자 메일 주소를 입력 합니다.
   
    ![SSMS에서 서버 관리자 추가](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a>다음 단계 
[인증 및 사용자 권한](analysis-services-manage-users.md)  
[데이터베이스 역할 및 사용자 관리](analysis-services-database-users.md)  
[역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md)  

