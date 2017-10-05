---
title: "Azure RemoteApp에서 Azure Active Directory 테넌트 변경 | Microsoft Docs"
description: "Azure RemoteApp과 연결된 Azure Active Directory 테넌트를 변경하는 방법에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 7c6c4ded8a11d8399968b2c32aff055d7f3ae5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-azure-active-directory-tenant-in-azure-remoteapp"></a>Azure RemoteApp에서 Azure Active Directory 테넌트 변경
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.
> 
> 

Azure RemoteApp은 Azure AD(Azure Active Directory)를 사용하여 사용자 액세스를 허용합니다. Azure RemoteApp에서 사용할 수 있는 유일한 Azure AD 테넌트는 Azure 구독과 연결된 것입니다. 포털의 **설정** 페이지에서 연결된 구독을 볼 수 있습니다. **구독** 탭에서 **디렉터리** 열을 확인합니다.

> [!NOTE]
> 성공적으로 변경하려면 먼저 모든 Azure RemoteApp 컬렉션에서 기존 Azure Active Directory 테넌트의 사용자를 모두 제거합니다. 이렇게 하려면 Azure 포털로 이동한 다음 **Azure RemoteApp** 탭으로 이동하여 모든 Azure RemoteApp 컬렉션을 엽니다. **사용자** 탭으로 이동하여 현재 Azure Active Directory 테넌트에 속하는 사용자를 제거합니다. 모든 기존 Azure RemoteApp 컬렉션에 대해 이 작업을 반복합니다. 이 작업을 수행하지 않으면 컬렉션을 만들거나 패치할 수 없습니다.
> 
> 

다른 테넌트를 사용하려는 경우 다음 단계를 사용하여 구독과의 연결을 변경합니다.

1. 포털에서 Azure RemoteApp 컬렉션에 대한 액세스 권한을 부여한 Azure AD 사용자를 제거합니다. 이 작업 방법에 대한 단계는 위의 참고를 참조하세요.
2. 서비스 관리자로 Microsoft 계정(이전의 Live ID)를 설정합니다. 본인이 서비스 관리자라는 사실을 모르는 경우 **설정 -> 관리자**를 클릭하여 확인합니다. 이제 다음과 같이 변경합니다.
   
   1. 오른쪽 위 모서리에서 사용자를 클릭한 다음 **내 청구서 보기**를 클릭합니다.
   2. 구독을 클릭합니다. 그런 다음 새 페이지에서 아래로 스크롤하여 오른쪽의 **구독 세부 정보 편집** 을 클릭합니다. 오른쪽 아래 가운데 쯤에 있을 것입니다.
   3. 서비스 관리자가 될 사용자에 Microsoft 계정을 입력합니다.
3. 이제 포털에서 로그아웃하고 이전 단계에서 지정한 Microsoft 계정으로 다시 로그인합니다.
4. **새로 만들기 -> App Services -> Active Directory -> 디렉터리 -> 사용자 지정 만들기**를 클릭합니다.
5. **디렉터리**에서 **기존 디렉터리 사용**을 선택합니다. 이제 포털에서 로그아웃할 것이므로 **로그아웃할 준비가 되었습니다.**를 선택합니다.
6. 추가할 디렉터리의 전역 관리자로 다시 포털에 로그인합니다. 아직 전역 관리자가 아니라면 로그인한 다음 다시 로그아웃합니다.
7. 로그인할 때 구독에서 기존 AD 테넌트를 사용할지 묻는 메시지가 표시될 것입니다. **계속**을 클릭한 다음 **지금 로그아웃**을 클릭합니다.
8. 다시 로그인하여 **설정 -> 구독**으로 다시 이동합니다. 구독을 선택한 다음 **디렉터리 편집**을 클릭합니다. 사용하려는 Azure AD 테넌트를 선택합니다.

이제 새 Azure AD 테넌트를 사용하여 Azure 구독에 대한 액세스를 제어하고 Azure RemoteApp에서 사용자 액세스를 구성할 수 있습니다.

