---
title: "Azure Active Directory Domain Services: SharePoint 사용자 프로필 서비스에 대한 지원을 사용하도록 설정 | Microsoft Docs"
description: "SharePoint Server에 대한 프로필 동기화를 지원하도록 Azure Active Directory Domain Services 관리 도메인 구성"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: c3c923b5c9cd652f0c5b0ec98c1cda740f180122
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-managed-domain-to-support-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="f367a-103">SharePoint Server에 대한 프로필 동기화를 지원하도록 관리 도메인 구성</span><span class="sxs-lookup"><span data-stu-id="f367a-103">Configure a managed domain to support profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="f367a-104">SharePoint Server에는 사용자 프로필 동기화에 사용되는 User Profile Service가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f367a-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="f367a-105">User Profile Service를 설정하려면 Active Directory 도메인에서 적절한 사용 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f367a-105">To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain.</span></span> <span data-ttu-id="f367a-106">자세한 내용은 [SharePoint Server 2013에서 프로필 동기화를 위해 Active Directory Domain Services 사용 권한 부여](https://technet.microsoft.com/library/hh296982.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f367a-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="f367a-107">이 문서에서는 SharePoint Server User Profile Sync Service를 배포하도록 Azure AD 도메인 서비스 관리 도메인을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f367a-107">This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.</span></span>

## <a name="the-aad-dc-service-accounts-group"></a><span data-ttu-id="f367a-108">'AAD DC 서비스 계정' 그룹</span><span class="sxs-lookup"><span data-stu-id="f367a-108">The 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="f367a-109">'**AAD DC 서비스 계정**'이라는 보안 그룹을 관리되는 도메인의 '사용자’ 조직 구성 단위 내에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f367a-109">A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="f367a-110">관리되는 도메인의 **Active Directory 사용자 및 컴퓨터** MMC 스냅인에서 이 그룹을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f367a-110">You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![AAD DC 서비스 계정 보안 그룹](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="f367a-112">이 보안 그룹의 구성원에게 다음 권한이 위임됩니다.</span><span class="sxs-lookup"><span data-stu-id="f367a-112">Members of this security group are delegated the following privileges:</span></span>
- <span data-ttu-id="f367a-113">관리되는 도메인의 루트 DSE에 대한 ‘디렉터리 변경 내용 복제' 권한</span><span class="sxs-lookup"><span data-stu-id="f367a-113">The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.</span></span>
- <span data-ttu-id="f367a-114">관리되는 도메인의 구성 명명 컨텍스트에 대한 ‘디렉터리 변경 내용 복제' 권한.</span><span class="sxs-lookup"><span data-stu-id="f367a-114">The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.</span></span>

<span data-ttu-id="f367a-115">이 보안 그룹은 기본 제공 그룹 **Pre-Windows 2000 Compatible Access**의 구성원이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f367a-115">This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![AAD DC 서비스 계정 보안 그룹](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-to-support-sharepoint-server-user-profile-sync"></a><span data-ttu-id="f367a-117">관리되는 도메인이 SharePoint Server 사용자 프로필 동기화를 지원하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f367a-117">Enable your managed domain to support SharePoint Server user profile sync</span></span>
<span data-ttu-id="f367a-118">SharePoint 사용자 프로필 동기화에 사용되는 서비스 계정을 **AAD DC 서비스 계정** 그룹에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f367a-118">You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="f367a-119">결과적으로 동기화 계정은 디렉터리에 대한 변경 내용을 복제할 수 있는 적절한 권한을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f367a-119">As a result, the synchronization account gets adequate privileges to replicate changes to the directory.</span></span> <span data-ttu-id="f367a-120">이 구성 단계를 수행하면 SharePoint Server 사용자 프로필 동기화가 제대로 작동될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f367a-120">This configuration step enables SharePoint Server user profile sync to work correctly.</span></span>

![AAD DC 서비스 계정 - 구성원 추가](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC 서비스 계정 - 구성원 추가](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="f367a-123">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="f367a-123">Related Content</span></span>
* [<span data-ttu-id="f367a-124">기술 참조 - SharePoint Server 2013에서 프로필 동기화를 위해 Active Directory Domain Services 사용 권한 부여</span><span class="sxs-lookup"><span data-stu-id="f367a-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
