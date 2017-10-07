---
title: "사용 하 여 aaaManaging 장치 hello Azure 포털-미리 보기 | Microsoft Docs"
description: "Toouse Azure 포털 toomanage 장치 hello 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a>Azure 포털 hello-미리 보기를 사용 하 여 장치 관리

>[!NOTE]
>이 기능은 현재 공개 미리 보기로 제공되고 있습니다. Toorevert 준비 하거나 변경 내용을 모두 제거 합니다. hello 기능은 공개 미리 보기 기간 동안 모든 Azure Active Directory (Azure AD) 구독에서 사용할 수 있습니다. 그러나 hello 기능이 일반 공급 되 면 hello 기능의 일부 측면 Azure Active Directory premium 구독에 필요할 수 있습니다.


Azure AD(Active Directory)의 장치 관리를 사용하면 보안 및 규정 준수에 대한 표준을 충족하는 장치에서 사용자 리소스에 액세스할 수 있습니다. 

항목 내용:

- Hello에 익숙한 것으로 가정 [Azure Active Directory의 toodevice 관리 소개](device-management-introduction.md)

- Azure 포털을 hello를 사용 하 여 장치를 관리 하는 방법에 대 한 정보를 제공 합니다.


hello Azure 포털에서에서 장치 toomanage 해야 tooclick **장치** hello에 **관리** hello hello 섹션 **Azure Active Directory** 블레이드 합니다.

