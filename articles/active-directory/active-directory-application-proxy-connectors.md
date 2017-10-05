---
title: "클래식 포털 Azure AD 앱 프록시 커넥터 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시에서 커넥터 그룹을 만들고 관리하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: fc65c4053c45d9c16c62ee0fe65924133a4bb94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>커넥터 그룹을 사용하여 별도의 네트워크 및 위치에서 응용 프로그램 게시
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-application-proxy-connectors-azure-portal.md)
> * [Azure 클래식 포털](active-directory-application-proxy-connectors.md)
>
>

커넥터 그룹은 다음을 비롯한 다양한 시나리오에 유용합니다.

* 여러 데이터 센터가 연결되어 있는 사이트. 이 경우 데이터 센터 간 링크가 비용이 높고 느리기 때문에 가능한 한 데이터 센터 내에서 많은 트래픽을 유지하려고 합니다. 각 데이터 센터에서 커넥터를 배포하여 데이터 센터 내에 있는 응용 프로그램만 제공할 수 있습니다. 이 방법은 데이터 센터 간 링크를 최소화하고 사용자에게 완전히 투명한 경험을 제공합니다.
* 기본 회사 네트워크에 속하지 않은 격리된 네트워크에 설치된 응용 프로그램을 관리하는 경우. 커넥터 그룹을 사용하여 격리된 네트워크의 전용 커넥터를 설치하고 해당 네트워크에 응용 프로그램도 격리할 수 있습니다.
* 클라우드 액세스를 위해 IaaS에 설치된 응용 프로그램의 경우 커넥터 그룹은 모든 앱에 대한 액세스를 보호하는 일반적인 서비스를 제공합니다. 커넥터 그룹은 회사 네트워크에 추가 종속성을 만들거나 앱 경험을 조각화하지 않습니다. 커넥터는 각 클라우드 데이터 센터에 설치될 수 있으며 이 네트워크에 있는 응용 프로그램만 처리할 수 있습니다. 고가용성을 얻기 위해 커넥터를 여러 개 설치할 수 있습니다.
* 특정 커넥터가 포리스트별로 배포되고 특정 응용 프로그램을 처리하도록 설정될 수 있는 다중 포리스트 환경에 대한 지원.
* 커넥터 그룹은 재해 복구 사이트에서 장애 조치(failover)를 감지하는 데 사용하거나 기본 사이트의 백업으로 사용할 수 있습니다.
* 커넥터 그룹은 단일 테넌트에서 여러 회사를 처리하는 데도 사용할 수 있습니다.

## <a name="prerequisite-create-your-connectors"></a>필수 조건: 커넥터 만들기
커넥터를 그룹화하려면 [여러 커넥터를 설치](active-directory-application-proxy-enable.md)한 후 이름을 지정하고 그룹화합니다. 마지막으로 특정 앱에 커넥터를 할당해야 합니다.

## <a name="step-1-create-connector-groups"></a>1단계: 커넥터 그룹 만들기
원하는 수 만큼 커넥터 그룹을 만들 수 있습니다. 커넥터 그룹은 Azure 클래식 포털에서 만들 수 있습니다.

1. 디렉터리를 선택하고 **구성**을 클릭합니다.  
    ![응용 프로그램 프록시 구성 스크린샷 - 커넥터 그룹 관리 클릭](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. 응용 프로그램 프록시에서 **커넥터 그룹 관리**를 클릭하고 그룹에 이름을 지정하여 커넥터 그룹을 만듭니다.  
    ![응용 프로그램 프록시 커넥터 그룹 스크린샷 - 새 그룹 이름 지정](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-to-your-groups"></a>2단계: 그룹에 커넥터 할당
커넥터 그룹이 만들어지면 해당 그룹에 커넥터를 이동합니다.

1. **응용 프로그램 프록시**에서 **커넥터 관리**를 클릭합니다.
2. **그룹**에서 각 커넥터에 대해 원하는 그룹을 선택합니다. 커넥터가 새 그룹에서 활성화되는 데 최대 10분까지 걸릴 수 있습니다.  
    ![응용 프로그램 프록시 커넥터 스크린샷 - 드롭다운 메뉴에서 그룹 선택](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-to-your-connector-groups"></a>3단계: 커넥터 그룹에 응용 프로그램 할당
마지막 단계는 각 응용 프로그램을 해당 응용 프로그램을 처리할 커넥터 그룹에 할당하는 것입니다.

1. Azure 클래식 포털의 해당 디렉터리에서 그룹에 할당할 응용 프로그램을 선택하고 **구성**을 클릭합니다.
2. **커넥터 그룹**에서 응용 프로그램에서 사용할 그룹을 선택합니다. 이 변경은 즉시 적용됩니다.  
    ![응용 프로그램 프록시 커넥터 그룹 스크린샷 - 드롭다운 메뉴에서 그룹 선택](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>참고 항목
* [응용 프로그램 프록시 사용](active-directory-application-proxy-enable.md)
* [Single Sign-On 사용](active-directory-application-proxy-sso-using-kcd.md)
* [조건부 액세스 사용](active-directory-application-proxy-conditional-access.md)
* [응용 프로그램 프록시에서 발생한 문제 해결](active-directory-application-proxy-troubleshoot.md)

최신 뉴스 및 업데이트는 [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)
