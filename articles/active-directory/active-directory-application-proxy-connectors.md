---
title: "Azure AD 응용 프로그램 프록시 커넥터를 포털 aaaClassic | Microsoft Docs"
description: "에서는 어떻게 toocreate에서 Azure AD 응용 프로그램 프록시 커넥터 그룹 및 관리 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>커넥터 그룹을 사용하여 별도의 네트워크 및 위치에서 응용 프로그램 게시
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-application-proxy-connectors-azure-portal.md)
> * [Azure 클래식 포털](active-directory-application-proxy-connectors.md)
>
>

커넥터 그룹은 다음을 비롯한 다양한 시나리오에 유용합니다.

* 여러 데이터 센터가 연결되어 있는 사이트. 이 경우 원하는 tookeep hello 데이터 센터 내에서 많은 트래픽을 최대한 데이터 센터 간 링크는 비용이 많이 들고 느린 때문에 있습니다. 각 데이터 센터 tooserve hello 응용 프로그램만 hello 데이터 센터 내에 있는 커넥터를 배포할 수 있습니다. 이 방법은 데이터 센터 간 링크를 최소화 하 고 tooyour 사용자 완전히 투명 한 경험을 제공 합니다.
* Hello 주요 회사 네트워크의 일부가 아닌 있는 격리 된 네트워크에 설치 된 응용 프로그램을 관리 합니다. 격리 된 네트워크 tooalso 응용 프로그램 격리 toohello 네트워크에 커넥터 그룹 전용 tooinstall 커넥터를 사용할 수 있습니다.
* 클라우드 액세스를 위해 IaaS에 설치 된 응용 프로그램에 대 한 커넥터 그룹을 공통 서비스 toosecure hello 액세스 tooall hello 앱을 제공 합니다. 커넥터 그룹 추가 종속성이 회사 네트워크에 생성 하거나 hello 앱 환경을 조각 하지 마십시오. 커넥터는 각 클라우드 데이터 센터에 설치될 수 있으며 이 네트워크에 있는 응용 프로그램만 처리할 수 있습니다. 여러 커넥터 tooachieve 고가용성을 설치할 수 있습니다.
* 특정 커넥터 포리스트당 배포 하 고 tooserve 특정 응용 프로그램 설정 될 수 있는 다중 포리스트 환경에 대 한 지원.
* 커넥터 그룹 tooeither 장애 조치를 감지 하거나에 대 한 백업으로 주 hello 재해 복구 사이트에서 사용할 수 있습니다 사이트입니다.
* 커넥터 그룹 수도 tooserve 사용 되는 단일 테 넌 트의 여러 회사 수 있습니다.

## <a name="prerequisite-create-your-connectors"></a>필수 조건: 커넥터 만들기
toogroup 커넥터, [여러 명의 커넥터가 설치](active-directory-application-proxy-enable.md), 한 다음 이름을 지정 하 고 그룹화 합니다. Tooassign가 마지막으로 해당 toospecific 앱.

## <a name="step-1-create-connector-groups"></a>1단계: 커넥터 그룹 만들기
원하는 수 만큼 커넥터 그룹을 만들 수 있습니다. 커넥터 그룹을 만들 hello Azure 클래식 포털에서에서 수행 됩니다.

1. 디렉터리를 선택하고 **구성**을 클릭합니다.  
    ![응용 프로그램 프록시 구성 스크린샷 - 커넥터 그룹 관리 클릭](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. 응용 프로그램 프록시를 아래에서 클릭 **커넥터 그룹 관리** 고 hello 그룹 이름을 제공 하 여 커넥터 그룹을 만들어야 합니다.  
    ![응용 프로그램 프록시 커넥터 그룹 스크린샷 - 새 그룹 이름 지정](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-tooyour-groups"></a>2 단계: tooyour 그룹 커넥터 할당
Hello 커넥터 그룹을 만든 후 hello 커넥터 toohello 적절 한 그룹을 이동 합니다.

1. **응용 프로그램 프록시**에서 **커넥터 관리**를 클릭합니다.
2. 아래 **그룹**선택, 각 커넥터에 대해 원하는 hello 그룹입니다. Hello 새 그룹에 활성 too10 분 toobecome hello 커넥터가 걸릴 수도 있습니다.  
    ![응용 프로그램 프록시 커넥터 스크린샷 - 드롭다운 메뉴에서 그룹 선택](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-tooyour-connector-groups"></a>3 단계: tooyour 커넥터 그룹 응용 프로그램 할당
hello 마지막 단계는 tooset 서비스를 제공 하는 각 응용 프로그램 toohello 커넥터 그룹입니다.

1. Hello 디렉터리에 Azure 클래식 포털에서에서 선택 hello tooassign toohello 그룹을 클릭 하 여 응용 프로그램 **구성**합니다.
2. 아래 **커넥터 그룹**선택, 응용 프로그램 toouse hello 원하는 hello 그룹입니다. 이 변경은 즉시 적용됩니다.  
    ![응용 프로그램 프록시 커넥터 그룹 스크린샷 - 드롭다운 메뉴에서 그룹 선택](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>참고 항목
* [응용 프로그램 프록시 사용](active-directory-application-proxy-enable.md)
* [Single Sign-On 사용](active-directory-application-proxy-sso-using-kcd.md)
* [조건부 액세스 사용](active-directory-application-proxy-conditional-access.md)
* [응용 프로그램 프록시에서 발생한 문제 해결](active-directory-application-proxy-troubleshoot.md)

Hello 최신 뉴스 및 업데이트에 대 한 체크 아웃 hello [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)