![Intune 장치 관리](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a>장치 설정 구성

toomanage toobe 필요한 hello Azure 포털을 사용 하 여 장치를 등록 하거나 tooAzure AD 가입 하십시오. 관리자로 서 등록 하 고 hello 장치 설정을 구성 하 여 장치를 가입 hello 과정을 미세 조정할 수 있습니다.

![Intune 장치 관리](./media/device-management-azure-portal/22.png)


hello 장치 설정 블레이드에서 tooconfigure가 있습니다.

- **사용자가 장치 tooAzure AD에 조인할 수 있습니다.** -이 설정 장치 tooAzure AD 가입할 수 있는 tooselect hello 사용자가 사용 합니다. hello 기본값은 **모든**합니다.

- **Azure AD에 추가 하는 로컬 관리자가 가입 장치** -장치에 대 한 로컬 관리자 권한을 hello 사용자를 선택할 수 있습니다. 여기에 추가 하는 사용자가 toohello 추가 *장치 관리자* Azure ad에서 역할입니다. Azure AD의 전역 관리자 및 장치 소유자에게는 기본적으로 로컬 관리자 권한이 부여됩니다. 이 옵션에는 Azure AD Premium 또는 Enterprise Mobility Suite (EMS) hello 등의 제품을 통해 사용할 수 있는 premium edition 기능입니다. 

- **Azure ad 사용자가 장치를 등록할 수 있습니다** -tooconfigure 설정을 tooallow 장치 toobe이 Azure AD에 등록 해야 합니다. 선택 하는 경우 **None**, Azure AD 조인 되지 않은 tooregister 또는 Azure AD 조인 하이브리드 장치 허용 되지 않습니다. Office 365용 Microsoft Intune 또는 MDM(모바일 장치 관리)에 등록하려면 먼저 장치를 등록해야 합니다. 이러한 서비스 중 하나를 구성한 경우 **모두**가 선택되고 **없음**은 사용할 수 없습니다.

- **Multi-factor Auth toojoin 장치가 필요** -두 번째 인증 단계 자신의 장치 tooAzure AD toojoin 사용자가 필요한 tooprovide 있는지 여부를 선택할 수 있습니다. hello 기본값은 **아니요**합니다. 그러나 장치를 등록하는 경우 Multi-Factor Authentication을 사용하는 것이 좋습니다. 이 서비스에 대해 multi-factor authentication을 활성화 하기 전에 multi-factor authentication 자신의 장치를 등록 하는 hello 사용자에 대해 구성 된 확인 해야 합니다. 다양한 Azure Multi-Factor Authentication 서비스에 대한 자세한 내용은 [Azure Multi-Factor Authentication 시작](../multi-factor-authentication/multi-factor-authentication-get-started.md)을 참조하세요. 

- **최대 장치 수가** -이 설정을 사용 하면 Azure AD에서 사용자가 장치의 tooselect hello 최대 수입니다. 사용자가이 할당량에 도달 하면 하나까지 수 tooadd 추가 장치 수 없습니다는 또는 이상의 hello 기존 장치가 제거 됩니다. hello 장치 따옴표는 모든 장치는 Azure AD 조인 또는 현재 등록 된 Azure AD에 대해 계산 됩니다. hello 기본값은 **20**합니다.

- **사용자가 장치에서 설정 및 응용 프로그램 데이터를 동기화가** -기본적으로이 설정은 너무**NONE**합니다. 특정 사용자 또는 그룹 중 하나 또는 모두를 선택 하면 해당 Windows 10 장치에서 hello 사용자의 설정 및 응용 프로그램 데이터 toosync 있습니다. Windows 10에서 동기화가 작동되는 방식에 대해 자세히 알아봅니다.
이 옵션에는 Azure AD Premium 또는 Enterprise Mobility Suite (EMS) hello 등의 제품을 통해 사용할 수 있는 프리미엄 기능입니다.
 
    ![Intune 장치 관리](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a>장치 찾기

관리자로 서 hello Azure 포털의에서 두 가지 옵션이 있습니다 toolocate 등록 하 고 장치를 가입 합니다.

- **모든 장치** hello에 **관리** hello 섹션 **장치** 블레이드  

    ![모든 장치](./media/device-management-azure-portal/41.png)


- **장치** hello에 **관리** 섹션은 **사용자** 블레이드
 
    ![모든 장치](./media/device-management-azure-portal/43.png)



두 옵션으로 얻을 수 있습니다 tooa 보기입니다.


- 필터로 hello 표시 이름을 사용 하 여 장치에 대 한 toosearch가 있습니다.

- 등록 및 조인된 장치의 자세한 개요를 제공합니다.

- 일반 장치 관리 작업을 tooperform 있습니다.
   

![모든 장치](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a>장치 관리 작업

관리자로 서 관리할 수 있습니다 hello 등록 또는 장치를 가입 합니다. 이 섹션에서는 일반 장치 관리 작업에 대한 정보를 제공합니다.


**Intune 장치 관리** - Intune 관리자인 경우 **Microsoft Intune**으로 표시된 장치를 관리할 수 있습니다. 관리자는 추가 장치를 볼 수 있습니다. 

![Intune 장치 관리](./media/device-management-azure-portal/31.png)


**Azure AD 장치 사용/사용 안 함**

tooenable 또는 사용 안 함 장치를 Azure AD에서 toobe 전역 관리자 필요 합니다. 장치를 사용하지 않도록 설정하면 장치에서 Azure AD 리소스에 액세스할 수 없게 됩니다.  눌러 수 toodisable hello 장치 *...* 자세한 내용은 hello 장치를 클릭 합니다.

 
![Intune 장치 관리](./media/device-management-azure-portal/33.png)

Hello에 hello 상태를 변경 하는 장치를 사용 하지 않도록 설정 **ENABLED** 열 너무**아니요**합니다.

![장치 사용 안 함](./media/device-management-azure-portal/32.png)


**Azure AD 장치를 삭제** -toodelete 장치를 Azure AD에서 toobe 전역 관리자를 사용 해야 합니다.  
장치 삭제:
 
- 장치에서 Azure AD 리소스에 액세스할 수 없게 됩니다. 

- 모든 예를 들어 연결 된 toohello 장치 된 세부 사항, Windows 장치에 대 한 BitLocker 키를 제거 합니다.  

- 복구할 수 없으며, 반드시 필요한 경우가 아니면 권장되지 않는 작업을 나타냅니다.

장치를 다른 관리 기관 (예: Microsoft Intune)에 의해 관리 되는 경우 해당 hello 장치 초기화 / Azure AD에서 hello 장치를 삭제 하기 전에 사용 중지 된에 있는지 확인 하십시오.

“…”를 선택하여 toodelete hello 장치 또는 추가 세부 정보에 대 한 hello 장치를 클릭
 
![장치 삭제](./media/device-management-azure-portal/34.png)


**보거나 장치 ID를 복사** -hello 장치 또는 PowerShell을 사용 하 여 문제를 해결 하는 동안에 장치 ID tooverify hello 장치 ID 세부 정보를 사용할 수 있습니다. tooaccess hello 복사 옵션을 hello 장치를 클릭 합니다.

![장치 ID 보기](./media/device-management-azure-portal/35.png)
  

**보거나 BitLocker 키를 복사** -관리자가 볼 수 있으며 복사 hello BitLocker 키 toohelp 사용자 toorecover의 암호화 된 드라이브입니다. 이러한 키는 암호화되고 해당 키가 Azure AD에 저장된 Windows 장치에 대해서만 사용할 수 있습니다. Hello 장치의 세부 정보에 액세스할 때이 키를 복사할 수 있습니다.
 
![BitLocker 키 보기](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a>감사 로그


hello 장치 활동은 hello 활동 로그를 통해 사용할 수 있습니다. 이 작업 트리거 hello 장치 등록 서비스에서 또는 hello 사용자가 포함 됩니다.

- 장치 만들기 및 hello 장치 소유자/사용자를 추가 합니다.

- Toodevice 설정을 변경 합니다.

- 장치 삭제 또는 업데이트 등의 장치 작업
 
데이터 감사 하 여 항목 지점 toohello는 **감사 로그** hello에 **활동** hello 섹션 **장치* 블레이드입니다.

![감사 로그](./media/device-management-azure-portal/61.png)


감사 로그에는 다음 항목을 보여 주는 기본 목록 보기가 있습니다.

- hello 발생의 hello 날짜 및 시간

- hello 대상

- 초기자 hello / 행위자 (누가) 활동

- hello 활동 (작업)

![감사 로그](./media/device-management-azure-portal/63.png)

클릭 하 여 hello 목록 보기를 사용자 지정할 수 있습니다 **열** hello 도구 모음에서입니다.
 
![감사 로그](./media/device-management-azure-portal/64.png)


hello 아래로 toonarrow 데이터 tooa 수준 수에 대 한 작동을 필터링 할 수 필드를 다음 hello를 사용 하 여 hello 감사 데이터를 보고.

- 범주
- 활동 리소스 종류
- 작업
- 날짜 범위
- 대상
- 초기자(작업자)

또한 toohello 필터를 검색할 수 있습니다 특정 항목에 대 한.

![감사 로그](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a>다음 단계

* [Azure Active Directory의 toodevice 관리 소개](device-management-introduction.md)



