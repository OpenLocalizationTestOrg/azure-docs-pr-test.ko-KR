---
title: "Azure Active Directory Domain Services: SharePoint 사용자 프로필 서비스에 대한 지원을 사용하도록 설정 | Microsoft Docs"
description: "SharePoint 서버에 대 한 Azure Active Directory 도메인 서비스 관리 되는 도메인 toosupport 프로필 동기화 구성"
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
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="81450-103">SharePoint 서버에 대 한 관리 되는 도메인 toosupport 프로필 동기화 구성</span><span class="sxs-lookup"><span data-stu-id="81450-103">Configure a managed domain toosupport profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="81450-104">SharePoint Server에는 사용자 프로필 동기화에 사용되는 User Profile Service가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81450-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="81450-105">사용자 프로필 서비스 hello tooset, 적절 한 사용 권한을 toobe Active Directory 도메인에 부여할 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="81450-105">tooset up hello User Profile Service, appropriate permissions need toobe granted on an Active Directory domain.</span></span> <span data-ttu-id="81450-106">자세한 내용은 [SharePoint Server 2013에서 프로필 동기화를 위해 Active Directory Domain Services 사용 권한 부여](https://technet.microsoft.com/library/hh296982.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81450-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="81450-107">이 문서에서는 Azure AD 도메인 서비스 관리 되는 도메인 toodeploy hello SharePoint 서버 사용자 프로필 동기화 서비스를 구성 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="81450-107">This article explains how you can configure Azure AD Domain Services managed domains toodeploy hello SharePoint Server User Profile Sync service.</span></span>

## <a name="hello-aad-dc-service-accounts-group"></a><span data-ttu-id="81450-108">hello ' AAD DC Service Accounts' 그룹</span><span class="sxs-lookup"><span data-stu-id="81450-108">hello 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="81450-109">라는 보안 그룹이 '**AAD DC 서비스 계정을**' hello '사용자' 관리 되는 도메인에 조직 구성 단위 내에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81450-109">A security group called '**AAD DC Service Accounts**' is available within hello 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="81450-110">Hello에이 그룹을 확인할 수 **Active Directory 사용자 및 컴퓨터** MMC 스냅인에서 관리 되는 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="81450-110">You can see this group in hello **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![AAD DC 서비스 계정 보안 그룹](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="81450-112">이 보안 그룹의 구성원은 다음 권한을 위임 된 hello:</span><span class="sxs-lookup"><span data-stu-id="81450-112">Members of this security group are delegated hello following privileges:</span></span>
- <span data-ttu-id="81450-113">hello 루트 DSE의 hello에 대 한 hello' 디렉터리 변경 내용 복제 ' 권한이 도메인을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="81450-113">hello 'Replicate Directory Changes' privilege on hello root DSE of hello managed domain.</span></span>
- <span data-ttu-id="81450-114">hello 구성 명명 컨텍스트 hello에 대 한 ' 디렉터리 변경 내용 복제 ' 권한이 (cn = configuration 컨테이너) hello의 도메인을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="81450-114">hello 'Replicate Directory Changes' privilege on hello Configuration naming context (cn=configuration container) of hello managed domain.</span></span>

<span data-ttu-id="81450-115">이 보안 그룹 hello 기본 제공 그룹의 멤버 이기도 **Pre-Windows 2000 Compatible Access**합니다.</span><span class="sxs-lookup"><span data-stu-id="81450-115">This security group is also a member of hello built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![AAD DC 서비스 계정 보안 그룹](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a><span data-ttu-id="81450-117">사용자 관리 되는 도메인 toosupport SharePoint 서버 사용자 프로필 동기화를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="81450-117">Enable your managed domain toosupport SharePoint Server user profile sync</span></span>
<span data-ttu-id="81450-118">SharePoint 사용자 프로필 동기화 toohello에 사용 되는 hello 서비스 계정을 추가할 수 있습니다 **AAD DC 서비스 계정을** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="81450-118">You can add hello service account used for SharePoint user profile synchronization toohello **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="81450-119">결과적으로, hello 동기화 계정 적절 한 권한을 tooreplicate 변경 toohello 디렉터리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="81450-119">As a result, hello synchronization account gets adequate privileges tooreplicate changes toohello directory.</span></span> <span data-ttu-id="81450-120">이 구성 단계는 SharePoint 서버 사용자 프로필 동기화 toowork를 올바르게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81450-120">This configuration step enables SharePoint Server user profile sync toowork correctly.</span></span>

![AAD DC 서비스 계정 - 구성원 추가](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC 서비스 계정 - 구성원 추가](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="81450-123">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="81450-123">Related Content</span></span>
* [<span data-ttu-id="81450-124">기술 참조 - SharePoint Server 2013에서 프로필 동기화를 위해 Active Directory Domain Services 사용 권한 부여</span><span class="sxs-lookup"><span data-stu-id="81450-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
