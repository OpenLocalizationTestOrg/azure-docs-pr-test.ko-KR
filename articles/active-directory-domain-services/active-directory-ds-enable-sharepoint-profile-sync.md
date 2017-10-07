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
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a>SharePoint 서버에 대 한 관리 되는 도메인 toosupport 프로필 동기화 구성
SharePoint Server에는 사용자 프로필 동기화에 사용되는 User Profile Service가 포함되어 있습니다. 사용자 프로필 서비스 hello tooset, 적절 한 사용 권한을 toobe Active Directory 도메인에 부여할 필요 합니다. 자세한 내용은 [SharePoint Server 2013에서 프로필 동기화를 위해 Active Directory Domain Services 사용 권한 부여](https://technet.microsoft.com/library/hh296982.aspx)를 참조하세요.

이 문서에서는 Azure AD 도메인 서비스 관리 되는 도메인 toodeploy hello SharePoint 서버 사용자 프로필 동기화 서비스를 구성 하는 방법에 대해 설명 합니다.

## <a name="hello-aad-dc-service-accounts-group"></a>hello ' AAD DC Service Accounts' 그룹
라는 보안 그룹이 '**AAD DC 서비스 계정을**' hello '사용자' 관리 되는 도메인에 조직 구성 단위 내에서 사용할 수 있습니다. Hello에이 그룹을 확인할 수 **Active Directory 사용자 및 컴퓨터** MMC 스냅인에서 관리 되는 도메인입니다.

![AAD DC 서비스 계정 보안 그룹](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

이 보안 그룹의 구성원은 다음 권한을 위임 된 hello:
- hello 루트 DSE의 hello에 대 한 hello' 디렉터리 변경 내용 복제 ' 권한이 도메인을 관리합니다.
- hello 구성 명명 컨텍스트 hello에 대 한 ' 디렉터리 변경 내용 복제 ' 권한이 (cn = configuration 컨테이너) hello의 도메인을 관리 합니다.

이 보안 그룹 hello 기본 제공 그룹의 멤버 이기도 **Pre-Windows 2000 Compatible Access**합니다.

![AAD DC 서비스 계정 보안 그룹](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a>사용자 관리 되는 도메인 toosupport SharePoint 서버 사용자 프로필 동기화를 사용 하도록 설정
SharePoint 사용자 프로필 동기화 toohello에 사용 되는 hello 서비스 계정을 추가할 수 있습니다 **AAD DC 서비스 계정을** 그룹입니다. 결과적으로, hello 동기화 계정 적절 한 권한을 tooreplicate 변경 toohello 디렉터리를 가져옵니다. 이 구성 단계는 SharePoint 서버 사용자 프로필 동기화 toowork를 올바르게 있습니다.

![AAD DC 서비스 계정 - 구성원 추가](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC 서비스 계정 - 구성원 추가](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a>관련 콘텐츠
* [기술 참조 - SharePoint Server 2013에서 프로필 동기화를 위해 Active Directory Domain Services 사용 권한 부여](https://technet.microsoft.com/library/hh296982.aspx)
