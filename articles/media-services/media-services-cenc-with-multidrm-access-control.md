---
title: "다중 DRM 및 Access Control이 포함된 CENC: Azure 및 Azure Media Services에서 참조 설계 및 구현 | Microsoft 문서"
description: "Toolicensing Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 hello 하는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 7814739b-cea9-4b9b-8370-538702e5c615
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;kilroyh;yanmf;juliako
ms.openlocfilehash: 033fb618650c4fbe9069d467159a8734da759bba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cenc-with-multi-drm-and-access-control-a-reference-design-and-implementation-on-azure-and-azure-media-services"></a>다중 DRM 및 액세스 제어가 포함된 CENC: Azure 및 Azure 미디어 서비스에서 참조 디자인 및 구현
 
## <a name="introduction"></a>소개
잘 알려진은 복잡 한 작업 toodesign DRM 하위 시스템은 OTT에 대 한 빌드를 또는 스트리밍 솔루션 온라인있지 않습니다. 한 비디오 공급자 toooutsource 연산자/온라인에 대 한 연습 공통이 부분 toospecialized DRM 서비스 공급자입니다. hello이 문서의 목적은 toopresent 참조 디자인 및 OTT 또는 온라인 스트리밍 솔루션에서 종단 간 DRM 하위 시스템의 구현입니다.

이 문서의 대상으로 하는 hello 판독기는 엔지니어 OTT 또는 온라인 스트리밍/다중-screen 솔루션 또는 DRM 하위 시스템에 관심이 있는 모든 독자의 DRM 하위 시스템에서 작업 합니다. 판독기는 PlayReady, Widevine, FairPlay 또는 Adobe Access 같은 hello 시장 hello DRM 기술 중 하나 이상에 대해 잘 알고 이라고 하는 hello 가정 합니다.

DRM에는 포함 다중 DRM의 CENC(일반적인 암호화)도 포함됩니다. 온라인 스트리밍 및 OTT 업계 주요 추세 단일 DRM 및 클라이언트 SDK 사용 하 여 다양 한 클라이언트 플랫폼에 대 한 이전 추세 hello에서 다중-native-DRM으로 다양 한 클라이언트 플랫폼에 CENC toouse 됩니다. PlayReady와 Widevine hello 당 암호화 된 CENC native-DRM을 사용할 경우 [일반 암호화 (ISO/IEC 23001-7 CENC)](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=65271/) 사양입니다.

다중 DRM으로 CENC의 hello 혜택은 다음과 같습니다.

1. 기본 DRM을 포함하는 다양한 플랫폼을 대상으로 단일 암호화 처리가 사용되므로 암호화 비용이 절감됩니다.
2. 암호화 된 자산의 단일 복사본만; 필요 않으므로 암호화 된 자산을 관리 하는의 hello 비용이 감소
3. DRM 클라이언트 hello 네이티브 DRM 클라이언트는 해당 네이티브 플랫폼에 일반적으로 무료 이므로 비용을 라이선스를 제거 합니다.

Microsoft는 몇몇 주요 기업들과 더불어 DASH 및 CENC의 적극적인 프로모터로 활동해왔습니다. Microsoft Azure 미디어 서비스에서 DASH 및CENC 지원을 제공하고 있습니다. Mingfei의 블로그의 [Azure Media Services에서 Google Widevine 라이선스 전달 서비스 발표](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/) 및 [다중 DRM 스트림을 배달하기 위해 Azure Media Services에서 Google Widevine 패키징 추가](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)에서 최근 소식을 참조하세요.  

### <a name="overview-of-this-article"></a>이 문서의 개요
이 문서의 목표 hello hello 다음이 포함 됩니다.

1. 다중 DRM의 CENC를 사용하는 DRM 하위 시스템에 대한 참조 디자인을 제공합니다.
2. Microsoft Azure/Azure 미디어 서비스 플랫폼에 대한 참조 구현을 제공합니다.
3. 몇 가지 디자인 및 구현 토픽에 대해 설명합니다.

Hello 문서 "다중 DRM" hello 다음을 다룹니다.

1. Microsoft PlayReady
2. Google Widevine
3. Apple FairPlay 

hello 다음 표에 요약 되어 hello 네이티브 플랫폼/네이티브 앱 및 각 DRM에서 지 원하는 브라우저.

| **클라이언트 플랫폼** | **네이티브 DRM 지원** | **브라우저/앱** | **스트리밍 형식** |
| --- | --- | --- | --- |
| **스마트 TV, 연산자 STB, OTT STB** |주로 PlayReady 및/또는 Widevine 및/또는 기타 |Linux, Opera, WebKit, 기타 |다양한 형식 |
| **Windows 10 장치(Windows PC, Windows 태블릿, Windows Phone, Xbox)** |PlayReady |MS Edge/IE11/EME<br/><br/><br/>UWP |DASH(HLS의 경우 PlayReady는 지원되지 않음)<br/><br/>DASH, 부드러운 스트리밍(HLS의 경우 PlayReady는 지원되지 않음) |
| **Android 장치(전화, 태블릿, TV)** |Widevine |크롬/EME |DASH,HLS |
| **iOS(iPhone, iPad), OS X 클라이언트 및 Apple TV** |FairPlay |Safari 8+/EME |HLS |


Hello 각 DRM에 대 한 배포의 현재 상태를 고려 하면 서비스는 보통 합니다 2 또는 3 tooimplement DRMs toomake 있는지 모든 hello 유형의 최상의 hello에서 끝점 주소 방법입니다.

Hello 서비스 논리의 hello 복잡도 간에 균형을 조절이 고 hello 클라이언트 쪽 tooreach 사용자의 특정 수준에 hello 복잡성에 hello 다양 한 클라이언트입니다.

toomake 선택 영역에 이러한 사항을 염두에 두어야 합니다.

* PlayReady는 모든 Windows 장치와 일부 Android 장치에서 고유하게 구현되며 거의 모든 플랫폼에서 소프트웨어 SDK를 통해 사용할 수 있습니다.
* Widevine은 모든 Android 장치, Chrome 및 일부 다른 장치에서 고유하게 구현됩니다.
* FairPlay는 iOS 및 Mac OS 클라이언트 또는 iTunes를 통해 사용할 수 있습니다.

따라서 일반적인 다중 DRM은 다음과 같습니다.

