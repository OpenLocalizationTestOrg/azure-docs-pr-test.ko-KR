---
title: "알림 허브에 대 한 aaaSecurity"
description: "이 항목에서는 Azure 알림 허브 보안에 대해 설명합니다."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 6506177c-e25c-4af7-8508-a3ddca9dc07c
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f59ad4594c2c0a2e2b22ab0b6d6bad53825a4dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security"></a>보안
## <a name="overview"></a>개요
이 항목에서는 Azure 알림 허브의 hello 보안 모델에 설명 합니다. Hello를 구현 하 고 알림 허브 서비스 버스 엔터티의 이기 때문에 서비스 버스와 동일한 보안 모델. 자세한 내용은 참조 hello [서비스 버스 인증](https://msdn.microsoft.com/library/azure/dn155925.aspx) 항목입니다.

## <a name="shared-access-signature-security-sas"></a>SAS(공유 액세스 서명) 보안
알림 허브는 SAS(공유 액세스 서명)라는 엔터티 수준 보안 체계를 구현합니다. 이 체계는 메시징 엔터티 toodeclare를 too12 엔터티에 대 한 권한을 부여 하는 설명에 권한 부여 규칙을 수 있습니다.

"보안 클레임입니다." hello 섹션에서 설명한 대로 각 규칙 이름, 키 값 (공유 암호) 및 권한 집합이 포함 알림 허브를 만들 때 두 개의 규칙이 자동으로 만들어집니다: Listen 권한 (클라이언트 응용 프로그램에서는 hello) 및 모든 권한 (앱 백 엔드 사용 하 여 hello)를 사용 합니다.

Hello 정보를 통해 전송 하는 경우 클라이언트 응용 프로그램에서 등록 관리를 수행할 때 알림 (예: 날씨 업데이트)는 중요 한를 일반적인 방식으로 tooaccess 알림 허브는 hello 규칙 수신 전용 액세스 toohello의 toogive hello 키 값 클라이언트 응용 프로그램 및 toogive hello hello 규칙 대 한 모든 권한 toohello 앱 백 엔드에서의 키 값입니다.

Windows 스토어 클라이언트 응용 프로그램에 hello 키 값을 포함 하는 권장 되지 않습니다. Hello 키 값을 포함 하는 방식으로 tooavoid은 toohave hello에 대 한 클라이언트 응용 프로그램에서에서 검색할 시작 시 hello 앱 백 엔드에서.

반드시 수신 액세스 권한이 있는 키 hello toounderstand 앱 tooregister 모든 태그에 대 한 클라이언트 수 있습니다. 앱 등록 toospecific 태그 toospecific 클라이언트 (예: 사용자 Id를 나타내는 태그)를 제한 해야 하는 경우 앱 백 hello 등록을 수행 해야 합니다. 자세한 내용은 등록 관리를 참조하세요. 이러한 방식으로 hello 클라이언트 응용 프로그램에는 하지도 직접 액세스 tooNotification 허브 참고 합니다.

## <a name="security-claims"></a>보안 클레임
알림 허브 작업은 세 가지 보안 클레임에 대 한 허용 비슷한 tooother 엔터티: 수신 대기, 전송 및 관리 합니다.

| 클레임 | 설명 | 허용되는 연산 |
| --- | --- | --- |
| 수신 대기 |단일 등록 만들기/업데이트, 읽기 및 삭제 |등록 만들기/업데이트<br><br>등록 읽기<br><br>핸들에 대한 모든 등록 읽기<br><br>등록 삭제 |
| 보내기 |보낼 메시지 toohello 알림 허브 |메시지 보내기 |
| 관리 |알림 허브의 CRUD(PNS 자격 증명 및 보안 키 업데이트 포함) 및 태그 기준 등록 읽기 |알림 허브 만들기/업데이트/읽기/삭제<br><br>태그별 등록 읽기 |

알림 허브와 Microsoft Azure 액세스 제어 토큰 및 hello 알림 허브에서 직접 구성한 공유 키를 사용 하 여 생성 한 서명 토큰을 부여 하는 클레임을 수락 합니다.

