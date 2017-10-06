---
title: "hello Azure 클래식 포털에서에서 aaaKnown 네트워크 | Microsoft Docs"
description: "알려진된 네트워크를 구성 하 여 여러 지역에서의 로그인 및 의심 스러운 활동 보고서와 함께 IP 주소에서의 로그인 hello에 포함 된 조직에서 소유 하는 IP 주소를 방지할 수 있습니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a>알려진 네트워크

> [!div class="op_single_selector"]
> * [Azure 클래식 포털](active-directory-known-networks.md)
> * [Azure 포털](active-directory-known-networks-azure-portal.md)
> 
> 


Azure Active Directory의 액세스 및 조직 디렉터리의 hello 무결성 및 보안에 대 한 사용 현황 보고서 toogain 가시성을 사용할 수 있습니다. 이 정보를 사용 하면 디렉터리 관리자 수 보다 잘 결정 있는 가능한 보안 위험이 발생할 수 있습니다 적절 하 게 될 수 toomitigate 이러한 위험.

Hello 시킨 "*여러 지역에서의 로그인*"및"*의심 스러운 활동을 포함 IP 주소에서 로그인*" 보고서가 실제로 소유 하는 IP 주소가 올바르게 플래그 프로그램 조직입니다. 

예를 들어 다음과 같은 경우에 이러한 문제가 발생할 수 있습니다. 

* 보스턴 사무실의 사용자가 샌프란시스코 트리거 hello "로그인 여러 지역에서" 보고서에서에서 원격으로 tooyour 데이터 센터에 로그인 
* 조직의 사용자가 toosign에서 여러 번 잘못 된 암호로 트리거 hello "로그인 의심 스러운 활동 IP 주소에서" 보고서 

tooprevent 생성 잘못 된 보안을 통해 이러한 경우를 보고, 알려진된 IP 주소 범위 toohello 목록이 조직의 공용 IP 주소를 추가 해야 합니다.    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a>조직의 공용 IP 주소 범위를 tooadd hello 다음 단계를 수행 하십시오.

1. 로그온 toohello [Azure 관리 포털](https://manage.windowsazure.com)합니다.

2. Hello 왼쪽된 창에서 클릭 **Active Directory**합니다. 

    ![알려진 네트워크](./media/active-directory-known-networks/known-netwoks-01.png)

3. Hello에 **디렉터리** 탭에서 디렉터리를 선택 합니다.

4. Hello 메뉴에서 hello 위에 표시를 클릭 **구성**합니다. 

    ![알려진 네트워크](./media/active-directory-known-networks/known-netwoks-02.png)

5. Hello 구성 탭에서 이동 너무**조직의 공용 IP 주소 범위** 

    ![알려진 네트워크](./media/active-directory-known-networks/known-netwoks-03.png)

6. **알려진 IP 주소 범위 추가**를 클릭합니다.

7. 주소 범위, 표시 되는 hello 대화 상자에서 추가 하 고 완료 되 면 hello 확인 단추를 클릭 합니다. 

    ![알려진 네트워크](./media/active-directory-known-networks/known-netwoks-04.png)

**추가 리소스:**

* [액세스 및 사용 보고서 보기](active-directory-view-access-usage-reports.md)
* [의심스러운 활동을 포함하는 IP 주소의 로그인](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [여러 지역에서의 로그인](active-directory-reporting-sign-ins-from-multiple-geographies.md)

