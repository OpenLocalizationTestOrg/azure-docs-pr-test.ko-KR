---
title: "aaaSettings 및 데이터 로밍 FAQ | Microsoft Docs"
description: "설정 및 앱 데이터 동기화에 대 한 답변 toosome 질문 IT 관리자가 있을 수를 제공 합니다."
services: active-directory
keywords: "엔터프라이즈 상태 로밍 설정, windows 클라우드, 엔터프라이즈 상태 로밍에 대한 질문과 대답"
documentationcenter: 
author: tanning
manager: swadhwa
editor: curtand
ms.assetid: c0824f5c-129b-4240-969f-921f6a64eae7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4d6d6619b3a5fbd1d274603808d89b73ed942cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="settings-and-data-roaming-faq"></a>설정 및 데이터 로밍 FAQ
이 토픽에서는 설정 및 앱 데이터 동기화에 대한 IT 관리자의 질문에 답변합니다.

## <a name="what-data-roams"></a>어떤 데이터가 로밍됩니까?
**Windows 설정**: hello hello Windows 운영 체제에 기본 제공 되는 PC 설정 합니다. 일반적으로이 사용자 PC를 개인 설정 하는 설정 하 고 hello 다음 광범위 한 범주를 포함:

* *테마*- 바탕 화면 테마 및 작업 표시줄 설정과 같은 기능 포함
* *Internet Explorer 설정*- 최근에 열어본 탭 및 즐겨찾기 포함
* *Edge 브라우저 설정*- 즐겨찾기, 읽기 목록 등
* *암호*- 인터넷 암호, Wi-Fi 프로필 등 포함
* *언어 기본 설정*- 키보드 레이아웃, 시스템 언어, 날짜 및 시간 등에 대한 설정 포함
* *접근성 기능*- 고대비 테마, 내레이터, 돋보기 등
* *기타 Windows 설정*- 명령 프롬프트 설정, 응용 프로그램 목록 등

