---
title: "Azure Active Directory Domain Services: 가상 네트워크 만들기 또는 선택 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스 hello Azure 클래식 포털을 사용 하 여 사용 하도록 설정"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a>Azure Active Directory Domain Services의 가상 네트워크 만들기 또는 선택
## <a name="before-you-begin"></a>시작하기 전에
너무 참조[Azure Active Directory 도메인 서비스에 대 한 네트워킹 고려 사항](active-directory-ds-networking.md)합니다.

## <a name="task-2-create-an-azure-virtual-network"></a>작업 2: Azure 가상 네트워크 만들기
다음 구성 작업 hello는 Azure 가상 네트워크 및 그 안에 서브넷이 toocreate 합니다. 가상 네트워크 내의 이 서브넷에서 Azure Active Directory Domain Services를 사용하도록 설정합니다. 기존 가상 네트워크는 편이 더 toouse를 설정한 경우이 단계를 건너뛸 수 있습니다.

> [!NOTE]
> Azure 가상 네트워크를 만들거나 Azure Active Directory 도메인 서비스와 toouse 속한 tooan Azure Active Directory 도메인 서비스에서 지원 되는 Azure 지역 선택 해당 hello 있는지 확인 하십시오. tooascertain Azure Active Directory 도메인 서비스를 사용할 수 있는 Azure 지역 hello를 참조 하십시오. [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/)합니다.
>
>후속 구성 단계에서 Azure Active Directory 도메인 서비스를 사용 하도록 설정 하면 hello 오른쪽 가상 네트워크를 선택 하면 hello 가상 네트워크 tooensure의 참고 hello 이름입니다.


toocreate tooenable Azure Active Directory 도메인 서비스를 원하는 Azure 가상 네트워크는 이러한 구성 지침을 따릅니다.

1. Toohello 이동 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 왼쪽된 창에서 선택 **네트워크**합니다.

    ![Networks 노드](./media/active-directory-domain-services-getting-started/networks-node.png)  
    hello **가상 네트워크** 창이 열립니다.
3. Hello hello hello 창 맨 아래에 작업 창에서 클릭 **새로**합니다.

    ![Virtual Networks 창](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. **Network Services**를 클릭한 다음 **Virtual Network**를 선택합니다.

    ![가상 네트워크 - 빠른 생성](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. 가상 네트워크 toocreate 클릭 **빠른 생성**합니다.

6. 지정는 **이름** 가상에 대 한 네트워크, 및 hello 다음을 수행 하는 것이 좋습니다.
    * Tooconfigure를 선택할 수 있습니다 **주소 공간** 또는 **최대 VM 수** 이 네트워크에 대 한 합니다.
    * Hello에 두면 **DNS 서버** 로 설정 **없음** 지금은 합니다. Azure Active Directory 도메인 서비스를 사용 하도록 설정한 후 hello 설정을 업데이트할 수 있습니다.
7. Hello에 **위치** 드롭 다운 목록에서 지원 되는 Azure 지역을 선택 합니다.  
    tooascertain Azure Active Directory 도메인 서비스를 사용할 수 있는 Azure 지역 hello를 참조 하십시오. [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/)합니다.
8. toocreate 가상 네트워크가 클릭 **가상 네트워크 만들기**합니다.

    ![Azure Active Directory Domain Services의 가상 네트워크 만들기](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. 가상 네트워크를 만든 후 hello 가상 네트워크의 hello 이름을 선택 하 고 클릭 hello **구성** 탭 합니다.

    ![서브넷 만들기](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. **가상 네트워크 주소 공간**, 클릭 **서브넷을 추가**, 다음 hello 이름의 서브넷을 지정 하 고 **AaddsSubnet**합니다.

    ![Azure Active Directory Domain Services의 서브넷 만들기](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. toocreate 서브넷 hello, 클릭 **저장**합니다.


## <a name="next-step"></a>다음 단계
[작업 3: Azure Active Directory Domain Services 활성화](active-directory-ds-getting-started-enableaadds.md)
