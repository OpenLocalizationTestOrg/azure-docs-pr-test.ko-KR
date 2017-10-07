---
title: "Active Directory 장치 관리 FAQ aaaAzure | Microsoft Docs"
description: "Azure Active Directory 장치 관리 FAQ"
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
ms.openlocfilehash: 000eb6a930187e13cb24cf628793afd06813be23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-device-management-faq"></a>Azure Active Directory 장치 관리 FAQ

**Q: 저는 최근에 hello 장치를 등록합니다. Hello 장치 hello Azure 포털에서에서 내 사용자 정보에서 볼 수 없는 이유**

**A:** 자동 장치 등록 된 도메인에 가입 하는 Windows 10 장치 hello 사용자 정보에 표시 되지 않습니다.
모든 장치 toouse PowerShell toosee 필요. 

만 hello 다음 장치 아래에 나열 됩니다 hello 사용자 정보:

- 엔터프라이즈에 조인되지 않은 모든 개인 장치 
- 모든 비 Windows 10/Windows Server 2016 
- 모든 비 Windows 장치 

---

**Q: 이유를 볼 수 없습니다 hello Azure 포털에서에서 Azure Active Directory에 등록 하는 모든 hello 장치?** 

**A:** 현재,이 방법은 toosee 없습니다 등록 된 모든 장치 hello Azure 포털의에서. Azure PowerShell toofind 모든 장치를 사용할 수 있습니다. 자세한 내용은 참조 hello [Get MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.

--- 

**Q: 어떻게 hello 클라이언트의 어떤 hello 장치 등록 상태를 알 수 있습니까 됩니다?**

**A:** hello 장치 등록 상태에 따라 달라 집니다.

- 어떤 hello 장치가
- 등록된 방법 
- Tooit을 관련 하는 모든 세부 정보입니다. 
 

---

**Q: 이유는 삭제 하려면 장치에 hello Azure 포털 또는 Windows PowerShell을 사용 하 여 여전히 나열 등록?**

**A:** 이것은 의도적인 작동입니다. hello 장치 액세스 tooresources hello 클라우드에서 없을 것입니다. Tooremove hello 장치를 다시 등록 하는 경우 수동 작업이 toobe hello 장치에 대해 수행 해야 합니다. 

온-프레미스 AD 도메인에 조인된 Windows 10 및 Windows Server 2016:

1.  관리자 권한으로 hello 명령 프롬프트를 엽니다.

2.  `dsregcmd.exe /debug /leave`를 입력합니다.

3.  로그 아웃 하 고 다시 hello 장치를 등록 하는 tootrigger hello 예약 된 작업에 로그인 합니다. 

온-프레미스 AD 도메인에 조인된 다른 Windows 플랫폼:

1.  관리자 권한으로 hello 명령 프롬프트를 엽니다.
2.  `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`을 입력합니다.
3.  `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`을 입력합니다.

---

**Q: Azure Portal에서 중복된 장치 항목이 나타나는 이유는 무엇인가요?**

**A:**

-   Windows 10 및 Windows Server 2016, toounjoin 시도 반복된 하 고 다시 가입 하는 경우 동일한 장치 hello에 대 한 중복 된 항목이 있을 수 있습니다. 

-   추가 회사 또는 학교 계정을 사용 하는 각 windows 사용자 hello로 새 장치 레코드를 만들어집니다 추가 회사 또는 학교 계정을 사용한 경우 동일한 장치 이름입니다.

-   다른 Windows 플랫폼에는 온-프레미스 AD 도메인에 가입 된 자동 등록을 사용 하 여 hello와 새 장치 레코드가 만들어집니다 각 도메인 사용자가 hello 장치에 로그온에 대 한 동일한 장치 이름입니다. 

-   초기화 된, AADJ 컴퓨터를 다시 설치 하 고 다시 조인 된 hello 동일한 이름, hello 사용 하 여 다른 레코드로 표시 됩니다 동일한 장치 이름입니다.

---

**Q: 액세스 이유는 사용자 여전히 리소스 hello Azure 포털에서에서 비활성화 하는 장치에서?**

**A:** 적용 revoke toobe tooan 시간 정도 걸릴 수 있습니다.

>[!Note] 
>손실 된 장치에 대 한 사용자가 hello 장치에 액세스할 수 없다고 hello 장치 tooensure 초기화 하는 것이 좋습니다. 자세한 내용은 [Intune에서 관리를 위해 장치 등록](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)을 참조하세요. 


---

**Q: 사용자에게 "여기에서 해당 위치로 이동할 수 없습니다." 메시지가 표시되는 이유는 무엇인가요?**

**A:** 사용자가 차단 되 고이 메시지가 특정 조건부 액세스 규칙 toorequire 특정 장치 상태를 구성 하는 경우 hello 장치 hello 조건을 충족 하지 않습니다. Hello 규칙을 평가 하 고 해당 hello 장치를 확인 하십시오 수 toomeet hello 조건 tooavoid이이 메시지입니다.

---


**Q: hello 장치 레코드 hello Azure 포털에서에서 사용자 정보 hello에서 참조 하 고 hello 클라이언트에 등록 된 hello 상태를 볼 수 있습니다. 조건부 액세스를 사용할 수 있게 제대로 설정되어 있는 것인가요?**

**A:** hello 장치 기록 (deviceID) 및 Azure 포털 hello에 대 한 상태가 hello 클라이언트와 일치 하 고 조건부 액세스에 대 한 평가 조건을 만족 해야 합니다. 자세한 내용은 [Azure Active Directory Device 등록 시작](active-directory-device-registration.md)을 참조하세요.

---

**Q: 왜 "사용자 이름 또는 암호가 올바르지 않습니다." 메시지가 장치에 대 한 I에 막 합류 tooAzure AD?**

**A:** 이 시나리오에 대한 일반적인 이유는 다음과 같습니다.

- 사용자 자격 증명이 더 이상 유효하지 않습니다.

- 컴퓨터가 없습니다 toocommunicate Azure Active Directory에 있습니다. 네트워크 연결 문제가 있는지 확인합니다.

- hello Azure AD Join 필수 조건은 충족 하지 않았습니다. 에 대 한 hello 단계를 따랐는지 확인 하십시오 [기능 tooWindows 10 장치의 Azure Active Directory Join을 통해 클라우드 확장](active-directory-azureadjoin-overview.md)합니다.  

- 페더레이션된 로그인에는 페더레이션 서버 toosupport WS-트러스트 활성 끝점이 필요 합니다. 

---

**Q: 표시 되는 이유 hello "Oops... 오류가 발생 했습니다!" 내 PC를 가입시 키 려 할 때 대화 마십시오?**

**A:** Intune에 Azure Active Directory를 등록했기 때문입니다. 자세한 내용은 [Windows 장치 관리 설정](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment)을 참조하세요.  

---

**PC의 경우 오류 정보 받지 않는 경우 하지만 실패 시도 toojoin 내 q 했습니까?**

**A:** toohello 장치 hello 기본 제공 관리자 계정을 사용 하 여 해당 hello 사용자가 로그인 한 가지 가능한 원인은 됩니다. Azure Active Directory Join toocomplete hello 설치 프로그램을 사용 하기 전에 다른 로컬 계정을 만드세요. 

---

**Q: 자동 장치 등록의 hello 설치에 대 한 지침을 어디서 찾을 수 있습니까?**

**A:** 자세한 지침을 참조 하십시오. [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와](active-directory-conditional-access-automatic-device-registration-setup.md)

---

**Q: 어디에 있습니까 문제 해결 hello 자동 장치 등록에 대 한 내용은?**

**A:** 문제 해결 정보는 다음을 참조하세요.

- [가입 된 컴퓨터 tooAzure AD – Windows 10 및 Windows Server 2016 도메인의 자동 등록 문제 해결](active-directory-device-registration-troubleshoot-windows.md)

- [Windows 하위 클라이언트에 대 한 컴퓨터 tooAzure AD 가입 된 도메인의 자동 등록 문제 해결](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

