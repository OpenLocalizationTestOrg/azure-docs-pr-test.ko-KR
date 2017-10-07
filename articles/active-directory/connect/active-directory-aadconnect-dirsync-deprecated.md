---
title: "디렉터리 동기화 및 Azure AD Sync에서 aaaUpgrade | Microsoft Docs"
description: "설명 방법을 디렉터리 동기화 및 Azure AD Sync tooAzure AD에서에서 tooupgrade 연결 합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Windows Azure Active Directory Sync 및 Azure Active Directory Sync 업그레이드
Azure AD Connect 가장 좋은 방법은 tooconnect Azure AD와 온-프레미스 디렉터리 hello는 및 Office 365 합니다. 이것이 좋은 시간 tooupgrade tooAzure Windows Azure Active Directory 동기화 (DirSync) 또는 Azure AD Sync에서 AD 연결 이러한 도구는 이제 사용 되지 않으며 2017 년 4 월 13에 대 한 지원의 끝에 도달 합니다.

hello 두 id 동기화 도구의 사용 되지 않는 단일 포리스트 고객 (DirSync) 및 다중 포리스트 및 기타 고급 고객 (Azure AD Sync) 제공 되었습니다. 이러한 이전 도구는 모든 시나리오에 사용할 수 있는 단일 솔루션(Azure AD Connect)으로 대체되었습니다. 이 도구는 새로운 기능, 향상된 기능 및 새로운 시나리오에 대한 지원을 제공합니다. toobe 수 toocontinue toosynchronize 프로그램 identity 데이터 tooAzure 온-프레미스 AD 및 Office 365 좋습니다 tooAzure AD를 업그레이드 하는 연결 합니다.

디렉터리 동기화의 마지막 릴리스입니다 hello은 2014 년 7 월에에서 발표 되었지만 및 Azure AD Sync의 hello 마지막 릴리스는 2015 년 5 월에에서 발표 되었습니다.

## <a name="what-is-azure-ad-connect"></a>Azure AD Connect의 정의
Azure AD Connect hello 후속 tooDirSync 및 Azure AD Sync가 있습니다. 이 두 도구가 지원하는 모든 시나리오를 통합합니다. 자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에서 확인할 수 있습니다.

## <a name="deprecation-schedule"></a>사용 중단 일정
| Date | 주석 |
| --- | --- |
| 2016년 4월 13일 |Microsoft Azure Active Directory 동기화("DirSync") 및 Azure Active Directory 동기화("Azure AD Sync")가 사용 중단될 예정입니다. |
| 2017년 4월 13일 |지원이 종료됩니다. 고객 수 tooopen tooAzure AD를 업그레이드 하지 않고 지원 케이스 더 이상 됩니다 먼저 연결 합니다. |
|2017년 12월 31일|Azure AD는 더 이상 Windows Azure Active Directory Sync(“DirSync”) 및 Microsoft Azure Active Directory Sync(“Azure AD Sync”)의 통신을 수락하지 않을 예정입니다.

## <a name="how-tootransition-tooazure-ad-connect"></a>어떻게 tootransition tooAzure AD 연결
DirSync를 실행 중인 경우 전체 업그레이드와 병렬 배포의 두 가지 방법으로 업그레이드할 수 있습니다. 전체 업그레이드는 대부분의 고객에게 권장되며, 최신 운영 체제가 설치되어 있고 개체 수가 50,000개 미만인 경우에 사용하는 것이 좋습니다. 경우에 따라 toodo 여기서 디렉터리 동기화 구성에는 병렬 배포에 Azure AD Connect를 실행 하는 새 tooa 서버 이동이 좋습니다.

Azure AD Sync를 사용하는 경우에는 전체 업그레이드가 권장됩니다. 가능한 tooinstall 병렬로 새 Azure AD Connect 서버 및 Azure AD Sync 서버 tooAzure AD에서에서 회전 마이그레이션을 수행 하려는 경우, 연결 합니다.

| 해결 방법 | 시나리오 |
| --- | --- |
| [DirSync에서 업그레이드](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>기존 DirSync 서버를 이미 실행 중인 경우</li> |
| [Azure AD Sync에서 업그레이드](active-directory-aadconnect-upgrade-previous-version.md) |<li>Azure AD Sync에서 전환하는 경우</li> |

어떻게 toosee 사용 하려는 경우 전체 toodo AD Connect 디렉터리 동기화 tooAzure에서 업그레이드 한 다음이 채널 9 비디오를 참조 하십시오.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>FAQ
**Q: 전자 메일 알림을 hello Azure 팀 및/또는 hello Office 365 메시지 센터에서 메시지를 받았는데 Connect를 사용 하 고 있습니다.**  
hello 알림은 toocustomers Azure AD Connect를 사용 하 여 빌드 번호 1.0도 전송 되었습니다. \*.0 (1.1 이전 릴리스를 사용 하 여). Azure AD Connect와 현재 toostay를 해제 하는 고객을 사용 하는 것이 좋습니다. hello [자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md) 1.1에서 도입 된 기능을 쉽게 tooalways 통해 최신 버전의 Azure AD Connect 설치 합니다.

**Q: DirSync/Azure AD Sync의 작동이 2017년 4월 13일에 중지됩니까?**  
DirSync/Azure AD Sync 13 2017 년 4 월에 toowork를 계속 됩니다.  그러나 Azure AD는 2017년 12월 31일이 되면 더 이상 DirSync/Azure AD Sync의 통신을 수락하지 않게 됩니다.

**Q: 어떤 DirSync 버전에서 업그레이드할 수 있나요?**  
현재 사용 중인 디렉터리 동기화 릴리스에서 지원 되는 tooupgrade 것 합니다.

**Q: FIM/MIM에 대 한 Azure AD 커넥터를 hello?**  
hello FIM/MIM에 대 한 Azure AD 커넥터에 **하지** 되었습니다 발표 사용 되지 않습니다. 현재 **기능 동결**상태입니다. Microsoft 권장 tooplan toomove 여기에서 사용 하는 고객 tooAzure AD 연결 합니다. 강력히 권장 toonot 시작 모든 새 배포를 사용 합니다. 이 커넥터는 hello 향후에 더 이상 사용 되지 발표 될 것입니다.

## <a name="additional-resources"></a>추가 리소스
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