* 옵션 1: PlayReady 및 Widevine
* 옵션 2: PlayReady, Widevine 및 FairPlay

## <a name="a-reference-design"></a>참조 디자인
이 섹션에서는 사용 되는 알 수 없는 tootechnologies tooimplement 인 참조 디자인 제공할 것 것입니다.

DRM 하위 시스템 hello 다음과 같은 구성 요소가 포함 될 수 있습니다.

1. 키 관리
2. DRM 패키징
3. DRM 라이선스 배달
4. 자격 확인
5. 인증/권한 부여
6. 플레이어
7. 원본/CDN

hello 다음 다이어그램에서는 hello 높은 수준 간의 상호 작용 DRM 하위 시스템의 hello 구성 요소

![CENC를 사용하는 DRM 하위 시스템](./media/media-services-cenc-with-multidrm-access-control/media-services-generic-drm-subsystem-with-cenc.png)

세 개의 기본 "계층" hello 디자인 되어 있습니다.

1. 외부적으로 노출되지 않는 백오피스 계층(검은색)
2. 공용; 향하는 모든 hello 끝점이 포함 된 "DMZ" 레이어 (파랑)
3. 공용 인터넷을 통과하는 트래픽과 CDN 및 플레이어를 포함하는 공용 인터넷 계층(옅은 파란색)

정적 또는 동적 암호화에 관계 없이 DRM 보호를 제어하기 위한 콘텐츠 관리 도구가 있어야 합니다. DRM 암호화에 대 한 hello 입력이 포함 되어야 합니다.

1. MBR 비디오 콘텐츠
2. 콘텐츠 키
3. 라이선스 획득 URL

재생 시간 동안 hello 높은 수준 흐름은입니다.

1. 사용자가 인증됩니다.
2. 권한 부여 토큰 hello 사용자;에 대해 만들어집니다.
3. DRM으로 보호 된 콘텐츠 (매니페스트)은 다운로드 한 tooplayer;
4. 플레이어 라이선스 취득 요청 toolicense 서버 키 ID 및 권한 부여와 함께 전송 토큰입니다.

이동 toohello 다음 항목인 하기 전에 몇 가지 단어 hello에 대 한 키 관리의 디자인합니다.

| **콘텐츠 키 대 자산(ContentKey–to-Asset)** | **시나리오** |
| --- | --- |
| 일대일(1–to-1) |hello 가장 간단 하 게 합니다. Hello 제어력을 제공합니다. 하지만 일반적으로 이렇게 hello 가장 높은 라이선스 배달 비용. 보호된 각 자산에 대해 최소 하나의 라이선스 요청이 필요합니다. |
| 일대다(1–to-Many) |Hello 콘텐츠 같은 여러 자산에 대 한 키를 사용할 수 있습니다. 예를 들어 장르 (또는 동영상 유전자)의 하위 집합 또는 장르와 같은 논리 그룹에 모든 hello 자산에 대 한 단일 콘텐츠 키를 사용할 수 있습니다. |
| 다대일(Many–to-1) |각 자산에 대해 여러 콘텐츠 키가 필요합니다. <br/><br/>예를 들어, MPEG DASH 및 HLS에 대 한 동적 aes-128 암호화를 위한 다중 DRM으로 tooapply 동적 CENC 보호 해야 할 경우 두 개의 별도 콘텐츠 키를 각각 고유한 ContentKeyType 필요 합니다. (동적 CENC 보호에 사용 되는 콘텐츠 키 hello에 대 한 ContentKeyType.CommonEncryption, 반면에 사용할 hello 콘텐츠 ContentKeyType.EnvelopeEncryption 동적 aes-128 암호화에 사용 되는 키를 사용 해야 합니다.)<br/><br/>이론적으로 CENC 보호 대시의 또 다른 예로, 콘텐츠, 콘텐츠 키 하나 사용 하는 tooprotect 비디오 스트림 및 다른 콘텐츠 키 tooprotect 오디오 스트림을 하십시오. |
| 많은 – 너무 다 |위의 두 가지 시나리오는 hello 조합의: 키의 각에 사용 되는 콘텐츠의 집합 hello 여러 자산 hello에 동일한 자산 "group"입니다. |

또 다른 중요 한 요인이 tooconsider 영구 및 비영구 라이선스 hello 사용입니다.

이러한 고려 사항이 중요한 이유는 무엇인가요?

라이선스 배달에 대 한 공용 클라우드를 사용 하는 경우 비용 직접적인 영향을 줍니다 toolicense 배달을 갖게 됩니다. 다음 두 가지 디자인의 경우 tooillustrate hello를 살펴보겠습니다.

1. 월간 구독: 영구 라이선스와 일대다(1–to-Many) 콘텐츠 키 대 자산 매핑을 사용합니다. 예: 모든 hello 어린이 동영상에 대 한 단일 콘텐츠 키 암호화에 사용 합니다. 이 경우 다음과 같습니다.

    모든 어린이용 영화에 요청된 전체 라이선스 수/장치 = 1
2. 월간 구독: 비영구 라이선스와 콘텐츠 키 및 자산 간에 일대일(1–to-1) 매핑을 사용합니다. 이 경우 다음과 같습니다.

    모든 어린이용 영화에 요청된 전체 라이선스 수/장치 = [본 영화 수] x [세션 수]

쉽게 볼 수 있듯이 두 개의 서로 다른 디자인에 매우 다른 라이선스 발생 하는 hello 요청 패턴 이므로 Azure 미디어 서비스 등 공용 클라우드 라이선스 배달 서비스를 제공 하면 비용 라이선스 배달

## <a name="mapping-design-tootechnology-for-implementation"></a>구현에 대 한 디자인 tootechnology 매핑
다음으로, 각 문서 블록에 대 한 어떤 기술 toouse를 지정 하 여 Microsoft Azure/Azure 미디어 서비스 플랫폼에서 우리의 일반 디자인 tootechnologies를 매핑합니다.

hello 아래 표에 나와 hello 매핑.

