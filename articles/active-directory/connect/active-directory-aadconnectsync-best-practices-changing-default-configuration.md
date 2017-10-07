---
title: "Azure AD Connect 동기화: hello 기본 구성 변경 | Microsoft Docs"
description: "Azure AD Connect sync의 hello 기본 구성을 변경 하는 유용한 정보를 제공 합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: aa05e935edd02c49c3c3fdc198b854f50327847c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-hello-default-configuration"></a>Azure AD Connect 동기화: hello 기본 구성 변경에 대 한 유용한 정보
hello이이 항목의 목적은 toodescribe 지원 하 고 변경 내용을 tooAzure AD Connect 동기화를 지원 되지 않습니다.

Azure AD Connect에서 만든 hello 구성은 Azure AD와 온-프레미스 Active Directory를 동기화 하는 대부분의 환경에 대 한 "있는 그대로" 작동 합니다. 그러나 일부 경우에는 일부 변경 내용이 tooa 구성 toosatisfy 특정 필요 필요한 tooapply 또는 요구 사항

## <a name="changes-toohello-service-account"></a>변경 내용 toohello 서비스 계정
Azure AD Connect 동기화 hello 설치 마법사가 만든 서비스 계정에서 실행 중입니다. 이 서비스 계정은 동기화에서 사용 하는 hello 암호화 키 toohello 데이터베이스를 보유 합니다. 127 자 긴 암호를 사용 하 여 만든이 및 toonot에 설정 된 hello 암호가 만료 됩니다.

* **지원 되지 않는** toochange 또는 리셋 hello hello 서비스 계정의 암호입니다. 이렇게 hello 암호화 키를 제거 하 고 hello 서비스 데이터베이스가 아닙니다. 수 tooaccess hello에 대 한 수 toostart 합니다.

## <a name="changes-toohello-scheduler"></a>변경 내용 toohello 스케줄러
Hello 릴리스 빌드에서 1.1 부터는 (2016 년 2 월) hello를 구성할 수 있습니다 [스케줄러](active-directory-aadconnectsync-feature-scheduler.md) toohave 서로 다른 동기화 주기를 hello 기본값과 30 분입니다.

## <a name="changes-toosynchronization-rules"></a>변경 내용 tooSynchronization 규칙
hello 설치 마법사는 hello 가장 일반적인 시나리오에 대 한 toowork 해야 하는 구성을 제공 합니다. Toomake toohello 구성 변경 해야 할 경우에 toostill가 지원 되는 구성 이러한 규칙을 따라야 합니다.

* 있습니다 수 [특성 흐름 변경](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) hello 기본 직접 특성 흐름 사용자 조직에 적합 하지 않은 경우.
* 너무 하려는 경우[특성을 전달 하지](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) 이 시나리오에 대 한 규칙 toocreate 해야 Azure AD에서 모든 기존 특성 값을 제거 합니다.
* [원치 않는 동기화 규칙을 사용하지 않습니다](#disable-an-unwanted-sync-rule) . 삭제된 규칙을 업그레이드 중 다시 만듭니다.
* 너무[기본적으로 규칙을 변경할](#change-an-out-of-box-rule), 규칙 및 hello 기본적으로 규칙을 사용 하지 않도록 설정 원래 hello의 복사본을 확인 해야 합니다. 동기화 규칙 편집기 hello 라는 메시지를 표시 하 고 수 있습니다.
* 동기화 규칙 편집기 hello를 사용 하 여 사용자 지정 동기화 규칙을 내보냅니다. hello 편집기 제공으로 사용할 수 있는 PowerShell 스크립트 tooeasily에서에서 다시 재해 복구 시나리오입니다.

> [!WARNING]
> hello 기본 제공 동기화 규칙에는 지문을 보유 합니다. Toothese 규칙 변경 하면 hello 지문은 더 이상와 일치 합니다. Azure AD Connect의 새로운 릴리스가 tooapply 려 할 때 hello 향후에 문제가 발생할 수 있습니다. 이 문서에 설명 되어 변경 내용을 hello 방법만 생성 합니다.

### <a name="disable-an-unwanted-sync-rule"></a>원치 않는 동기화 규칙을 사용하지 않습니다
기본 동기화 규칙을 삭제하지 마십시오. 다음 업그레이드 도중에 다시 만들어집니다.

경우에 따라 hello 설치 마법사에서 토폴로지에 대 한 작동 하지 않는 구성을 발생 했습니다. 예를 들어 계정-리소스 포리스트 토폴로지에서 있지만 hello 계정 포리스트 hello Exchange 스키마에 확장 된 hello 스키마가 있는 경우 Exchange에 대 한 규칙 hello 계정 포리스트 및 hello 리소스 포리스트를 위해 생성 됩니다. 이 경우 toodisable hello 동기화 규칙 Exchange 필요합니다.

![비활성화된 동기화 규칙](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

위의 hello 그림에서 hello 설치 마법사에서에서 발견 되는 Exchange 2003 스키마가 이전 hello 계정 포리스트 합니다. Fabrikam의 환경에서 리소스 포리스트 hello 도입 되기 전에이 스키마 확장이 추가 되었습니다. tooensure hello 이전 Exchange 구현을 없는 특성이 동기화 되는, 표시 된 것 처럼 hello 동기화 규칙을 비활성화 해야 합니다.

### <a name="change-an-out-of-box-rule"></a>기본 규칙을 변경하려면
기본적으로 규칙을 변경 해야 하는 hello 유일한 시간은 toochange hello 조인 규칙을 식별할 때. 특성 흐름 toochange 해야 할 경우 hello 기본 제공 규칙 보다 우선 순위가 높은 동기화 규칙을 만들기 해야 합니다. tooclone 실제로 필요한 규칙은 hello 규칙만 hello **에서 from AD-User Join**합니다. 다른 모든 규칙을 더 높은 우선 순위 규칙으로 덮어쓸 수 있습니다.

Toomake 변경 tooan 기본적으로 규칙을 해야 하는 경우 다음 hello 기본적으로 규칙의 사본을 hello 원래 규칙을 사용 하지 않도록 설정 합니다. Hello 변경 toohello 복제 된 규칙을 확인 합니다. 동기화 규칙 편집기 hello 되어 이러한 단계를 지원 합니다. 기본 규칙을 열면 이 대화 상자가 나타납니다.  
![경고 받은 기본 규칙](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

선택 **예** toocreate hello 규칙의 복사본입니다. 다음 복제 된 규칙 hello 열립니다.  
![복제된 규칙](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)

이 복제 된 규칙에서 모든 필요한 변경 tooscope, 조인 및 변환을 확인 합니다.

## <a name="next-steps"></a>다음 단계
**개요 항목**

* [Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
