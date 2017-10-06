---
title: "Azure AD Connect: 미리 보기의 기능 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect에서 미리 보기 상태인 기능을 더 자세하게 설명합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a>미리 보기 기능에 대한 자세한 내용
이 항목에서는 toouse 현재 미리 보기에서 기능이 방법에 대해 설명 합니다.

## <a name="group-writeback"></a>그룹 쓰기 저장
선택적 기능에서 그룹 쓰기 저장에 대 한 hello 옵션 있습니다 toowriteback **Office 365 그룹** Exchange가 설치 된 tooa 포리스트 합니다. 항상 hello 클라우드에서 마스터 되는 그룹입니다. Exchange 온-프레미스를 사용 하도록 설정한 경우를 작성할 수 있습니다 다시 이러한 그룹 tooon 온-프레미스 사용자가 온-프레미스 Exchange 사서함이 있는 보내고 다음이 그룹의 전자 메일을 받을 수 있습니다.

Office 365 그룹을 어떻게 toouse을 찾을 수 있습니다에 대 한 자세한 내용은 [여기](http://aka.ms/O365g)합니다.

Office 365 그룹은 온-프레미스 AD DS에서 배포 그룹으로 표현됩니다. 온-프레미스 Exchange server이 새로운 그룹 유형을 Exchange 2013 누적 업데이트 8 (2015 년 3 월에에서 릴리스됨) 또는 Exchange 2016 toorecognize 이어야 합니다.

**Hello 미리 보기 기간 동안 참고 사항**

* hello address book 특성은 현재 hello 미리 보기에 채워지지 않았습니다. 이 특성이 없으면 hello 그룹 hello 전체 주소 목록에에서 표시 되지 않습니다. 가장 쉬운 방법은 toopopulate hello이 특성은 toouse hello Exchange PowerShell cmdlet `update-recipient`합니다.
* Hello Exchange 스키마를 사용 하 여 포리스트만에 그룹에 대 한 유효한 대상이 됩니다. 없는 교환이 검색 된 다음 그룹 쓰기 저장 경우 가능한 tooenable 합니다.
* 현재 단일 포리스트 Exchange 조직 배포만 지원합니다. 있는 경우 둘 이상의 Exchange 조직 온-프레미스 사용자 다른 포리스트의 이러한 그룹 tooappear에 대 한 온-프레미스 GALSync 솔루션을 해야 합니다.
* 보안 그룹 또는 메일 그룹에는 hello 그룹 쓰기 저장 기능을 처리 하지 않습니다.

> [!NOTE]
> 구독 tooAzure AD Premium 그룹 쓰기 저장에 필요 합니다.
> 
>

## <a name="user-writeback"></a>사용자 쓰기 저장
> [!IMPORTANT]
> hello 사용자 쓰기 저장 미리 보기 기능은 제거 되었습니다 hello 2015 년 8 월 업데이트 tooAzure AD에에서 연결 합니다. 이 기능을 사용하도록 설정한 경우 사용하지 않도록 설정해야 합니다.
>
>

## <a name="next-steps"></a>다음 단계
[Azure AD Connect의 사용자 지정 설치](active-directory-aadconnect-get-started-custom.md)를 계속 진행합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
