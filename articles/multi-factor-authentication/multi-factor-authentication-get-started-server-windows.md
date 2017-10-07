---
title: "aaaWindows 인증 및 Azure MFA 서버 | Microsoft Docs"
description: "Windows 인증 및 Azure Multi-factor Authentication 서버를 배포 하는 데 도움이 되는 hello Azure multi-factor authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Windows 인증 및 Azure Multi-Factor Authentication 서버
Hello Azure Multi-factor Authentication 서버 tooenable의 hello Windows 인증 섹션을 사용 하 고 응용 프로그램에 대해 Windows 인증을 구성 합니다. Windows 인증을 설정 하기 전에 hello 염두에서 목록 다음에 유의 하십시오.

* 설치 후에 터미널 서비스 tootake 효과 대 한 Azure Multi-factor Authentication hello를 다시 부팅 합니다.
* 'Azure Multi-factor Authentication 사용자 일치 체크 hello 사용자 목록에 없는 경우 됩니다 수 toolog hello 컴퓨터에 다시 부팅 후 합니다.
* 신뢰할 수 있는 Ip hello 응용 프로그램이 클라이언트 IP hello hello 인증을 제공할 수 있는지 여부에 종속 됩니다. 현재는 터미널 서비스만 지원됩니다.  

> [!NOTE]
> 이 기능은 Windows Server 2012 r 2에서 지원 되는 toosecure 터미널 서비스가 없습니다.

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a>toosecure 응용 프로그램을 Windows 인증을 사용 하 여 hello 절차를 수행 합니다.
1. Azure Multi-factor Authentication 서버 hello hello Windows 인증 아이콘을 클릭 합니다.
   ![Windows 인증](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Hello 확인 **Windows 인증 사용** 확인란을 선택 합니다. 이 상자는 기본적으로 선택되지 않습니다.
3. hello 응용 프로그램 탭 hello 관리자 tooconfigure Windows 인증을 위해 하나 이상의 응용 프로그램을 사용 합니다.
4. 서버 또는 응용 프로그램 select-hello 서버/응용 프로그램을 사용할지를 지정 합니다. **확인**을 클릭합니다.
5. **추가**를 클릭합니다.
6. hello 신뢰할 수 있는 Ip 탭에서는 특정 Ip에서 시작 되는 tooskip Azure Multi-factor Authentication에 대 한 Windows 세션이 있습니다. 예를 들어 직원 hello 응용 프로그램을 사용 하 여 hello 사무실과 집, 경우 hello office에 Azure Multi-factor Authentication 확인용 전화 하지 않으려면를 결정할 수 있습니다. 이 경우 신뢰할 수 있는 Ip 항목으로 hello office 서브넷을 지정 합니다.
7. **추가**를 클릭합니다.
8. 선택 **단일 IP** tooskip 단일 IP 주소를 원하는 경우.
9. 선택 **IP 범위** tooskip 전체 IP 범위를 넣으면 됩니다. 예 10.63.193.1-10.63.193.100.
10. 선택 **서브넷** 원하는 경우 toospecify Ip 범위 서브넷 표기법을 사용 합니다. Hello 서브넷 시작 IP 주소를 입력 하 고 hello hello 드롭 다운 목록에서 적절 한 넷마스크를 선택 하십시오.
11. **확인**을 클릭합니다.

## <a name="next-steps"></a>다음 단계

- [Azure MFA 서버에 대한 타사 VPN 어플라이언스 구성](multi-factor-authentication-advanced-vpn-configurations.md)

- [Azure MFA에 대 한 hello NPS 확장으로 기존 인증 인프라를 확장 합니다.](multi-factor-authentication-nps-extension.md)
