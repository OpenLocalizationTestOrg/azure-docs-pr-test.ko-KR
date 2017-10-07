---
title: "Azure AD Connect 동기화: AD 휴지통 사용 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect와 AD 휴지통 기능의 hello 사용을 권장합니다."
services: active-directory
keywords: "AD 휴지통, 실수로 삭제, 원본 앵커"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a>Azure AD Connect 동기화: AD 휴지통 사용
동기화 된 tooAzure AD는 해당 온-프레미스 Active 디렉터리에 대해 hello AD 휴지통 기능을 사용 하는 것이 좋습니다. 

온-프레미스를 실수로 삭제 한 경우 AD 사용자 개체 및 Azure AD hello 기능을 사용 하 고, Azure AD 사용자 개체를 해당 하는 hello 복원 복원 합니다.  Hello AD 휴지통을 활성화 기능에 대 한 정보를 참조 tooarticle [삭제 된 Active Directory 개체 복원에 대 한 시나리오를 개요](https://technet.microsoft.com/library/dd379542.aspx)합니다.

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a>휴지통 hello AD 사용의 이점
이 기능은 hello 다음을 수행 하 여 Azure AD 사용자 개체를 복원 하 여 확인할 수 있습니다.

* 온-프레미스를 실수로 삭제 한 경우 hello 해당 Azure AD 사용자 개체에서에서 삭제 됩니다. hello 다음 동기화 주기 AD 사용자 개체입니다. 기본적으로 Azure AD 일시 삭제 된 상태에서 Azure AD 사용자 개체를 삭제 하는 hello 30 일 동안 유지합니다.

* 온-프레미스에 있는 경우 AD 휴지통 기능이 활성화 되어 있으면 삭제 하는 hello 복원할 수 있습니다 온-프레미스 AD 사용자 개체의 원본 앵커 값을 변경 하지 않고 있습니다. Hello 온-프레미스를 복구 하는 경우 AD 사용자 개체는 동기화 tooAzure AD, Azure AD는 복원 hello 일시 삭제 된 해당 Azure AD 사용자 개체입니다. 원본 앵커 특성에 대 한 내용은 tooarticle 참조 [Azure AD Connect: 개념 디자인](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor)합니다.

* 온-프레미스 없는 경우 AD 휴지통 기능 활성화를 필요한 toocreate AD 사용자 개체 tooreplace hello 삭제 된 개체 일 수 있습니다. Azure AD Connect 동기화 서비스가 구성 된 toouse 시스템에서 생성 된 AD 특성 (예: ObjectGuid) hello 원본 앵커 특성에 대 한 이면 hello 새로 만든된 AD 사용자 개체 됩니다 하지가 hello 동일한 원본 앵커 값 hello AD 사용자 개체를 삭제 합니다. Azure AD에서는 새 hello 새로 만든된 AD 사용자 개체 이면 동기화 된 tooAzure AD hello 일시 삭제 된 Azure AD 사용자 개체를 복원 하는 대신 Azure AD 사용자 개체입니다.

> [!NOTE]
> 기본적으로 Azure AD는 Azure AD 사용자 개체를 영구적으로 삭제하기 전에 30일 동안 일시 삭제 상태로 유지합니다. 그러나 관리자가 이러한 개체의 hello 삭제를 가속화할 수 있습니다. Hello 개체가 영구적으로 삭제 되 면 더 이상 복구할 수, 경우에도 온-프레미스 AD 휴지통 기능을 사용할 수 없습니다.



## <a name="next-steps"></a>다음 단계
**개요 항목**

* [Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정](active-directory-aadconnectsync-whatis.md)

* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
