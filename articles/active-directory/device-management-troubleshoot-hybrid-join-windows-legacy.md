---
title: "aaaTroubleshooting 하이브리드 Azure Active Directory 가입 하위 수준 장치 | Microsoft Docs"
description: "하위 수준 장치에 조인된 하이브리드 Azure Active Directory 문제 해결"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a>하위 수준 장치에 조인된 하이브리드 Azure Active Directory 문제 해결 

이 항목은 적용 가능한 유일한 toohello 다음 장치: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Windows 10 또는 Windows Server 2016의 경우 [Windows 10 및 Windows Server 2016 장치에 조인된 하이브리드 Azure Active Directory 문제 해결](device-management-troubleshoot-hybrid-join-windows-current.md)을 참조하세요.

이 항목에서는 있다고 가정 [구성 된 하이브리드 Azure Active Directory 가입 장치](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello 다음 시나리오:

- 장치 기반 조건부 액세스

- [엔터프라이즈 설정 로밍](active-directory-windows-enterprise-state-roaming-overview.md)

- [비즈니스용 Windows Hello](active-directory-azureadjoin-passport-deployment.md) 





이 항목에서는 문제 해결 방법을 tooresolve 잠재적 문제에 대 한 지침입니다.  

**알아야 할 사항:** 

- 사용자 당 장치의 hello 최대 수는 장치 중심입니다. 예를 들어 경우 *jdoe* 및 *jharnett* 로그인 tooa 장치 별도 등록 (DeviceID) hello에서 각각의 대해 만들어집니다 **사용자** 정보 탭 합니다.  

- 초기 등록 hello / 참가 장치 시도 하는 구성 된 tooperform 로그온 또는 잠금 / 잠금 해제 합니다. 작업 스케줄러 작업에 의해 트리거되는 5분 지연이 있을 수 있습니다. 

- Hello 운영 체제 또는 수동 다시 설치 여러 항목의 hello 사용자 정보 탭 아래에 결과 hello Azure 포털 및 등록 취소 하 고 다시 등록 Azure AD에 새 등록을 만들 수 있습니다. 


## <a name="step-1-retrieve-hello-registration-status"></a>1 단계: hello 등록 상태를 검색 합니다. 

**tooverify hello 등록 상태:**  

1. 관리자 권한으로 명령 프롬프트를 열고 hello 

2. `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`를 입력합니다.

이 명령은 hello 조인 상태에 대 한 자세한 정보를 제공 하는 대화 상자를 표시 합니다.

![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a>2 단계: hello 하이브리드 Azure AD 조인 상태를 평가 합니다. 

Hello 하이브리드 Azure AD 조인 성공 하지 못한 경우 hello 대화 상자에는 발생 한 hello 문제에 대 한 세부 정보와 함께 제공 합니다.

**hello 가장 일반적인 사항은 다음과 같습니다.**

- 잘못 구성된 AD FS 또는 Azure AD

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- 도메인 사용자로 로그온되지 않음

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- 할당량에 도달함

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- hello 서비스가 응답 하지 않습니다. 

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

Hello 이벤트 로그에 hello 상태 정보를 찾을 수도 **응용 프로그램 및 서비스 Log\Microsoft 작업 공간 연결**합니다.
  
**실패 한 하이브리드 Azure AD 조인에 대 한 hello 가장 일반적인 원인은 다음과 같습니다.** 

- 컴퓨터가 켜져 hello 조직의 내부 네트워크 또는 VPN 연결 tooan 없이 온-프레미스 AD 도메인 컨트롤러입니다.

- 로컬 컴퓨터 계정 사용 하 여 tooyour 컴퓨터에 기록 됩니다. 

- 서비스 구성 문제: 

  - hello 페더레이션 서버가 있는 상태 구성된 toosupport **WIAORMULTIAUTHN**합니다. 

  - Azure AD에서 hello 컴퓨터 속한 hello AD 포리스트에 tooyour 확인 된 도메인 이름을 가리키는 서비스 연결 지점 개체가 있습니다.

  - 사용자 장치 hello 제한에 도달 했습니다. 

## <a name="next-steps"></a>다음 단계

질문에 대 한 참조 hello [장치 관리 FAQ](device-management-faq.md)  
