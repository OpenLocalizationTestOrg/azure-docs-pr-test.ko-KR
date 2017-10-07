---
title: "사용자 tooyour Azure RemoteApp 컬렉션 aaaAdd | Microsoft Docs"
description: "자세한 내용은 방법 tooadd 사용자 tooyour Azure RemoteApp 컬렉션"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a>어떻게 tooadd 사용자 tooyour Azure RemoteApp 컬렉션
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

사용자가 참조 하 고 Azure RemoteApp에 앱을 사용할 수, toogrant tooyour 컬렉션 액세스 해야 합니다. 이것은 쉽게 일부 hello: hello에 **사용자 액세스** 탭, hello 사용자에 대 한 hello 계정 정보를 입력 한 후 hello 확인 표시를 클릭 합니다.

어떤 계정 정보가 필요할까요? 사용자가 만든 (클라우드 또는 하이브리드) 여부를 사용 하 고 Office 365 ProPlus 해당 컬렉션에 컬렉션의 hello 형식에 따라 다릅니다.

## <a name="supported-user-identities"></a>지원되는 사용자 ID
hello 다른 컬렉션 형식 (및 하이브리드 클라우드) 다른 사용자 id를 사용 하 여 액세스 tooapplications에 대 한 지원.  

RemoteApp의 하이브리드 컬렉션에 대 한 사용자 tooset 온-프레미스 및 Directory 통합과 함께 Azure Active Directory 테 넌 트에 Active Directory 도메인 인프라를 필요 (및 필요에 따라 단일 로그온). 또한 toocreate hello 온-프레미스 디렉터리에 몇 가지 Active Directory 개체가 필요 합니다.  

RemoteApp의 클라우드 컬렉션에 대 한 Azure Active Directory id 지원 권한이 있는 사용자 Microsoft 계정 사용자 액세스 tooRemoteApp tooinclude를 부여할 수 있습니다.  아래 hello 표를 참조 합니다.

Office 365 사용자는 Azure Active Directory 사용자입니다. Azure Active Directory 하이브리드, 디렉터리 동기화된 계정이 있는 경우, RemoteApp 하이브리드 배포에서 사용자 액세스 권한이 부여될 수 있습니다.   

이 테이블은 identity 컬렉션과 hello Active Directory 요구 사항 이란에서 지원 되는 빠른 참조로 사용할 수 있습니다.

| 사용자 계정 | 클라우드 | 하이브리드 |
| --- | --- | --- |
| Microsoft 계정 |예 |아니요 |
| Azure AD(Azure Active Directory) | | |
| Azure AD 클라우드만 해당 |예 |아니요 |
| 암호 동기화를 사용하는 ADsync |예 |예 |
| 암호 동기화를 사용하지 않는 ADsync |예 |아니요 |
| AD FS 포함 ADsync |예 |yes |
| [타사 Azure 지원 ID 공급자](https://msdn.microsoft.com/library/azure/jj679342.aspx)(예: Ping) |yes |예 |
| Multi-Factor Authentication |예 |예 |

RemoteApp에 대한 Active Directory 구성에 대한 [자세한 내용](remoteapp-ad.md) 을 확인하세요.

> [!NOTE]
> hello Azure Active Directory 사용자 구독와 관련 된 hello 테 넌 트에서 이어야 합니다. (보고 하 고 hello에 가입 내용을 수정 **설정을** hello 포털에서 탭 합니다. 참조 [변경 hello Azure Active Directory 테 넌 트가 RemoteApp에서 사용 하는](remoteapp-changetenant.md) 자세한 정보에 대 한 합니다.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Office 365 ProPlus 사용자 계정 정보
템플릿 이미지를 Office 365 ProPlus hello을 사용 하는 컬렉션의 경우 *또는* hello에 대 한 Office 365 구독이 있는 tooadd Azure Active Directory 사용자를 Office 365를 사용 하는 사용자 지정 이미지를 만든 경우만 허용 됩니다 기본 도메인 가입 합니다. 자세한 내용은 [Azure RemoteApp과 함께 Office 365 사용](remoteapp-o365.md) 을 참조하세요.