| **구성 요소** | **Technology** |
| --- | --- |
| **플레이어** |[Azure 미디어 플레이어](https://azure.microsoft.com/services/media-services/media-player/) |
| **IDP(ID 공급자)** |Azure Active Directory |
| **STS(보안 토큰 서비스)** |Azure Active Directory |
| **DRM 보호 워크플로** |Azure 미디어 서비스 동적 보호 |
| **DRM 라이선스 배달** |1. Azure Media Services 라이선스 배달(PlayReady, Widevine, FairPlay) 또는 <br/>2. Axinom License Server, <br/>3. 사용자 지정 PlayReady 라이선스 서버 |
| **원본** |Azure 미디어 서비스 스트리밍 끝점 |
| **키 관리** |참조 구현에는 필요하지 않음 |
| **콘텐츠 관리** |C# 콘솔 응용 프로그램 |

즉, IDP(ID 공급자) 및 STS(보안 토큰 서비스) 모두 Azure AD입니다. 플레이어로는 [Azure 미디어 플레이어 API](http://amp.azure.net/libs/amp/latest/docs/)를 사용합니다. Azure 미디어 서비스와 Azure 미디어 플레이어는 모두 다중 DRM의 DASH 및 CENC를 지원합니다.

다음 다이어그램에 표시 하는 hello 기술 매핑 위에 hello로 전체 구조와 흐름 hello 합니다.

![AMS에서 CENC](./media/media-services-cenc-with-multidrm-access-control/media-services-cenc-subsystem-on-AMS-platform.png)

동적 CENC 암호화를 순서 tooset, hello 콘텐츠 관리 도구는 다음 입력 hello를 사용:

1. 개방 콘텐츠
2. 키 생성/관리에서 콘텐츠 키
3. 라이선스 획득 URL
4. Azure AD의 정보 목록

hello 콘텐츠 관리 도구의 hello 출력이 됩니다.

1. JWT 토큰 및 DRM 라이선스 사양; 라이선스 배달 확인 하는 방법에 대 한 hello 사양이 포함 되어 있는 ContentKeyAuthorizationPolicy
2. AssetDeliveryPolicy - 스트리밍 형식, DRM 보호 및 라이선스 획득 URL에 대한 사양 포함

런타임 중으로 hello 흐름은 아래:

1. 사용자 인증 시 JWT 토큰이 생성됩니다.
2. Hello JWT 토큰에 포함 된 hello 클레임 중 하나에 "EntitledUserGroup"의 hello 그룹 개체 ID가 포함 된 "groups" 클레임입니다. 이 클레임은 "자격 확인"을 전달하는 데 사용됩니다.
3. CENC의 플레이어 다운로드 클라이언트 매니페스트 콘텐츠를 보호 되 고 "표시" hello 다음:

   1. 키 ID
   2. hello 콘텐츠를 보호 하는 CENC
   3. 라이선스 획득 URL
4. 플레이어는 hello 브라우저/DRM이 지원에 따라 라이선스 취득 요청을 합니다. Hello 라이선스 취득 요청, 키 ID 및 hello JWT 토큰도 전송 됩니다. 라이선스 배달 서비스는 hello JWT 토큰 및 라이선스 필요 hello를 발급 하기 전에 포함 된 hello 클레임을 확인 합니다.

## <a name="implementation"></a>구현
### <a name="implementation-procedures"></a>구현 절차
hello 구현 단계를 수행 하는 hello를 포함 됩니다.

1. 테스트 자산 준비: 인코딩/패키지는 테스트 비디오 toomulti 비트 전송률 조각난 MP4 Azure 미디어 서비스에서 합니다. 이 자산은 DRM으로 보호되지 않습니다. DRM 보호는 나중에 동적 보호로 수행됩니다.
2. 키 ID 및 콘텐츠 키(필요한 경우 키 시드에서)를 만듭니다. 여기서는 여러 테스트 자산에 대해 단일 집합의 키 ID 및 콘텐츠 키만 다루므로 키 관리 시스템이 필요하지 않습니다.
3. Hello 테스트 자산에 대 한 AMS API tooconfigure 다중 DRM 라이선스 배달 서비스를 사용 합니다. 사용자 지정 라이선스 서버를 회사 나 Azure 미디어 서비스에서 라이선스 서비스 대신 회사의 공급 업체에서 사용 하는 경우이 단계를 건너뛰고 라이선스 배달 구성 하기 위한 hello 단계에서 라이선스 취득 Url을 지정 수 있습니다. AMS API는 몇 가지 세부 필요한 toospecify 권한 부여 정책 제한 등의 구성을 등 다양 한 DRM 라이선스 서비스에 대 한 응답 템플릿을 사용 합니다. 이때 hello Azure 포털이 아직 hello이이 구성에 대 한 UI 필요한 제공 합니다. Julia Kornich의 문서 [PlayReady 및/또는 Widevine 동적 일반 암호화 사용](media-services-protect-with-drm.md)에서 API 수준 정보 및 샘플 코드를 찾을 수 있습니다.
4. AMS API tooconfigure 자산 배달 정책을 사용 하 여 hello 테스트 자산에 대 한 합니다. Julia Kornich의 문서 [PlayReady 및/또는 Widevine 동적 일반 암호화 사용](media-services-protect-with-drm.md)에서 API 수준 정보 및 샘플 코드를 찾을 수 있습니다.
5. Azure에서 Azure Active Directory 테넌트를 만들고 구성합니다.
6. Azure Active Directory 테 넌 트의 몇 가지 사용자 계정 및 그룹 만들기: 이상 만들어야 "EntitledUser" 그룹 및 사용자 toothis 그룹을 추가 합니다. 이 그룹의 사용자 라이선스를 취득에서 권한 검사를 통과 합니다 및이 그룹에 없는 사용자가 toopass 인증 검사에 실패 하 고 됩니다 수 tooacquire 어떠한 사용권도 합니다. 이 "EntitledUser" 그룹의 구성원은 Azure AD에서 발급 된 hello JWT 토큰에 필요한 "groups" 클레임입니다. 이 클레임 요구 사항은 다중 DRM 라이선스 배달 서비스 단계를 구성하는 데 지정해야 합니다.
7. 비디오 플레이어를 호스팅할 ASP.NET MVC 앱을 만듭니다. 이 ASP.NET 응용 프로그램 hello Azure Active Directory 테 넌 트에 대 한 사용자 인증으로 보호 됩니다. 적절 한 클레임은 사용자 인증 후에 얻은 hello 액세스 토큰에 포함 됩니다. 이 단계에는 OpenID Connect API가 권장됩니다. NuGet 패키지를 다음 tooinstall hello가 필요 합니다.
   * Install-Package Microsoft.Azure.ActiveDirectory.GraphClient
   * Install-Package Microsoft.Owin.Security.OpenIdConnect
   * Install-Package Microsoft.Owin.Security.Cookies
   * Install-Package Microsoft.Owin.Host.SystemWeb
   * Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
8. [Azure 미디어 플레이어 API](http://amp.azure.net/libs/amp/latest/docs/)를 사용하여 플레이어를 만듭니다. [Azure 미디어 플레이어의 ProtectionInfo API](http://amp.azure.net/libs/amp/latest/docs/) toospecify 사용 하면 다른 DRM 플랫폼에서 어떤 DRM 기술 toouse 합니다.
9. 테스트 매트릭스:

| **DRM** | **브라우저** | **자격이 있는 사용자에 대한 결과** | **자격이 없는 사용자에 대한 결과** |
| --- | --- | --- | --- |
| **PlayReady** |Windows 10의 MS Edge 또는 IE11 |합격 |불합격 |
| **Widevine** |Windows 10의 Chrome |합격 |불합격 |
| **FairPlay** |TBD | | |

Azure 미디어 서비스 팀의 George Trifonov는 ASP.NET MVC 플레이어 앱에 대한 Azure Active Directory를 설정하는 자세한 단계를 제공하는 블로그, [Azure Active Directory와 Azure 미디어 서비스 OWIN MVC 기반 앱을 Azure Active Directory와 통합 및 JWT 클레임을 기반으로 하는 콘텐츠 키 배달 제한](http://gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)을 작성했습니다.

또한 [Azure 미디어 서비스 및 동적 암호화의 JWT 토큰 인증](http://gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)에 대한 블로그도 작성했습니다. 그리고 그의 [Azure 미디어 서비스 키 배달을 사용한 Azure AD 통합 샘플](https://github.com/AzureMediaServicesSamples/Key-delivery-with-AAD-integration/)을 여기에서 다룹니다.

Azure Active Directory에 대한 자세한 내용은 다음을 참조하세요.

* [Azure Active Directory 개발자 가이드](../active-directory/active-directory-developers-guide.md)에서 개발자 정보를 찾을 수 있습니다.
* [Azure AD 디렉터리 관리](../active-directory/active-directory-administer.md)에서 관리자 정보를 찾을 수 있습니다.

### <a name="some-gotchas-in-implementation"></a>구현에 대해 몇 가지 알려진 문제
Hello 구현에서 썼지만이 있습니다. 다행히 문제가 발생 하는 경우 문제 해결 "문제" 목록은 다음 hello 수 있습니다.

1. **발급자** URL은 **"/"**로 끝나야 합니다.  

    **대상 그룹** hello 플레이어 응용 프로그램 클라이언트 ID와도 추가 해야 해야 **"/"** hello 발급자 URL의 hello 끝에 있습니다.

        <add key="ida:audience" value="[Application Client ID GUID]" />
        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/" />

    [JWT 디코더](http://jwt.calebb.net/), 표시 되어야 **aud** 및 **iss** hello JWT 토큰에서 다음과 같이 합니다.

    ![첫 번째 알려진 문제](./media/media-services-cenc-with-multidrm-access-control/media-services-1st-gotcha.png)
2. AAD에서 (hello 응용 프로그램의 구성 탭)에서 사용 권한을 toohello 응용 프로그램을 추가 합니다. 각 응용 프로그램(로컬 및 배포된 버전)에 필요합니다.

    ![두 번째 알려진 문제](./media/media-services-cenc-with-multidrm-access-control/media-services-perms-to-other-apps.png)
3. 동적 CENC 보호 설정에 hello 오른쪽 발급자를 사용 합니다.

        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/"/>

    hello 다음 작동 하지 않습니다.

        <add key="ida:issuer" value="https://willzhanad.onmicrosoft.com/" />

    hello GUID는 hello AAD 테 넌 트 id입니다. Azure 포털에서 끝점 팝업에서 hello GUID를 찾을 수 있습니다.
4. 그룹 멤버 자격 클레임 권한을 부여합니다. Hello 다음 했으므로, AAD 응용 프로그램 매니페스트 파일에서 올바른지 확인

    "groupMembershipClaims": "All" (hello 기본값은 null)
5. 제한 사항 요구 사항을 만들 때 적절한 TokenType을 설정합니다.

        objTokenRestrictionTemplate.TokenType = TokenType.JWT;

    추가 지원 하기 때문 JWT (AAD)의 또한 tooSWT (ACS) hello TokenType 기본값이 TokenType.JWT입니다. SWT/ACS를 사용 하는 경우에 tooTokenType.SWT를 설정 해야 합니다.

## <a name="additional-topics-for-implementation"></a>구현에 대한 추가 토픽
다음으로 디자인 및 구현에 대한 몇 가지 추가 토픽에 대해서 설명합니다.

### <a name="http-or-https"></a>HTTP 또는 HTTPS
ASP.NET MVC 플레이어 응용 프로그램 구축 hello hello 다음을 지원 해야 합니다.

1. Toobe HTTPS; 아래는 Azure AD 통해 사용자 인증
2. 클라이언트와 toobe HTTPS; 아래는 Azure AD 간의 JWT 토큰 교환
3. 라이선스를 취득 hello 클라이언트 라이선스 배달 Azure 미디어 서비스에서 제공 하는 경우 HTTPS에서 필요한 toobe 하 여 DRM 합니다. 물론 PlayReady 제품군은 라이선스 배달에 대한 HTTPS를 위임하지 않습니다. PlayReady 라이선스 서버가 Azure 미디어 서비스 외부에 있는 경우 HTTP 또는 HTTPS를 사용할 수 있습니다.

따라서 hello ASP.NET 플레이어 응용 프로그램에서 모범 사례로 HTTPS를 사용 합니다. 즉, hello Azure Media Player 페이지 HTTPS 아래의 됩니다. 그러나 스트리밍에 대 한 혼합 콘텐츠 문제 tooconsider 필요 하므로, HTTP 것이 좋습니다.

1. 브라우저에서는 혼합 콘텐츠를 허용하지 않습니다. 하지만 Silverlight과 같은 플러그인, 부드러운 스트리밍을 위한 OSMF 플러그인 및 DASH는 허용합니다. 혼합 된 콘텐츠는 보안 문제-toohello 위협 때문에 이것이 hello 기능 tooinject의을 일으킬 수 있는 악의적인 JS hello 고객 데이터 toobe 위험에 노출 합니다.  브라우저에서는 기본적으로이 차단 되며 지금까지 주위 hello 유일한 방법은 toowork tooallow hello 서버 (원점) 변에 모든 도메인 (관계 없이 https 또는 http). 하지만 좋은 방법은 아닙니다.
2. 둘 다 HTTP를 사용하거나 둘 다 HTTPS를 사용해서 혼합 콘텐츠를 피해야 합니다. 혼합된 콘텐츠를 재생할 때 silverlightSS 기술은 혼합된 콘텐츠 경고를 지워야 합니다. flashSS 기술은 혼합된 콘텐츠 경고 없이 혼합된 콘텐츠를 처리합니다.
3. 스트리밍 끝점이 2014년 8월 전에 만들어진 경우 HTTPS를 지원하지 않습니다. 이 경우 HTTPS에 대한 새 스트리밍 끝점을 만들어 사용하세요.

Hello 참조 구현 DRM으로 보호 된 내용에 대 한 응용 프로그램 및 스트리밍 HTTTPS 아래 됩니다. 열린 내용에 대 한 hello 플레이어 필요는 없습니다 인증 또는 라이선스 수 있도록 hello liberty toouse 하거나 HTTP 또는 HTTPS입니다.

### <a name="azure-active-directory-signing-key-rollover"></a>Azure Active Directory 서명 키 롤오버
구현 고려 사항에는 중요 한 지점을 tootake입니다. 이 구현에서 고려 하지 않는 완료 hello 시스템은 결국 작업 최대 6 주 동안 완전히 중지 합니다.

Azure AD는 업계 표준 tooestablish 신뢰 자체와 Azure AD를 사용 하 여 응용 프로그램 사이 사용 합니다. 특히, Azure AD는 공개 및 개인 키 쌍으로 구성된 서명 키를 사용합니다. Azure AD 사용자 hello에 대 한 정보를 포함 하는 보안 토큰을 만들 때 응용 프로그램 백 toohello 전송 하기 전에 해당 개인 키를 사용 하 여 Azure AD에서이 토큰이 서명 됩니다. 토큰 hello tooverify가 유효 하 고 실제로 Azure AD에서 공개한, hello 응용 프로그램 hello hello 테 넌 트의 페더레이션 메타 데이터 문서에 포함 된 Azure AD에 의해 노출 되는 공개 키를 사용 하 여 hello 토큰 서명의 유효성을 검사 해야 합니다. 이 공개 키 – 및 hello 서명 키 파생 되는 –는 hello Azure AD 테 넌 트의 모든 사용 하는 동일한 것입니다.

Hello 문서에서 키 롤오버를 Azure AD에 대 한 자세한 정보를 확인할 수 있습니다: [Azure AD의 서명 키 롤오버에 대 한 중요 한 정보](../active-directory/active-directory-signing-key-rollover.md)합니다.

Hello 사이 [공개-개인 키 쌍](https://login.microsoftonline.com/common/discovery/keys/),

* hello 개인 키를 사용 하 여 Azure Active Directory toogenerate JWT 토큰입니다.
* hello 공개 키가 AMS tooverify hello JWT 토큰의 DRM 라이선스 배달 서비스와 같은 응용 프로그램에서 사용

보안을 위해 Azure Active Directory는 이 인증서를 주기적(6주마다)으로 바꿉니다. 보안 위반 시 hello 키 롤오버 언제 든 지 발생할 수 있습니다. 따라서 AMS의 hello 라이선스 배달 서비스 hello 키 쌍을 회전 하는 Azure AD 토큰 인증에서 AMS 그렇지 않으면 실패 합니다 하 고 라이선스가 없습니다. 실행 될 때 사용할 tooupdate hello 공개 키가 필요 합니다.

이 작업은 DRM 라이선스 배달 서비스를 구성할 때 TokenRestrictionTemplate.OpenIdConnectDiscoveryDocument를 설정하여 수행합니다.

hello JWT 토큰 흐름은 아래:

1. Azure AD가 인증된 된 사용자;에 대 한 hello 현재 개인 키가 있는 hello JWT 토큰을 발급
2. 플레이어 다중-DRM으로 보호 된 콘텐츠가 있는 CENC을 인식 하는 경우 Azure AD에서 발급 하는 hello JWT 토큰을 찾을 먼저 됩니다.
3. hello 플레이어는 hello JWT 토큰 toolicense 배달 서비스를 사용 하 여 라이선스 취득 요청을 AMS;에 보냅니다.
4. AMS에 hello 라이선스 배달 서비스 라이선스를 발급 하기 전에 Azure AD tooverify hello JWT 토큰에서 hello 현재/올바른 공개 키를 사용 합니다.

Azure AD에서 현재/올바른 공개 키를 hello에 대 한 DRM 라이선스 배달 서비스를 항상 확인 합니다. Azure AD에서 제공 하는 hello 공개 키를 Azure AD에서 발급 한 JWT 토큰을 확인 하는 데 사용 되는 hello 키가 됩니다.

경우에 어떻게 hello 키 롤오버 후 AAD JWT 토큰을 생성 되기 전에 hello JWT 토큰은 플레이어 tooDRM 라이선스 배달 서비스에에서 의해 AMS 확인을 위해 전송 됩니까?

없기 때문에 키를 언제 든 지 롤오버 될 수 있습니다, 항상 올바른 공개 키를 둘 이상의 hello 페더레이션 메타 데이터 문서에서 사용할 수 있습니다. Azure 미디어 서비스 라이선스 배달 키에에서 지정 된 hello 문서 키가 두 개를 곧 롤오버 될 수 있으므로 다른 수를 대체할 유 니 hello를 사용할 수 있습니다.

### <a name="where-is-hello-access-token"></a>여기서는 액세스 토큰 hello?
웹 응용 프로그램에서 API 앱을 호출 하는 방법을 살펴볼 [OAuth 2.0 클라이언트 자격 증명 부여를 사용 하는 응용 프로그램 Id](../active-directory/develop/active-directory-authentication-scenarios.md#web-application-to-web-api),으로 hello 인증 흐름은 아래:

1. TooAzure AD hello 웹 응용 프로그램에서 사용자가 로그인 (hello 참조 [웹 브라우저 응용 프로그램 tooWeb](../active-directory/develop/active-directory-authentication-scenarios.md#web-browser-to-web-application)합니다.
2. hello Azure AD 권한 부여 끝점 hello 사용자 에이전트 백 toohello 클라이언트 응용 프로그램을 권한 부여 코드와 함께 리디렉션합니다. hello 사용자 에이전트가 인증 코드 toohello 클라이언트 응용 프로그램의 리디렉션 URI를 반환합니다.
3. hello 웹 응용 프로그램 toohello 웹 API를 인증 하 고 원하는 hello 리소스를 검색할 수 있도록 tooacquire 액세스 토큰이 필요 합니다. Hello 자격 증명, 클라이언트 ID 및 web API의 응용 프로그램 ID URI를 제공 하는 요청 tooAzure AD의 토큰 끝점을 만듭니다. Hello 권한 부여 코드 tooprove 해당 hello에서는 사용자가 동의 합니다.
4. Azure AD hello 응용 프로그램을 인증 하 고는 사용 되는 toocall hello 웹 API JWT 액세스 토큰을 반환 합니다.
5. HTTPS를 통해 웹 응용 프로그램 hello hello 요청 toohello web API의 hello 권한 부여 헤더에 JWT 액세스 토큰 tooadd hello "Bearer" 라는 지정 JWT 문자열을 반환 하는 hello를 사용 합니다. hello web API 다음 hello JWT 토큰을 확인 하 고 원하는 리소스를 반환 hello 유효성 검사가 성공 하면 키를 누릅니다.

이 "응용 프로그램 id" 흐름 hello web API는 해당 hello 웹 응용 프로그램 인증 된 hello 사용자를 신뢰합니다. 이런 이유로, 이 패턴을 신뢰할 수 있는 하위 시스템이라고 합니다. hello [이 페이지에는 다이어그램](https://docs.microsoft.com/azure/active-directory/active-directory-protocols-oauth-code) 인증 코드 부여 흐름이 작동 하는 방법에 대해 설명 합니다.

토큰 제한 된 라이선스를 취득에서 우리는 다음과 같습니다. hello 같은 신뢰할 수 있는 하위 패턴입니다. Azure 미디어 서비스에서 hello 라이선스 배달 서비스는 hello 웹 API 리소스에 "백 엔드 리소스" hello는 웹 응용 프로그램이 tooaccess 있어야 합니다. 따라서 hello 액세스 토큰 어디 입니까?

실제로, Azure AD에서 액세스 토큰을 가져옵니다. 사용자 인증에 성공하면 인증 코드가 반환됩니다. 클라이언트 ID와 응용 프로그램 키, 액세스 토큰에 대 한 tooexchange 함께 hello 권한 부여 코드가 다음을 사용 됩니다. 및 hello 액세스 토큰 가리키는 "포인터" 응용 프로그램에 액세스 또는 Azure 미디어 서비스 라이선스 배달 서비스를 나타내는입니다.

다음 hello 단계를 수행 하 여 Azure AD에서 hello "포인터" 응용 프로그램을 구성 및 tooregister 필요:

1. Hello Azure AD 테 넌 트

   * 로그온 URL과 함께 응용 프로그램(리소스)을 추가합니다.

   https://[resource_name].azurewebsites.net/ 및

   * 앱 ID URL:

   https://[aad_tenant_name].onmicrosoft.com/[resource_name];
2. Hello 리소스 응용 프로그램에 대 한 새 키를 추가 합니다.
3. Hello groupMembershipClaims 속성에는 다음 값 hello 있도록 hello 응용 프로그램 매니페스트 파일 업데이트: "groupMembershipClaims": "All",  
4. "사용 권한 tooother applications" hello 절의 toohello 플레이어 웹 응용 프로그램을 가리키는 hello Azure AD 앱에서 위의 1 단계에서 추가 된 hello 리소스 응용 프로그램을 추가 합니다. "위임된 권한"에서 "[resource_name] 액세스" 확인 표시를 선택합니다. 이 hello 웹 응용 프로그램 사용 권한을 부여 toocreate 액세스 토큰 hello 리소스 응용 프로그램에 액세스 합니다. Visual Studio 및 Azure 웹 앱과 함께 개발 하는 경우 로컬 및 배포 된 버전의 hello 웹 앱에 대 한이 수행 해야 있습니다.

따라서 Azure AD에서 발급 하는 hello JWT 토큰은 실제로이 "포인터" 리소스에 액세스 하기 위한 hello 액세스 토큰입니다.

### <a name="what-about-live-streaming"></a>라이브 스트리밍의 경우는 어떨까요?
위의 hello에서 논의 했습니다 되었습니다 중점적으로 주문형으로 자산입니다. 라이브 스트리밍의 경우는 어떨까요?

hello 다행 스럽게도 정확 하 게 사용할 수 있는 동일한 디자인 및 구현 "VOD 자산"으로 프로그램과 연결 된 hello 자산을 처리 하 여 Azure 미디어 서비스에서 라이브 스트리밍 보호를 위한 hello 합니다.

구체적으로 잘 알려진 toodo 라이브 Azure 미디어 서비스에서 스트리밍 채널을 다음 hello 채널에서 프로그램 toocreate 사용 해야 합니다. toocreate hello 프로그램 toocreate hello 프로그램에 대 한 라이브 보관 hello를 포함 하는 자산 해야 합니다. 다중 DRM 보호 하기만 하면 toodo, hello 라이브 콘텐츠의와 순서 tooprovide CENC에서에서은 tooapply hello 동일한 설치/처리 toohello 자산 hello 프로그램을 시작 하기 전에 "VOD 자산" 인 경우에 따라 합니다.

### <a name="what-about-license-servers-outside-of-azure-media-services"></a>Azure 미디어 서비스 외부에서 라이선스 서버는 어떨까요?
고객들은 대체로 고유한 데이터 센터 또는 DRM 서비스 공급자가 호스팅하는 형태로 라이선스 서버 팜에 투자할 수 있습니다. 다행히 Azure 미디어 서비스 콘텐츠 보호 하면 toooperate 혼합 모드에서: 내용이 호스팅되며 Azure 미디어 서비스 외부의 서버를 통해 DRM 라이선스를 배달 하는 동안 Azure 미디어 서비스에서 동적으로 보호 합니다. 이 경우 변경 따른 다음 hello 가지가 있습니다.

1. hello 보안 토큰 서비스 요구 tooissue 있는 토큰을 사용할 수 있으며 hello 라이선스 서버 팜에서 확인할 수 있습니다. 예를 들어 Axinom에서 제공 하는 hello Widevine 라이선스 서버 "메시지 자격"을 포함 하는 특정 JWT 토큰이 필요 합니다. 따라서 STS tooissue toohave 이러한 JWT 토큰이 필요 합니다. hello 작성자는 이러한 구현을 완료 하 고 문서에 따라 hello에서 hello 세부 정보를 찾을 수 있습니다 [Azure 설명서 센터](https://azure.microsoft.com/documentation/): [를 사용 하 여 Axinom toodeliver Widevine 라이선스tooAzure미디어서비스](media-services-axinom-integration.md).
2. Azure 미디어 서비스에서 tooconfigure 라이선스 배달 서비스 (ContentKeyAuthorizationPolicy) 더 이상 필요 합니다. 필요한 toodo 됩니다 (예: PlayReady, Widevine 및 FairPlay) tooprovide hello 라이선스 취득 Url을 구성한 경우 AssetDeliveryPolicy CENC 다중 DRM으로 설정 합니다.

### <a name="what-if-i-want-toouse-a-custom-sts"></a>사용자 지정 STS toouse을 원하는 경우 어떻게 합니까?
고객이 JWT 토큰을 제공 하는 데 toouse 사용자 지정 STS (보안 토큰 서비스)를 선택할 수 있는 몇 가지 이유 있을 수 있습니다. 다음과 같습니다.

1. hello Identity 공급자 (IDP) hello 고객에서 사용 하는 STS를 지원 하지 않습니다. 이 경우 사용자 지정 STS가 옵션일 수 있습니다.
2. hello 고객 요금 청구 시스템 고객의 구독자와 STS의 통합에 보다 유연한 또는 긴밀 하 게 제어를 해야 합니다. 예를 들어 MVPD 연산자 premium, basic, 스포츠와 같은 여러 OTT 구독자 패키지를 제공할 수 있습니다, 그리고 hello 오른쪽 패키지의 내용에만 사용할 수 없도록 등 hello 연산자가 구독자의 패키지와 토큰의 toomatch hello 클레임을 지정할 수 있습니다. 이 경우 사용자 지정 STS hello 필요한 유연성 및 제어를 제공 합니다.

두 가지 변경 내용이 사용자 지정 STS를 사용 시 toobe가 필요 합니다.

1. 자산에 대 한 라이선스 배달 서비스를 구성할 때 toospecify hello 보안 키 대신 Azure Active Directory에서 현재 키 hello hello 사용자 지정 STS (아래의 자세한 내용)에서 확인에 사용 해야 합니다.
2. JTW 토큰 생성 되 면 hello Azure Active Directory에 hello 현재 X509 인증서의 개인 키 대신 보안 키가 지정 됩니다.

두 가지 유형의 보안 키가 있습니다.

1. 대칭 키: hello; JWT 토큰을 확인 하 고 생성 모두 동일한 키가 사용
2. 비대칭 키: 공개-개인 키 쌍에서 X509 인증서 JWT 토큰 및 hello 공개 키 hello 토큰을 확인 하는 데 암호화/생성을 위한 개인 키로 사용 됩니다.

#### <a name="tech-note"></a>기술 참고 사항
.NET Framework를 사용 하는 경우 C# 개발 플랫폼으로 X509 hello / 비대칭 보안 키에 사용 된 인증서 키 길이가 2048 이상 있어야 합니다. 이 작업은 hello 클래스 System.IdentityModel.Tokens.X509AsymmetricSecurityKey.NET Framework에서의 필요 합니다. 그렇지 않으면 hello 다음 예외가 throw 됩니다.

IDX10630: 서명 하는 것에 대 한 'System.IdentityModel.Tokens.X509AsymmetricSecurityKey' hello '2048' 비트 보다 작을 수 없습니다.

## <a name="hello-completed-system-and-test"></a>완료 하는 hello 시스템 및 테스트
단계별로 몇 가지 시나리오를 완료 하는 hello 종단 간 시스템에 판독기 로그인 계정의 가져오기 전에 basic hello 동작의 "형식"을 가질 수 있습니다.

hello 플레이어 웹 응용 프로그램 및 로그인 있습니다 [여기](https://openidconnectweb.azurewebsites.net/)합니다.

필요한 경우 "비통합" 시나리오: 어떤은 보호 되지 않은 상태로 하나 또는 DRM으로 보호 된 Azure 미디어 서비스에서 호스트 되는 비디오 자산 하지만 (요청 하는 라이선스 toowhoever 발급) 토큰 인증 없이 테스트할 수 로그인 없이 (전환 하 여 tooHTTP HTTP를 통해이 비디오 스트리밍).

필요한 경우-완벽 한 통합된 시나리오: 비디오 자산 인증 토큰 및 JWT 토큰을 Azure AD에서 생성 되 고 Azure 미디어 서비스에서 동적 DRM 보호 중인 toologin 사용 해야 합니다.

### <a name="user-login"></a>사용자 로그인
순서 tootest hello 종단 간 통합된 DRM 시스템을 toohave "계정" 만들거나 추가 해야 합니다.

계정이란?

원래 Microsoft 계정 사용자만 Azure에 액세스할 수 있었으나 이제는 이 두 가지 시스템의 사용자도 액세스할 수 있습니다. 이 작업을 수행 하 여 모든 hello Azure 속성 신뢰 있으면 조직 사용자를 인증 하는 Azure AD 인증을 위해 Azure AD와 페더레이션 관계를 만들어 Azure AD hello Microsoft 계정 소비자 id 시스템을 신뢰 tooauthenticate 소비자 사용자입니다. 결과적으로, Azure AD는 "기본" Azure AD 계정 뿐 아니라 수 tooauthenticate "게스트" Microsoft 계정입니다.

Microsoft 계정 (MSA) 도메인을 신뢰 하는 Azure AD, 이후 hello 도메인 toohello 사용자 지정 Azure AD를 다음 중 하나에서 모든 계정 테 넌 트 및 계정 toologin hello를 사용 하 여 추가할 수 있습니다.

| **도메인 이름** | **도메인** |
| --- | --- |
| **사용자 지정 Azure AD 테넌트 도메인** |somename.onmicrosoft.com |
| **회사 도메인** |microsoft.com |
| **Microsoft 계정(MSA) 도메인** |outlook.com, live.com, hotmail.com |

Hello 작성자 toohave 생성 되거나 자동으로 추가 계정 문의할 수 있습니다.

다른 도메인 계정을 사용 하는 다른 로그인 페이지의 hello 스크린 샷에 다음과 같습니다.

**사용자 지정 Azure AD에 도메인 계정을 테 넌 트**: hello 사용자 지정 Azure AD 테 넌 트 도메인의 hello 사용자 지정된 로그인 페이지를 참조 하는 경우에 합니다.

![사용자 지정 Azure AD 테넌트 도메인 계정](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain1.png)

**스마트 카드와 Microsoft 도메인 계정을**: Microsoft 회사에서 사용자 지정 하는 hello 로그인 페이지를 참조 하는 경우 2 단계 인증을 가진 IT 합니다.

![사용자 지정 Azure AD 테넌트 도메인 계정](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain2.png)

**Microsoft 계정 (MSA)**:이 경우 소비자에 대 한 hello Microsoft 계정 로그인 페이지를 표시 합니다.

![사용자 지정 Azure AD 테넌트 도메인 계정](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain3.png)

### <a name="using-encrypted-media-extensions-for-playready"></a>PlayReady에 암호화된 미디어 확장 사용
최신 브라우저와 암호화 된 미디어 확장 (EME) Windows 10에서는 PlayReady Windows 8.1 IE 11 및 Microsoft Edge 브라우저와 같은 지원 하지 것입니다는 PlayReady에 대 한 기본 DRM EME에 대 한 hello 합니다.

![PlayReady에 EME 사용](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready1.png)

hello 어두운 플레이어 영역이 PlayReady 보호에서 보호 된 비디오의 화면 캡처를 만드는 방지 toohello 사실 때문입니다.

hello 다음 화면 표시 hello 플레이어 플러그 인 및 MSE/EME 지원 됩니다.

![PlayReady에 EME 사용](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready2.png)

Windows 10의 Microsoft Edge 및 IE 11에 있는 EME를 통해 이를 지원하는 Windows 10 장치에서 [PlayReady SL3000](https://www.microsoft.com/playready/features/EnhancedContentProtection.aspx/)을 호출할 수 있습니다. PlayReady SL3000 향상 된 프리미엄 콘텐츠 hello 흐름의 잠금을 해제 (4k HDR, 등) 및 새로운 콘텐츠 전송 모델 (향상 된 콘텐츠에 대 한 초기 창).

Hello Windows 장치에 집중: PlayReady hello HW (PlayReady SL3000) Windows 장치에서 사용할 수에 DRM hello 됩니다. 스트리밍 서비스는 EME 또는 UWP 응용 프로그램을 통해 PlayReady를 사용하고 PlayReady SL3000을 사용하여 다른 DRM보다 더 높은 화질을 제공할 수 있습니다. 일반적으로 2k 콘텐츠 Chrome 또는 Firefox를 통해 전달 됩니다 및에 Microsoft 가장자리/IE11 또는 UWP 응용 프로그램을 통해 콘텐츠 K 4 hello 같은 장치 (에 따라 서비스 설정 및 구현)입니다.

#### <a name="using-eme-for-widevine"></a>Widevine에 EME 사용
EME/Widevine 지원을 통해 Windows 10, Windows 8.1, Mac OSX Yosemite 및 Chrome에서 Chrome 41 + 같은 Android 4.4.4에 최신 브라우저에 Google Widevine는 hello EME 뒤 DRM입니다.

![Widevine에 EME 사용](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine1.png)

Widevine은 보호된 비디오의 화면 캡처 만들기를 차단하지 않습니다.

![Widevine에 EME 사용](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine2.png)

### <a name="not-entitled-users"></a>자격이 없는 사용자
사용자 "권한을 부여 받은 사용자" 그룹의 멤버인 경우 hello 사용자 수 toopass "권한 검사" 되지 않으며 아래와 같이 hello 다중 DRM 라이선스 서비스 tooissue hello 요청된 라이선스를 거부 합니다. hello 자세한 설명은입니다 "라이선스 획득 하지 못했습니다", 정상적으로 되 합니다.

![자격이 없는 사용자](./media/media-services-cenc-with-multidrm-access-control/media-services-unentitledusers.png)

### <a name="running-custom-secure-token-service"></a>사용자 지정 보안 토큰 서비스 실행
사용자 지정 보안 토큰 서비스 (STS)를 실행 중인 hello 시나리오에 대 한는 hello JWT 토큰 대칭 또는 비대칭 키를 사용 하 여 hello 사용자 지정 STS에서 발급 될 됩니다.

대칭 키 (Chrome 사용)를 사용 하 여 hello 사례:

![사용자 지정 STS 실행](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts1.png)

X509 통해 비대칭 키를 사용 하 여 대/소문자 hello 인증서 (Microsoft 최신 브라우저를 사용 하 여).

![사용자 지정 STS 실행](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts2.png)

경우 위의 hello 모두에서 사용자 인증이 계속 hello 동일 – Azure AD를 통해. hello 유일한 차이점은 hello Azure AD는 대신 사용자 지정 STS에서 발급 한 JWT 토큰이 됩니다. 물론, 동적 CENC 보호를 구성할 때 라이선스 배달 서비스의 hello 제한이 hello 유형을 지정 JWT 토큰에 대칭 키나 비대칭 키입니다.

## <a name="summary"></a>요약
이 문서에서는 다중 원시 DRM 및 토큰 인증을 통한 액세스 제어가 포함된 CENC와 Azure, Azure 미디어 서비스 및 Azure 미디어 플레이어를 사용한 디자인 및 구현에 대해 설명했습니다.

* 참조 디자인; DRM/CENC 하위 시스템의 모든 hello 필요한 구성 요소를 포함 하 게 제공 됩니다.
* Azure, Azure 미디어 서비스 및 Azure 미디어 플레이어에 대한 참조 구현입니다.
* Hello 디자인 및 구현에 직접 관련 된 일부 항목 에서도 설명 합니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
 
