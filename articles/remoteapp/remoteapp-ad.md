---
title: "AD aaaAzure + Azure RemoteApp에 대 한 Active Directory 요구 사항 | Microsoft Docs"
description: "자세한 방법을 tooset Azure RemoteApp과 함께 toowork Active Directory를 구성 합니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Azure AD + Azure RemoteApp에 대한 Active Directory 요구 사항
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp 하이브리드 컬렉션 또는 toofederate AD Connect를 사용 하 여 원하는 클라우드 컬렉션 toodo hello 다음을 해야 합니다.

### <a name="connect-azure-ad-and-active-directory"></a>Azure AD 및 Active Directory 연결
Azure AD 테 넌 트를 온-프레미스 Active Directory 환경 tooconnect를 하려는 경우 AD Connect를 사용 합니다. 이동할 수만 [4 번의 클릭](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello 두 디렉터리입니다.

참고 - 하이브리드 컬렉션에는 디렉터리 동기화가 필요합니다.

### <a name="make-sure-your-domaincom-match"></a>“@domain.com”이 일치하는지 확인
시작 하기 전에 해야 Azure AD 도메인에 온-프레미스 포리스트 일치 hello 접미사에 대 한 해당 hello UPN 합니다. 

Azure RemoteApp에 로그인 하는 모든 사용자로 로그인은 Azure AD에서 hello UPN 도메인 접미사를 설정한 후 "@ 사용자<hello suffix you set up>." 사용자가 로그인 수 있는지도 hello를 사용 하 여 동일한 있는지 확인 user@suffix hello 온-프레미스 도메인에 있습니다. 일부 경우에 설정할 수 있습니다 한 도메인 이름-에 hello 사용자에 대 한 다른 도메인 접미사를 지정 하는 동안 Azure AD에서 이 경우 사용자가 수 tooconnect tooany 도메인에 가입 된 컴퓨터 또는 Azure RemoteApp을 통해 리소스 수 없습니다.

예를 들어 contoso.com으로 AAD에서 사용자 UPN 도메인 접미사를 설정 했지만 프레미스/AD에서 일부 사용자가 사용 하 여 구성 된 toolog @contoso.uk, 해당 사용자는 hello ARA 컬렉션에 로그인 할 수 toocorrectly 경우가 없습니다. AAD와 AD에서 UPN 해야 하는 사용자가 로그인 toobe 가능한 hello에 대 한 동일 hello "

### <a name="create-objects-for-azure-remoteapp"></a>Azure RemoteApp에 대한 개체 만들기
다음 온-프레미스 Active Directory 개체 toocreate hello를 해야 합니다.

* 서비스 계정 tooprovide toodomain 리소스에 액세스 RDSH 끝점 toohello 온-프레미스 도메인에 가입 하 여 RemoteApp 프로그램에 대 한 합니다.
* 조직 구성 단위 (OU) toocontain RemoteApp 컴퓨터 개체입니다. 권장 (않음 필요 하지 않음) tooisolate hello 계정과 RemoteApp에 사용할 정책을 하는 OU hello 사용 됩니다.

RemoteApp 컬렉션을 만들 때 필요한 두이 개체 모두 수 있으므로 있는지 toodo 이러한 단계 먼저 합니다.

