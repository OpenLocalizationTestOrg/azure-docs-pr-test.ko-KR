---
title: "aaaGroup 정책 및 MDM 설정 | Microsoft Docs"
description: "회사 소유의 장치에 사용해야 하는 그룹 정책 및 MDM(모바일 장치 관리) 설정에 대한 정보를 제공합니다. 이러한 정책은 적용된 toohello 사용자의 전체 장치 사용 됩니다."
services: active-directory
keywords: "엔터프라이즈 상태 로밍에 대한 그룹 정책 및 MDM 설정이란, 엔터프라이즈 상태 로밍, windows 클라우드"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a>그룹 정책 및 MDM 설정
이러한 정책 적용된 toohello 사용자의 전체 장치 때문에 이러한 그룹 정책 및 모바일 장치 관리 (MDM) 설정 회사 소유 장치에만 사용 합니다. 개인은 MDM 정책 toodisable 설정 동기화를 적용 하는 경우, 사용자 소유 장치 부정적인 영향을 줍니다 해당 장치의 hello 사용 합니다. 또한 다른 사용자 계정에 hello 장치 영향도 hello 정책에 의해 합니다.

개인 (비관리) 장치에 대 한 로밍 toomanage צ ְ ײ를 원하는 엔터프라이즈에 Azure 포털 tooenable hello 또는 그룹 정책 또는 mdm.를 사용 하 여 보다는 로밍, 사용 하지 않도록 설정
다음 표에서 hello hello 정책 설정을 사용할 수 있는 설명 합니다.

## <a name="mdm-settings"></a>MDM 설정
hello MDM 정책 설정은 tooboth Windows 10 및 Windows 10 Mobile에 적용 됩니다.  Windows 10 Mobile 지원은 사용자의 OneDrive 계정을 통한 Microsoft 계정 기반의 로밍에 대해서만 제공됩니다.  참조 하십시오 너무 Azure AD에 대 한 지원 되는 장치에 대 한 자세한 내용은 "장치 및 끝점" 섹션에 따라 동기화 하는 중입니다.

| 이름 | 설명 |
| --- | --- |
| Microsoft 계정 연결 허용 |사용자가 tooauthenticate를 hello 장치에서 Microsoft 계정을 사용할 수 있습니다. |
| 내 설정 동기화 허용 |사용자가 tooroam Windows 설정 및 앱 데이터가; 허용 비활성화 하면이 정책이 비활성화 됩니다 동기화 뿐만 아니라 모바일 장치에 백업 |

## <a name="group-policy-settings"></a>그룹 정책 설정
hello 그룹 정책 설정은 10 tooWindows 장치 tooan 조인 된 Active Directory 도메인에 적용 됩니다. hello 테이블에는 레거시 설정이 toomanage 동기화 설정에 표시 하는 엔터프라이즈 상태 로밍에 대 한 Windows 10에서는 작동 하지 않는 '사용 하지 않는' hello 설명에서와 설명 하는 포함 되어 있습니다.

| 이름 | 설명 |
| --- | --- |
| 계정: Microsoft 계정 차단 |이 정책 설정은 사용자가 이 컴퓨터에서 새 Microsoft 계정을 추가하지 못하게 차단합니다. |
| 동기화 안 함 |사용자가 tooroam Windows 설정 및 응용 프로그램 데이터를 방지합니다. |
| 개인 설정 동기화 안 함 |Hello 테마 그룹의 동기화를 해제 합니다. |
| 브라우저 설정 동기화 안 함 |Hello Internet Explorer 그룹의 동기화를 해제 합니다. |
| 암호 동기화 안 함 |암호 그룹 동기화 비활성화 |
| 기타 Windows 설정 동기화 안 함 |기타 Windows 설정 그룹 동기화 비활성화 |
| 바탕 화면 개인 설정 동기화 안 함 |사용 안 함. 효과 없음 |
| 데이터 통신 연결에서 동기화 안 함 |셀룰러 3G 같은 데이터 통신 연결에서 로밍 비활성화 |
| 앱 동기화 안 함 |사용 안 함. 효과 없음 |
| 앱 설정 동기화 안 함 |앱 데이터 로밍 비활성화 |
| 시작 설정 동기화 안 함 |사용 안 함. 효과 없음 |

## <a name="related-topics"></a>관련된 항목
* [엔터프라이즈 상태 로밍 개요](active-directory-windows-enterprise-state-roaming-overview.md)
* [Azure Active Directory에서 엔터프라이즈 상태 로밍 활성화](active-directory-windows-enterprise-state-roaming-enable.md)
* [설정 및 데이터 로밍 FAQ](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Windows 10 로밍 설정 참조](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [문제 해결](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