**응용 프로그램 데이터**: 유니버설 Windows 앱 폴더, 로밍 설정을 데이터 tooa를 작성할 수 있으며 toothis 폴더에 기록 된 모든 데이터가 자동으로 동기화 됩니다. 그 toohello 개별 응용 프로그램 개발자 toodesign이 기능의 앱 tootake 이점이 제공 됩니다. Toodevelop 로밍를 사용 하는 유니버설 Windows 앱 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 hello [응용 프로그램 데이터 저장소 API](https://msdn.microsoft.com/library/windows/apps/mt299098.aspx) 및 hello [Windows 8 응용 프로그램 개발자 블로그 로밍 데이터](http://blogs.msdn.com/b/windowsappdev/archive/2012/07/17/roaming-your-app-data.aspx)합니다.

## <a name="what-account-is-used-for-settings-sync"></a>설정 동기화에 어떤 계정이 사용됩니까?
Windows 8 및 Windows 8.1에서는 설정 동기화에 항상 소비자 Microsoft 계정이 사용되었습니다. 기업 사용자는 hello 기능 tooconnect Microsoft 계정 tootheir Active Directory 도메인 계정 toogain 액세스 toosettings 동기화 했습니다. Windows 10에서는 이 연결된 Microsoft 계정 기능이 기본/보조 계정 프레임워크로 대체됩니다.

hello 계정 toosign tooWindows에서 사용 되는 hello 기본 계정이 정의 됩니다. Microsoft 계정, Azure Active Directory(Azure AD) 계정, 온-프레미스 Active Directory 계정 또는 로컬 계정일 수 있습니다. 또한 toohello 기본 계정에서 Windows 10 사용자 하나 이상의 보조 클라우드 계정 tootheir 장치를 추가할 수 있습니다. 보조 계정은 일반적으로 Microsoft 계정, Azure AD 계정 또는 Gmail이나 Facebook과 같은 기타 계정입니다. 이러한 보조 계정 액세스 single sign-on 및 Windows 스토어 hello 같은 tooadditional 서비스를 제공 하지만 설정 동기화 전원을 켤 수 없습니다.

Windows 10 hello 장치에 대 한 기본 계정을 hello만 설정 동기화에 사용할 수 있습니다 (참조 [Windows 10의 Windows 8 tooAzure AD 설정 동기화에서 Microsoft 계정 설정 동기화에서 업그레이드 하려면 어떻게 해야 합니까?](active-directory-windows-enterprise-state-roaming-faqs.md#how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-to-azure-ad-settings-sync-in-windows-10)).

데이터는 hello 장치에서 다른 사용자 계정 hello 간에 함께 저장 되지 됩니다. 설정 동기화에는 두 가지 규칙이 있습니다.

* Windows 설정 hello 기본 계정을 사용 하 여 항상 로밍 됩니다.
* 응용 프로그램 데이터는 hello 사용 되는 계정 tooacquire hello 앱으로 태그가 지정 됩니다. Hello 기본 계정을 사용 하 여 태그를 지정 하는 앱만 동기화 합니다. 응용 프로그램 소유권 태그는 앱을 테스트용 로드 된 hello Windows 스토어 또는 모바일 장치 관리 (MDM)를 통해 때 결정 됩니다.

응용 프로그램의 소유자를 식별할 수 없으면 hello 기본 계정으로 로밍 됩니다. Windows 8 또는 Windows 8.1 tooWindows 10에서에서 장치를 업그레이드 하는 경우 hello Microsoft 계정에 의해 획득 하는 대로 모든 hello 앱을 태그가 지정 됩니다. 대부분의 사용자가 hello Windows 스토어를 통해 앱을 획득 하 고 Azure AD 계정 이전 tooWindows 10에 대 한 Windows 스토어 지원 되지 않았습니다 때문입니다. 오프 라인 라이선스를 통해 앱이 설치 되어 hello 장치의 기본 계정을 hello를 사용 하 여 하는 태그가 hello 앱 지정 됩니다.

> [!NOTE]
> Windows 10 장치에 회사 소유는 설정 되며 연결 된 tooAzure AD 도메인 계정으로 Microsoft 계정 tooa 연결할 더 이상 수 없습니다. 모든 hello 사용자의 데이터 동기화 기능 tooconnect Microsoft 계정 tooa 도메인 계정을 hello 있고 toohello Microsoft 계정 (즉, hello Microsoft 계정 연결 하는 hello Microsoft 계정 및 Active Directory 기능을 통해 로밍)에서 제거 됩니다 조인된 tooa는 Windows 10 장치는 Active Directory 또는 Azure AD 환경에 연결 합니다.
>
>

## <a name="how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-tooazure-ad-settings-sync-in-windows-10"></a>Windows 10의 Windows 8 tooAzure AD 설정 동기화에서 Microsoft 계정 설정 동기화에서 업그레이드 하려면 어떻게 해야 합니까?
연결 된 Microsoft 계정으로 Windows 8 또는 Windows 8.1 실행 하는 조인 된 toohello Active Directory 도메인의 경우 Microsoft 계정을 통해 설정을 동기화 합니다. TooWindows 10을 업그레이드 한 후 도메인에 가입 된 사용자 및 hello Active Directory 도메인을 Azure AD와 연결 되지 않으면 Microsoft 계정을 통해 사용자 설정을 유지할지 toosync 계속 됩니다.

Hello 온-프레미스 Active Directory 도메인은 Azure AD와 연결 하는 경우 장치 hello 연결 된 Azure AD 계정을 사용 하 여 toosync 설정을 시도 합니다. 관리자에 게 Azure AD 엔터프라이즈 상태 로밍, 연결 된 설정 되지 않으면 Azure AD 계정 설정을 동기화 하는 중지 됩니다. Windows 10 사용자인 경우 Azure AD ID로 로그인하면 관리자가 Azure AD를 통한 설정 동기화를 활성화하는 즉시 Windows 설정 동기화가 시작됩니다.

회사 장치에서 개인 데이터를 저장 하는 경우에 Windows 운영 체제 및 응용 프로그램 데이터가 시작 됩니다 tooAzure AD를 동기화 하는 중 알고 있어야 합니다. 이 hello 다음 영향을 줍니다.

* 개인 Microsoft 계정 설정을 hello 설정 외 작업에 드리프트 되거나 학교 Azure AD 계정이 됩니다. 동기화 hello Microsoft 계정 및 Azure AD 설정 때문에 이것이 별도 계정을 사용 하 여 지금 됩니다.
* 연결된 Microsoft 계정을 통해 이미 동기화된 Wi-Fi 암호, 웹 자격 증명 및 Internet Explorer 즐겨찾기 등 개인 데이터는 Azure AD를 통해 동기화됩니다.

## <a name="how-do-microsoft-account-and-azure-ad-enterprise-state-roaming-interoperability-work"></a>Microsoft 계정과 Azure AD 엔터프라이즈 상태 로밍의 상호 운용성이 어떻게 됩니까?
2015 년 11 월 hello 또는 이상 릴리스의 Windows 10에서 엔터프라이즈 상태 로밍만 지원 됩니다는 단일 계정에 대 한 한 번에. 회사 또는 학교 계정 Azure AD 사용 하 여 tooWindows에 로그인 할 경우 모든 데이터는 Azure AD를 통해 동기화 됩니다. 개인 Microsoft 계정을 사용 하 여 tooWindows에 로그인 할 경우 모든 데이터는 hello Microsoft 계정을 통해 동기화 됩니다. Hello 장치에만 hello 기본 로그인 계정을 사용 하 여 유니버설 응용 프로그램 데이터 로밍 하 고 hello 응용 프로그램의 라이선스는 hello 기본 계정에서 소유 하는 경우에 로밍 됩니다. 보조 계정에서 소유 하는 hello 앱에 대 한 유니버설 응용 프로그램 데이터 동기화 되지 않습니다.

## <a name="do-settings-sync-for-azure-ad-accounts-from-multiple-tenants"></a>여러 테넌트의 Azure AD 계정에 대한 설정이 동기화됩니까?
Azure AD 테 넌 트 hello에 있는 서로 다른 여러 Azure AD 계정 하는 경우 동일한 장치 각 Azure AD 테 넌 트에 대 한 hello 장치 레지스트리 toocommunicate Azure 권한 관리 (Azure RMS)를 업데이트 해야 합니다.  

1. 각 Azure AD 테 넌 트에 대 한 hello를 GUID를 찾습니다. Hello Azure 클래식 포털을 열고 Azure AD 테 넌 트를 선택 합니다. hello GUID hello 테 넌 트에 대 한 브라우저의 주소 표시줄 hello에에서 hello URL입니다. 예: `https://manage.windowsazure.com/YourAccount.onmicrosoft.com#Workspaces/ActiveDirectoryExtension/Directory/Tenant GUID/directoryQuickStart`
2. Tooadd hello 레지스트리 키가 필요 hello GUID를 사용 하는 다음 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\SettingSync\WinMSIPC\<ID GUID를 테 넌 트 >**합니다.
   Hello에서 **ID GUID를 테 넌 트** 키, 명명 된 새 다중 문자열 값 (다중-REG-SZ) **AllowedRMSServerUrls**합니다. 해당 데이터에 대 한 hello hello의 배포 지점 Url hello 장치 액세스 하는 다른 Azure 테 넌 트 라이선스를 지정 합니다.
3. Hello hello를 실행 하 여 배포 지점 Url 라이선스를 찾을 수 있습니다 **Get-aadrmconfiguration** cmdlet. Hello hello에 대 한 값 경우 **LicensingIntranetDistributionPointUrl** 및 **LicensingExtranetDistributionPointUrl** 다르면 두 값을 지정 합니다. 값은 hello hello 동일, hello 값을 한 번만 지정 합니다.

## <a name="what-are-hello-roaming-settings-options-for-existing-windows-desktop-applications"></a>기존 Windows 데스크톱 응용 프로그램에 대 한 hello 로밍 설정 옵션은 무엇입니까?
로밍은 유니버설 Windows 앱에서만 작동합니다. 기존 Windows 데스크톱 응용 프로그램에서 로밍을 활성화할 수 있는 두 가지 옵션이 있습니다.

* hello [데스크톱 브리지](http://aka.ms/desktopbridge) 프로그램 기존 Windows 데스크톱 앱 toohello 유니버설 Windows 플랫폼을 제공 하는 데 도움이 됩니다. 여기에서 최소한의 코드 변경 내용은 Azure AD 앱 데이터 로밍 tootake 활용이 필요 합니다. 앱 id 사용 하 여 앱을 제공 하는 hello 데스크톱 브리지는 필요한 tooenable 앱 데이터를 기존 데스크톱 응용 프로그램에 대 한 로밍 합니다.
* [UE-V(사용자 경험 가상화)](https://technet.microsoft.com/library/dn458947.aspx) 를 사용하면 기존 Windows 데스크톱 앱에 대한 사용자 지정 설정 템플릿을 만들 수 있고 Win32 앱에 대해서만 로밍을 사용할 수 있습니다. 이 옵션 hello hello 응용 프로그램의 응용 프로그램 개발자 toochange 코드 하지 않아도 됩니다. Ue-v 제한 tooon 온-프레미스 Active Directory Microsoft Desktop Optimization Pack hello를 구매한 고객에 대 한 로밍 됩니다.

관리자의 Windows 운영 체제 설정 및 통해 유니버설 앱 데이터 로밍 변경 하 여 Ue-v tooroam Windows 데스크톱 응용 프로그램 데이터를 구성할 수 있습니다 [Ue-v 그룹 정책이](https://technet.microsoft.com/itpro/mdop/uev-v2/configuring-ue-v-2x-with-group-policy-objects-both-uevv2)를 포함 하 여:

* Windows 설정 로밍 그룹 정책
* Windows 앱 동기화 안 함 그룹 정책
* Internet Explorer hello 응용 프로그램 섹션에서 로밍

Hello 이후, Microsoft Ue-v Windows에 강력 하 게 통합 하는 방법으로 toomake 조사 하 고 hello Azure AD 클라우드를 통해 Ue-v tooroam 설정을 확장할 수 있습니다.

## <a name="can-i-store-synced-settings-and-data-on-premises"></a>동기화된 설정 및 데이터를 온-프레미스에 저장할 수 있나요?
엔터프라이즈 상태 로밍 hello Azure 클라우드에에서 동기화 된 모든 데이터를 저장합니다. UE-V는 온-프레미스 로밍 솔루션을 제공합니다.

## <a name="who-owns-hello-data-thats-being-roamed"></a>누가 hello 데이터 로밍 중인를 소유 합니까?
hello 기업 자체 hello 엔터프라이즈 상태 로밍를 통해 로밍 하는 데이터입니다. 데이터는 Azure 데이터 센터에 저장됩니다. 모든 사용자 데이터 및 Azure RMS를 사용 하 여 hello 클라우드에서 대기 모두 전송 중에 암호화 됩니다. 이 사용자 자격 증명과 같은 중요 한 특정 데이터만 hello 장치를 벗어나기 전에를 암호화 하는 비교 개선 tooMicrosoft 계정 기반 설정 동기화 합니다.

Microsoft는 커밋된 toosafeguarding 고객 데이터입니다. 엔터프라이즈 사용자의 설정 데이터는 Windows 10 장치에서 나오기 전에 Azure RMS를 통해 암호화되므로 다른 사용자가 이 데이터를 읽을 수 없습니다. 조직에 Azure RMS 유료 구독 경우 추적 등 다른 Azure RMS 기능을 사용 하 고 문서를 해지, 자동으로 중요 한 정보가 포함 된 메일을 보호 하 고 관리할 수 고유한 키 ("bring your own key" 솔루션을도 hello 알려진 byok 방식)입니다. 이러한 기능 및 Azure RMS의 작동 방식에 대한 자세한 내용은 [Azure Rights Management란](https://technet.microsoft.com/jj585026.aspx)을 참조하세요.

## <a name="can-i-manage-sync-for-a-specific-app-or-setting"></a>특정 앱 또는 설정에 대한 동기화를 관리할 수 있나요?
Windows 10에서 개별 응용 프로그램에 대 한 로밍 없습니다 MDM 또는 그룹 정책 설정을 toodisable 있습니다. 테넌트 관리자는 관리되는 장치의 모든 앱에 대해 앱 데이터 동기화를 비활성화할 수 있지만 앱당 또는 앱 내부 수준에서 더욱 정교하게 제어하는 방법은 없습니다.

## <a name="how-can-i-enable-or-disable-roaming"></a>로밍을 활성화/비활성화하려면 어떻게 해야 하나요?
Hello에 **설정** 응용 프로그램에 너무 이동**계정** > **설정 동기화**합니다. 이 페이지에서 어느 계정이 사용 되는 tooroam 설정 되 고 볼 수 있습니다 하 고 로밍 설정 toobe의 개별 그룹을 사용 하지 않도록 설정 하거나 설정할 수 있습니다.

## <a name="what-is-microsofts-recommendation-for-enabling-roaming-in-windows-10"></a>Microsoft는 Windows 10 로밍 활성화에 대해 무엇을 권장합니까?
Microsoft에서는 사용자 프로필 로밍, UE-V, 엔터프라이즈 상태 로밍을 포함하여 몇 가지 설정 로밍 솔루션을 제공하고 있습니다.  Microsoft는 커밋된 toomaking 엔터프라이즈 상태 로밍 이후 버전의 Windows에에서 투자 합니다. 조직 또는 모두에 이동 데이터 toohello 클라우드와 없으면 기본 로밍 기술로 Ue-v를 사용 하는 하도록 권장 합니다. 조직 로밍 기존의 Windows 데스크톱 응용 프로그램에 대 한 지원이 필요 하지만 eager toomove toohello 클라우드, 하는 경우에 엔터프라이즈 상태 로밍 및 Ue-v를 사용 하는 것이 좋습니다. UE-V와 엔터프라이즈 상태 로밍이 매우 비슷한 기술이지만 상호 배타적인 관계는 아니며 상호 보완적 toohelp 조직 hello 로밍 사용자가 필요로 하는 서비스를 제공 하는지 확인 합니다.  

엔터프라이즈 상태 로밍 및 Ue-v를 사용할 때 hello 규칙에 적용 됩니다.

* 엔터프라이즈 상태 로밍는 hello 장치에서 hello 기본 로밍 에이전트입니다. Ue-v 되 고 사용 되는 toosupplement hello "Win32 간격입니다."
* Windows 설정 및 최신 UWP 앱 데이터 로밍 Ue-v 정책을 hello Ue-v 그룹을 사용 하는 경우 해제 되어야 합니다. UE-V 그룹 정책을 사용하여 비활성화해야 합니다.

## <a name="how-does-enterprise-state-roaming-support-virtual-desktop-infrastructure-vdi"></a>엔터프라이즈 상태 로밍은 VDI(가상 데스크톱 인프라)를 어떻게 지원하나요?
엔터프라이즈 상태 로밍은 서버 SKU가 아니라 Windows 10 클라이언트 SKU에서 지원됩니다. 클라이언트 VM 하이퍼바이저 컴퓨터에서 호스트 toohello 가상 컴퓨터를 원격으로 로그인 하는 경우 데이터 로밍 됩니다. 여러 사용자가 동일한 운영 체제 및 사용자가 전체 데스크톱 경험을 위해 tooa 서버에 원격으로 로그인 하는 hello를 공유 하는 경우 로밍 작동 하지 않을 수 있습니다. 후자의 세션 기반 경우 hello 공식적으로 지원 되지 않습니다.

## <a name="what-happens-when-my-organization-purchases-azure-rms-after-using-roaming"></a>조직에서 로밍을 사용하다가 Azure RMS를 구입하면 어떻게 되나요?
조직에서 이미 사용 하는 경우 Windows 10에서 로밍 hello Azure RMS 제한 된 사용 가능한 구독으로 유료 Azure RMS 구독을 구입 영향을 받지 hello 로밍 기능의 hello 기능에 없으며 구성 변경 없이 됩니다. IT 관리자가 필요합니다.

## <a name="known-issues"></a>알려진 문제
Hello에 hello 설명서를 참조 하십시오 [문제 해결](active-directory-windows-enterprise-state-roaming-troubleshooting.md) 알려진 문제의 목록에 대 한 섹션. 

## <a name="related-topics"></a>관련된 항목
* [엔터프라이즈 상태 로밍 개요](active-directory-windows-enterprise-state-roaming-overview.md)
* [Azure Active Directory에서 엔터프라이즈 상태 로밍 활성화](active-directory-windows-enterprise-state-roaming-enable.md)
* [설정 동기화에 대한 그룹 정책 및 MDM 설정](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 로밍 설정 참조](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [문제 해결](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
