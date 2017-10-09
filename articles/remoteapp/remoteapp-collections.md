---
title: "컬렉션 do aaaWhat 유형의 Azure RemoteApp에 대 한 필요 한가요? | Microsoft Docs"
description: "Hello 유형의 Azure RemoteApp과 함께 사용할 수 있는 컬렉션에 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f00b5fe41af597cf75e26300bf7842c3a8ff94fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>Azure RemoteApp에 필요한 컬렉션의 종류는 무엇입니까?
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp를 사용하면 어떠한 장치의 사용자와도 앱 및 리소스를 공유할 수 있습니다. 컬렉션 toohold hello 앱 및 리소스를 만들어서 수행 하 고 사용자와 해당 컬렉션을 공유 합니다. 서로 다른 네트워크 및 인증 옵션을 사용하는 두 가지 컬렉션 옵션이 있습니다. 어느 옵션이 사용자에게 적합합니까?

Hello 다른 고려 사항 및 Azure RemoteApp 컬렉션에서 가장 toomake tooget hello를 필요로 하는 선택 사항 과정을 살펴보겠습니다. 

## <a name="quick-differences-between-hello-collection-types"></a>빠른 차이점 hello 컬렉션 형식
|  | 클라우드 | 하이브리드 |
| --- | --- | --- |
| 기존 VNET 사용 |예 |예 |
| AD에 연결된 계정(DirSync)이 필요합니다. |아니요 |예 |
| 도메인 가입이 필요합니다. |아니요 |예 |
| 도메인 컨트롤러의 액세스 가능한 tooVNET 필요 |아니요 |예 |

## <a name="cloud-collections"></a>클라우드 컬렉션
* 빠른 toocreate-hello 컬렉션 신속 하 게 프로 비전 되 면 앱 빠른 toousers 가져오기 의미 합니다.
* 자신의 앱을 가져오거나 우리의 앱을 공유합니다. (Azure VM에서 작성 됨) 사용자 지정 이미지 또는 구독에 포함 된 hello 이미지 중 하나를 사용할 수 있습니다.
* 컬렉션 및 온-프레미스 도메인 간의 tooconfigure 연결 하지 않아도 됩니다.
* 하지만 필요에 따라 사용자 고유의 Azure VNET tooprovide 액세스를 온-프레미스 환경에 SQL Server (데이터베이스 인증을 사용 하 여)와 같은 리소스에 데이터를 공유 하거나 toouse 비-Windows 인증에 사용할 수 있습니다.

그렇다면 어떻게 만드나요?

* 클라우드 전용입니까? Hello와 함께 만들기 **빠른 생성** hello 포털에서 옵션입니다.
* 클라우드 + VNET입니까? Hello를 사용 하 여 만들 **VNET와 함께 만들기** 옵션은 있 toojoin 도메인을 선택 하지 마십시오.

## <a name="hybrid-collections"></a>하이브리드 컬렉션
* 전체 액세스 tooon 온-프레미스 네트워크 + Azure VNET을 제공 합니다.
* 앱 및 데이터에 대한 도메인 조인 액세스를 포함합니다. 원격 응용 프로그램은 사용자의 온-프레미스 Active Directory에 대해 인증한 다음 사용자 도메인의 리소스에 액세스할 수 있습니다.
* 기존 시스템 센터 솔루션 및 Windows 그룹 정책을 사용하여 고급 모니터링 및 관리를 사용하도록 설정합니다(Windows Server 2012 R2에서 만든 사용자 지정 이미지를 통해).
* 지원 [ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect Azure VNET tooyour 지역 VNET입니다.

Hello를 사용 하 여 만들 **VNET와 함께 만들기** 옵션 및 toojoin 도메인 선택 합니다.

## <a name="authentication-options"></a>인증 옵션
Azure RemoteApp은 Microsoft 계정과 Azure Active Directory 계정을 모두 지원하지만 일부 컬렉션은 일부 방법을 지원하지 않을 수 있습니다. 

| 계정 유형 |  | 클라우드 | 클라우드 + VNET | 하이브리드 |
| --- | --- | --- | --- | --- |
| Microsoft 계정 | |예 |예 |아니요 |
| Azure AD(Azure Active Directory) | | | | |
| Azure AD만 |예 |예 |아니요 | |
| 암호 동기화를 사용하는 AD Connect |예 |예 |예 | |
| 암호 동기화를 사용하지 않는 AD Connect |예 |예 |아니요 | |
| AD FS를 사용하는 AD Connect |예 |예 |예 | |
| 타사 Azure 지원 ID 공급자(예: Ping) |예 |예 |예 | |
| Multi-Factor Authentication | |예 |예 |예 |

### <a name="cloud-and-cloud--vnet"></a>클라우드 및 클라우드 + VNET
클라우드 컬렉션을 사용한 Microsoft 계정, Azure AD 계정 또는 두 hello 혼합 하 여 사용할 수 있습니다. 사용자에 게 가장 적합 한 hello 계정을 사용 합니다.

Microsoft 계정을 사용하기 위한 특정 요구 사항이 없습니다. 

Azure AD 계정을 toouse 하려는 경우 toomake Azure AD 테 넌 트 구독에 연결 된 하나 hello과 일치 해야 합니다. Azure RemoteApp 구독을 만들 때 hello Azure AD 테 넌 트를 사용 하는 구독에 자동으로 연결 되었습니다. 모든 Azure AD 사용자 부여 권한을 tooneeds toobe 해당 동일한 테 넌 트 됩니다. 필요한 경우 다음을 할 수 있습니다 [hello Azure AD 테 넌 트 변경](remoteapp-changetenant.md) 구독과 연관 됩니다.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>하이브리드(또는 클라우드 + Azure AD + AD)
Azure AD + 온-프레미스 Active Directory 사용은 하이브리드 컬렉션에 대한 전제 조건입니다. Toouse AD Connect toointegrate hello 두 디렉터리 필요합니다. 하지만 toohow AD Connect를 구성할 때 몇 가지 선택 필요 있습니다. 

암호 동기화 사용 또는 AD 페더레이션 사용 등 두 가지 AD Connect 시나리오가 있습니다. 체크 아웃 hello [AD Connect 정보](../active-directory/active-directory-aadconnect.md) toofigure 아웃 다음 중 가장 적합 한 합니다.

또한 Azure AD + AD를 클라우드 컬렉션과 함께 사용할 수 있습니다. Hello 같은 설정 단계를 따르고 있는지 확인 합니다.

체크 아웃 [Azure AD + Azure RemoteApp에 대 한 Active Directory 요구 사항](remoteapp-ad.md) hello 단계 필요한 tooconfigure Azure AD 및 Active Directory에 대 한 합니다.

## <a name="go-create-your-collection"></a>사용자의 컬렉션을 만드십시오!
물론 म 계산 했습니다 것, 한 가지 왼쪽된 toodo 이므로-첫 번째 Azure RemoteApp 컬렉션 만들기 것 같습니다.

[클라우드 컬렉션 만들기](remoteapp-create-cloud-deployment.md) 또는 [하이브리드 컬렉션을 만들기](remoteapp-create-hybrid-deployment.md) - 그냥 만들어만 보세요!

