---
title: "aaaSecuring 액세스 tooAzure RemoteApp, 이후 | Microsoft Docs"
description: "Azure Active Directory의 조건부 액세스를 사용 하 여 보안 액세스 tooAzure RemoteApp에 알아봅니다"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: a19b0b09-ab26-4beb-80bb-33a46da39887
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 98dfe69e2f5fa5014b6eb3157e01f131c287134d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-remoteapp-and-beyond"></a>보안 액세스 tooAzure RemoteApp를 이상
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

이 문서에서 관리자로 hello 최종 사용자는 Azure RemoteApp을 통해에서 시작 및 끝 SQL 데이터베이스 또는 다른 응용 프로그램 백 엔드 같은 보안 리소스에 대 한 보안 액세스 채널을 설정 하는 방법의 개요를 제공 합니다. hello 목적은 모임 hello 원하는 조건을 원격 응용 프로그램에 액세스할 수 있으며 안전한 백 엔드 hello 하는 권한 있는 사용자만 수만 액세스할 수 있는지 제어 하는 hello Azure RemoteApp 환경에서와 다른 위치에서가 아니라 toomake입니다.

Admin 님 안녕하세요 toolook에 필요한 주요 영역 3 가지가 있습니다.

![Azure RemoteApp에 대한 조건부 액세스 고려 사항](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

정보 및 대답 toothese 질문에 대 한 계속 읽어 보십시오.

## <a name="who-can-access-hello-collection"></a>Hello 컬렉션에 액세스할 수 있는 사용자?
관리자에 게 hello 컬렉션에 있는 원격 응용 프로그램에 액세스할 수 있는 hello 사용자를 선택 합니다. Azure AD(Azure Active Directory) 회사 또는 학교 계정(이전 명칭, “조직 계정”) 또는 Microsoft 계정을 사용할 수 있습니다.(예: @outlook.com) Azure AD 계정을;을 사용 하 여 대부분의 엔터프라이즈 시나리오 나중에 설명 하는 조건부 액세스 기능을 사용할 수 있게 하며 도메인에 가입 된 컬렉션에 대 한 hello만 선택할 수도 있습니다. hello 문서의 hello 나머지 부분에서는 Azure AD 계정을 사용 하는 Azure RemoteApp과 함께 가정 합니다.

**수행한 내용:**

Azure AD 계정 toocontrol 액세스 tooAzure RemoteApp 목록에 두 가지 작업을 사용 하 여:

1. 게시 하 고 이러한 응용 프로그램 백 엔드를 액세스 하는 응용 프로그램에 연결 하는 hello 액세스할 수 있는 사용자 항상 알고 있습니다.
2. म 하므로 만들 수 있습니다 하 고 등 multi-factor authentication이 사용자 계정 삭제, 설정 된 암호 정책에 사용 하 여 Azure AD 기본 hello를 제어 합니다. 

## <a name="how-is-hello-collection-accessed-from-where"></a>Hello 컬렉션을 액세스 하는 방법을 어디서 액세스하나요?
일반적으로 관리자는 공용 인터넷 환경에서 Azure RemoteApp 같은 액세스 하기 위한 toodefine 정책 사용 하려고 합니다. 예를 들어 hello 회사 네트워크 외부에서 hello 환경에 액세스 하는 사용자가 multi-factor authentication (MFA) toogain 액세스 toouse; tooensure 원하는 또는 아마도 차단 해야 완전히 합니다.

Azure RemoteApp 관리자는 Azure RemoteApp 환경에 대 한 Azure AD Premium tooset 조건부 액세스 정책을 통해 사용할 수 있는 hello 기능을 사용할 수 있습니다. 다양 한 보고 및 경고 기능 toomonitor hello 환경 액세스 하는 방법을 사용할 수 있습니다.

### <a name="how-tooset-up-conditional-access-for-azure-remoteapp"></a>어떻게 tooset Azure RemoteApp에 대 한 조건부 액세스를
우리는 예제 시나리오를 통해 진행 중인 toowalk – hello 회사 네트워크 외부 사용자가 hello Azure RemoteApp 관리자가 tooblock 액세스 toohello 환경입니다.

> [!NOTE]
> Azure AD Premium 계층 toohello를 업그레이드 하 고 Azure RemoteApp 컬렉션을 하나 이상 만들었다고 가정 합니다.
> 
> 

1. Azure 포털에서 클릭 hello **Active Directory** 탭 합니다. Tooconfigure hello 디렉터리를 클릭 합니다.
   
   기억: 조건부 액세스 이므로 속성의 디렉터리 및 Azure RemoteApp의 모든 구성은 hello 디렉터리 수준에서 수행 됩니다. 즉, 이러한 변경 내용은 toobe hello 디렉터리 관리자 toomake 필요 합니다.
2. 클릭 **응용 프로그램**, 클릭 하 고 **Microsoft Azure RemoteApp** tooset 조건부 액세스를 합니다. 디렉터리에 별도로 "software as a service" 응용 프로그램 각각에 대한 조건부 액세스를 설정할 수 있습니다.
   ![Azure RemoteApp에 대한 조건부 액세스 설정](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)
3. Hello에 **구성** 탭, 설정 **액세스 규칙을 사용 하도록 설정** tooON 합니다.
   ![Azure RemoteApp에 대한 액세스 규칙 사용](./media/remoteapp-secureaccess/ra-enableaccessrules.png)
4. 이제 다양 한 규칙을 구성할 수 있으며 tooapply가 선택 되도록 합니다.
   
   1. 선택 **아닐 때 액세스 작업을 차단** toocompletely는 사용자가 지정한 hello 네트워크 환경 외부에서 Azure RemoteApp에 액세스 하지 못하도록 방지 합니다.
   2. Hello 옵션 toodefine hello IP 주소 범위 "신뢰할 수 있는 네트워크입니다."를 구성 하는 아래를 클릭 합니다. 외부의 모든 항목은 거부됩니다.
5. Hello Azure RemoteApp 클라이언트 지정한 hello 범위를 벗어나는 IP 주소에서 시작 하 여 구성을 테스트 합니다. Azure AD 자격 증명으로 로그인한 후에 다음과 같은 메시지가 표시되어야 합니다.

![거부 된 액세스 tooAzure RemoteApp](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a>미래 조건부 액세스 기능
조건부 액세스의 새로운 기능 hello Azure Active Directory 팀은 작업입니다. 관리자 수 toocreate 새로운 유형의 네트워크 위치를 기반으로 규칙 이외의 규칙 것입니다. 새로운 기능 hello 공개 미리 보기는 곧 제공 될 예정입니다.

### <a name="how-toomonitor-access-tooazure-remoteapp"></a>Toomonitor tooAzure RemoteApp을 액세스 하는 방법
조건부 액세스와 함께 훌륭한 기능 toouse hello Azure Active Directory Premium에 대 한 보고 기능입니다. 사용자 환경에 액세스 하는 보고서 toomonitor 사용할 수 있으며 의심 스러운 활동을 검색할 수 있습니다.

Azure RemoteApp 몇 번 했다는 것을 액세스 hello 사용자의 hello 이름을 볼 수는 예를 들어 및 시기.

1. Azure 포털에서 **Active Directory**를 클릭한 다음 디렉터리를 클릭합니다.
2. Toohello 이동 **보고서** 탭 합니다.
3. 보고서의 hello 목록에서 선택 **응용 프로그램 사용 현황** 아래 **응용 프로그램 통합**합니다.
   
   Azure RemoteApp에 대한 몇 가지 집계된 통계를 볼 수 있습니다. 
   ![집계된 Azure RemoteApp 액세스 통계](./media/remoteapp-secureaccess/ra-accessstats.png)
4. Azure RemoteApp을 액세스 하는 사용자에 대 한 hello 응용 프로그램 tooreveal 정보를 클릭 합니다.
   ![Azure RemoteApp에 대한 사용자 액세스 통계](./media/remoteapp-secureaccess/ra-userstats.png)

### <a name="summary"></a>요약
Azure Active Directory premium에 대 한 액세스 규칙 tooAzure RemoteApp (및 Azure AD를 통해 사용할 수 있는 서비스 응용 프로그램으로 다른 소프트웨어)를 설정할 수 있습니다. 규칙은 현재 제한 toonetwork 위치 기반 정책 하지만 향후 hello에 확장 될 것 엔터프라이즈 관리의 tooother 측면.

Azure AD Premium 보고도 제공 하 고 모니터링 제어 hello admin 님 안녕하세요 추가로 확장 하는 기능에는 Azure RemoteApp 환경 동안 키를 누릅니다.

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a>내 보안 리소스가 내 Azure RemoteApp 환경에서만 액세스할 수 있는지 확인하려면 어떻게 해야 하나요?
이 문서의 이전 섹션에서 액세스 toohello Azure RemoteApp 환경 보안에 집중 합니다. म 얻을 하는 hello 서비스 사용 방법을 액세스 규칙 toofurther 제어를 설정 하 고 액세스할 수 있는 hello 사용자를 선택 하 여 합니다.

Azure RemoteApp 배포에 대 한 일반적인 시나리오는 hello 원격 응용 프로그램 백 엔드 리소스, 예: SQL 데이터베이스와 toocommunicate에 필요 합니다. 이 리소스를 호스팅할 온-프레미스 (예: 회사 네트워크)에서 또는 (예: Azure IaaS)에서 hello 클라우드에 있습니다. 관리자는 toomake hello 백 엔드 리소스 수만 액세스할 수 있는지 및 예를 들어 하지 공용 인터넷을 통해 액세스 하 고 사용자의 PC에서 직접 실행 하려면 응용 프로그램을 Azure RemoteApp을 통해 배포 된 응용 프로그램에서 원하는 경우가 종종 있습니다. Azure RemoteApp hello 중앙에서 관리 하 고 보안 된 환경 및 사용자와 상호 작용 해야 하는 hello 유일한 경로 hello 백 엔드 리소스를 종종 발견 됩니다.

hello 솔루션은 Azure RemoteApp 환경 모두 hello tooplace 및 hello 보안 리소스에 hello 동일한 Azure 가상 네트워크 (VNET). Hello 리소스를 다른 사이트에 있으면, 예: toocreate VNet 확장 hello Azure 데이터 센터 및 hello 고객 온-프레미스 환경의 사이트 간 VPN 연결을 설정할 수 있습니다.

Azure RemoteApp에서는 고유의 VNET을 제공할 수 있는 두 가지 형식의 컬렉션 배포를 지원합니다.

* 이외의 도메인에 가입: hello 응용 프로그램 "시야" hello의 다른 리소스에에서 갖습니다 hello VNET 합니다. 예를 들어 SQL 인증을 사용 하는 사용 되는 tooconnect 응용 프로그램 tooa SQL 데이터베이스가 될 수 있습니다이 (응용 프로그램 hello 데이터베이스에 대해 직접 hello 사용자를 인증 하는 데 사용)
* Azure RemoteApp에서 사용 하는 hello 가상 컴퓨터에 hello VNET에에서 조인 된 tooa 도메인 컨트롤러는 도메인에 가입 된:. Hello 응용 프로그램 tooauthenticate 순서 tooget 액세스 tooa 백 엔드 리소스에 Windows 도메인 컨트롤러에 대해 필요한 경우에 유용 합니다.
  ![Azure RemoteApp의 도메인 가입 컬렉션](./media/remoteapp-secureaccess/ra-domainjoined.png)

### <a name="how-toocreate-a-secure-connection-between-azure-and-my-on-premises-environment"></a>어떻게 toocreate Azure와 내 온-프레미스 환경 사이의 보안 연결
Azure와 온-프레미스 환경을 연결하기 위한 몇 가지 구성 옵션이 있습니다. Hello 옵션의 개요는 있습니다.

Azure RemoteApp과 함께 tooconfigure VNet을 먼저, 필요한 고 컬렉션의 hello 생성 프로세스 동안 사용 합니다. 

## <a name="hello-complete-solution"></a>hello 완벽 한 솔루션
아래 hello 다이어그램이 작성 하는 보안 액세스 채널을 통해 Azure RemoteApp (ARA), hello 최종 사용자 로부터 hello 백 엔드 리소스로 hello 완벽 한 솔루션을 보여 줍니다.
![Azure RemoteApp을 secure](./media/remoteapp-secureaccess/ra-secureoverview.png) 에서 단계 1 hello 사용자를 선택 하 고 ARA 액세스할 수 있는 방법을 제어 하는 액세스 규칙을 생성 합니다. 아래 hello 예제에서 우리만 액세스를 허용 hello 회사 네트워크에서 작업 하는 사용자에 대 한 합니다. 호환 되지 않는 사용자는 수 tooaccess hello ARA 환경을 전혀 수 없습니다.
2 단계에서에서 것을 제어 하는 hello VNet/VPN 구성 통해서만 hello 백 엔드 리소스를 노출 합니다. Azure RemoteApp에에서 놓았습니다 hello 동일한 VNet입니다. hello 최종 결과 hello 리소스 hello ARA 환경을 통해만 액세스할 수 있습니다.

