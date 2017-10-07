---
title: "aaaSecure 앱 및 Azure RemoteApp에서 리소스 | Microsoft Docs"
description: "자세한 방법을 toolock 앱 및 Azure RemoteApp의 리소스"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 26325826e92855a12a0087f19a3e32cbe1116449
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Azure RemoteApp의 앱 및 리소스 보호
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp 사용자 통해 액세스 toocentrally 관리 하는 Windows 앱 사용자가 수 및 작업할 수 없는 제어할 수 있습니다.  Hello 사용자가 원하는 toocontrol hello 사용자 액세스는 관리 되지 않는 장치 (예: 자신의 개인 Macbook)에서 연결 또는 발생할 때 특히 유용 합니다.

예를 들어 사용자 인증에 대 한 Active Directory를 사용 하는 경우 두려는 tooprevent에서 데이터를 앱 외부로 복사에서 데이터를 복사 원격 데스크톱 그룹 정책 tooblock 사용자가 구성할 수 있습니다.

다른 예로 사용자의 컬렉션에서 특정 앱에 대 한 tooblock 인터넷 액세스 하려는 경우. 블록 컬렉션에 대 한 hello 이미지를 만들 때 액세스 hello 하는 Windows 방화벽 규칙을 만들 수 있습니다.

## <a name="implementation-options"></a>구현 옵션
  다음은 사용할 수 있는 동시에 개별적으로 또는 필요에 따라 hello 키 구현 옵션입니다.

1. RemoteApp 컬렉션이 도메인에 가입 된 모든를 적용할 수 있습니다 [그룹 정책](https://technet.microsoft.com/library/cc725828.aspx) (hello 유휴 상태 및 연결 끊기 시간 제한 정책 설명 hello 예외로 [여기](../azure-subscription-service-limits.md)).
2. 대체 tooGroup (컬렉션 도메인에 가입 되었거나 ad에서 hello 적절 한 권한이 없는) 경우 정책으로 구성할 수 있습니다 [로컬 정책을](https://technet.microsoft.com/library/cc775702.aspx) 템플릿 이미지에 있습니다.  충돌이 발생하는 경우 해당 그룹 정책이 로컬 정책보다 우선합니다.
3. 일부 운영 체제/응용 프로그램 설정은 정책을 통해 구성할 수 있지만 hello를 사용 하 여 레지스트리 키를 통해 있을 수도 [RegEdit 도구](remoteapp-hybridtrouble.md) 템플릿 이미지를 구성 하는 중입니다.
4. 사용할 수 있습니다 [Windows 방화벽](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) hello 앱이 실행 되는 hello 컴퓨터에서 네트워크 액세스 tooand toocontrol 합니다. Hello Url 및 여기에 정의 된 포트를 차단 하지 해야 합니다.
5. 사용할 수 있습니다 [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) toocontrol 응용 프로그램 및 파일의 사용자가 실행할 수 있는 합니다. 예를 들어 숙련 된 사용자 hello에서 사용할 수 있지만 게시 하지 못했습니다. 있는 toorun 응용 프로그램에서 사용한 toocreate hello 컬렉션 이미지 하는 방법을 알아낼 수-이 AppLocker 차단할 수 있습니다.

## <a name="detailed-information"></a>자세한 정보
* 다음 RDS 정책 hello는 가장 유용한 가능성이 toobe:
  * [장치 및 리소스 리디렉션](https://technet.microsoft.com/library/ee791794.aspx)
  * [프린터 리디렉션](https://technet.microsoft.com/library/ee791784.aspx)
  * [프로필](https://technet.microsoft.com/library/ee791865.aspx).
* 구성 리디렉션을 통해 hello RemoteApp PowerShell 모듈을 참고 (표시 된 대로 [여기](remoteapp-redirection.md)) hello 클라이언트 컴퓨터 tooenforce hello 정책에 기반으로 통해 tooenforce hello 정책 보안 hello 기본 목표는 경우 해야 하므로 템플릿 이미지에 대 한 로컬 정책 hello 또는 그룹 정책을 통해 합니다.
* [Windows Server 2012 R2 정책](https://technet.microsoft.com/library/hh831791.aspx)
* [Office 2013 정책을](https://technet.microsoft.com/library/cc178969.aspx) (포함 하 여 [어떻게 toocustomize hello Office 도구 모음](https://technet.microsoft.com/library/cc179143.aspx)).

