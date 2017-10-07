---
title: "Azure Active Directory Domain Services: Azure Active Directory Domain Services 활성화 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스 hello Azure 클래식 포털을 사용 하 여 사용 하도록 설정"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Azure Active Directory 도메인 서비스 hello Azure 클래식 포털을 사용 하 여 사용 하도록 설정

## <a name="task-3-enable-azure-active-directory-domain-services"></a>작업 3: Azure Active Directory Domain Services 활성화
이 태스크에서는 단계를 수행 하는 hello를 수행 하 여 디렉터리에 대 한 Azure Active Directory 도메인 서비스 (Azure AD DS)를 사용 합니다.

1. Toohello 이동 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 왼쪽된 창에서 선택 hello **Active Directory** 단추입니다.
3. Hello Azure Active Directory (Azure AD) 테 넌 트 (디렉터리) Azure AD DS tooenable 원하는 선택 합니다.

    ![Azure AD 디렉터리 선택](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Hello에 **미리 보기 디렉터리** 페이지에서 hello **구성** 탭 합니다.

    ![디렉터리의 탭 구성](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. 아래 **도메인 서비스**, hello 변경 **이 디렉터리에 대 한 도메인 서비스 사용** 옵션**예**합니다.  
    추가 Azure Active Directory 도메인 서비스 구성 옵션 hello 페이지에 나타납니다.

    ![Domain Services 사용](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > 테 넌 트에 대 한 Azure Active Directory 도메인 서비스를 사용 하도록 설정 하면 Azure AD를 생성 하 고 사용자를 인증에 필요한 hello Kerberos 및 NTLM 자격 증명 해시를 저장 합니다.
   >
   >
6. Hello 지정 **도메인 서비스의 DNS 도메인 이름을**합니다.

   * hello 디렉터리의 기본 도메인 이름을 hello (으로 **. onmicrosoft.com** 접미사) 기본적으로 선택 됩니다.

   * hello 목록에 포함 되어 Azure AD 디렉터리에 대해 구성 된 모든 도메인을 둘 다를 포함 하 여 확인 및 hello에서 구성 하는 도메인을 확인 되지 않은 **도메인** 탭 합니다.

   * 사용자 지정 도메인 이름도 입력할 수 있습니다. 이 예제에서는 hello 사용자 지정 도메인 이름이 *contoso100.com*합니다.

     > [!WARNING]
     > 지정 된 도메인 이름 hello 접두사 (예를 들어 *contoso100* hello에 *contoso100.com* 도메인 이름) 15 자 이하의 포함 해야 합니다. 15자를 초과하는 접두사가 포함된 Azure Active Directory Domain Services 도메인은 만들 수 없습니다.
     >
     >
7. 선택한 관리 되는 hello에 대 한 도메인 hello 가상 네트워크에 이미 존재 하지 않는 hello DNS 도메인 이름을 확인 합니다. 특히, toosee 여부 확인:

   * Hello 사용 하 여 도메인을 이미 있으면 hello 가상 네트워크에 동일한 DNS 도메인 이름이 있습니다.

   * hello 선택한 가상 네트워크에 온-프레미스 네트워크에 VPN 연결이 있게 되며 hello 사용 하 여 도메인 온-프레미스 네트워크에 동일한 DNS 도메인 이름이 있습니다.

   * Hello 가상 네트워크에 해당 이름 가진 기존 클라우드 서비스를가지고 있습니다.
8. 사용할 수 있는 Azure Active Directory 도메인 서비스 toobe 원하는 가상 네트워크를 선택 합니다. Hello 가상 네트워크와 전용된 서브넷 hello에서 만든 선택 **연결 도메인 toothis 가상 네트워크 서비스** 드롭 다운 목록입니다. 또한 hello 다음을 고려 합니다.

   * 사용자가 지정한 해당 hello 가상 네트워크 속해 tooan Azure Active Directory 도메인 서비스에서 지원 되는 Azure 지역을 확인 합니다. tooascertain Azure Active Directory 도메인 서비스를 사용할 수 있는 Azure 지역 hello를 참조 하십시오. [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/)합니다.

   * Azure Active Directory 도메인 서비스에 지원 되지 않습니다 tooa 영역에 속하는 가상 네트워크 hello 드롭 다운 목록에 표시 되지 않습니다.

   * Azure Active Directory 도메인 서비스에 대 한 hello 가상 네트워크 내에서 전용된 서브넷을 사용 합니다. 수행 *하지* 선택 hello 게이트웨이 서브넷입니다. [네트워킹 고려 사항](active-directory-ds-networking.md)을 참조합니다.

   * 마찬가지로, 가상 네트워크를 Azure 리소스 관리자를 사용 하 여 만든 hello 드롭 다운 목록에 표시 되지 않습니다. Resource Manager 기반 가상 네트워크가 현재 Azure Active Directory Domain Services에서 지원되지 않기 때문입니다.
9. hello 작업창 hello hello 페이지 맨 아래에 Azure Active Directory 도메인 서비스 tooenable 클릭 **저장**합니다.
    * Azure Active Directory 도메인 서비스에 대 한 디렉터리를 활성화 하는 동안 hello 페이지의 상태를 표시 하는 *보류 중인*합니다.

        ![Domain Services 사용 창](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > Azure Active Directory Domain Services는 관리되는 도메인에 고가용성을 제공합니다. Azure Active Directory 도메인 서비스를 활성화 한 후 서비스는 hello 가상 네트워크에서 사용할 수 있는 도메인에서 hello IP 주소는 한 번만 표시 합니다. hello 두 번째 IP 주소가 표시 됩니다 hello 직후 먼저 곧 hello 서비스를 사용 하면 도메인에 대 한 고가용성 있습니다. 고가용성 구성 된 도메인에 대 한 활성, 표시 되어야 hello에 두 개의 IP 주소 시점과 **도메인 서비스** hello 섹션 **구성** 탭 합니다.
        >
        >
    * 서비스는 hello에 가상 네트워크에서 사용할 수 있는 도메인에서 hello 첫 번째 IP 주소가 약 20 too30 분 후 **IP 주소** 필드 hello에 **구성** 페이지.

        ![첫 번째 프로비전된 IP를 보여 주는 Domain Services 창](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * 고가용성은 도메인에 대 한 운영, 두 개의 IP 주소 hello 페이지에 표시 됩니다. 관리되는 도메인은 이 두 IP 주소에서 선택한 가상 네트워크에서 사용할 수 있습니다.

10. 가상 네트워크에 대 한 hello DNS 설정을 업데이트할 수 있도록 두 개의 IP 주소 hello note 합니다. 이렇게 하면 특정 도메인 가입 등의 작업에 대 한 hello tooconnect toohello 도메인을 가상 네트워크에 가상 컴퓨터.

    ![프로비전된 IP를 보여 주는 Domain Services 창](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> 에 Azure AD 테 넌 트 (예를 들어 hello 수 사용자 또는 그룹)의 hello 크기에 따라 tooyour 관리 되는 컨텍스트의 동기화 도메인 약간의 시간이 됩니다. 이 동기화 프로세스 hello 백그라운드에서 발생합니다. 큰 테 넌 트에는 수십 개의 개체에 대 한 하루 또는 모든 사용자, 그룹 멤버 자격 및 자격 증명 toobe 동기화에 대 한 두 개의 걸릴 수 있습니다.
>
>

## <a name="next-step"></a>다음 단계
[작업 4: hello Azure 가상 네트워크에 대 한 hello DNS 설정을 업데이트합니다](active-directory-ds-getting-started-update-dns.md)
