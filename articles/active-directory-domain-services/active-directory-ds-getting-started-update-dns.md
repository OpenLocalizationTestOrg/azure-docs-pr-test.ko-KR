---
title: "Azure Active Directory 도메인 서비스: 업데이트 hello Azure 가상 네트워크에 대 한 DNS 설정을 | Microsoft Docs"
description: "Azure Active Directory Domain Services 시작"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a>Hello Azure 가상 네트워크에 대 한 DNS 설정을 업데이트 합니다.
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>작업 4: 업데이트 hello Azure 가상 네트워크에 대 한 DNS 설정
Hello 구성 작업 앞에에서 성공적으로 사용 하도록 설정한 디렉터리에 대 한 Azure Active Directory 도메인 서비스. hello 다음 작업은 tooensure hello 가상 네트워크 내에서 컴퓨터 연결 하 고 이러한 서비스를 사용할 수 있습니다. 이 문서에서는 사용자 가상 네트워크 toopoint toohello 두 IP 주소에 대해 Azure Active Directory 도메인 서비스를 hello 가상 네트워크에서 사용할 수 있는 hello DNS 서버 설정을 업데이트 합니다.

> [!NOTE]
> Hello 디렉터리에 대 한 Azure Active Directory 도메인 서비스를 활성화 한 후 Azure Active Directory 도메인 서비스용 hello에 표시 되는 hello IP 주소를 기록해 둡니다 **구성** 디렉터리의 탭 합니다.
>
>

tooupdate hello DNS 서버 설정을 hello 가상 네트워크를 사용 하도록 설정한 Azure Active Directory 도메인 서비스, 단계를 수행 하는 전체 hello:

1. Toohello 이동 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 왼쪽된 창에서 선택 **네트워크**합니다.  
    hello **네트워크** 창이 열립니다.

    ![가상 네트워크 창](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. Hello에 **가상 네트워크** 탭, 선택 hello 가상 네트워크를 사용 하도록 설정한 Azure Active Directory 도메인 서비스 tooview 속성입니다.
4. Hello 클릭 **구성** 탭 합니다.

    ![가상 네트워크 창](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. Hello에 **DNS 서버** 섹션을 hello에 표시 된 hello IP 주소 둘 다 입력 **도메인 서비스** hello 섹션 **구성** 디렉터리의 탭 합니다.
6. hello hello 창 맨 아래에 hello 작업창에서이 가상 네트워크에 대 한 toosave hello DNS 서버 설정을 클릭 **저장**합니다.

   ![Hello hello 가상 네트워크 DNS 서버 설정을 업데이트합니다](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  Hello 네트워크의 가상 컴퓨터만 다시 시작한 후에 새로운 DNS 설정을 hello를 가져옵니다. 필요할 경우 tooget 업데이트 hello DNS 설정을 바로, hello 포털, PowerShell 또는 CLI hello에 의해 다시 시작을 트리거하십시오.
>
>

## <a name="next-steps"></a>다음 단계
태스크 5: [암호 동기화 tooAzure Active Directory 도메인 서비스를 사용 하도록 설정](active-directory-ds-getting-started-password-sync.md)
