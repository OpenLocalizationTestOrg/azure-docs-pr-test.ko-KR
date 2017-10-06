---
title: "aaaWhat 그룹 기반 Azure Active Directory에서 라이선스는? | Microsoft Docs"
description: "Azure Active Directory 그룹 기반 라이선스, 작동 방법 및 모범 사례에 대한 설명"
services: active-directory
keywords: "Azure AD 라이선스"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/29/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 11647de6b76022cd2393751fcafc67ce671aeba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a>Azure Active Directory에서 그룹 기반 라이선스 기본

Office 365, Enterprise Mobility + Security, Dynamics CRM 및 기타 유사한 제품과 같은 Microsoft 유료 클라우드 서비스를 사용하려면 라이선스가 필요합니다. 이러한 라이선스를이 갖고 tooeach 해야 사용자에 게 액세스 toothese 서비스 할당 됩니다. toomanage 라이선스 관리자 사용 하 여 hello 관리 포털 (Office 또는 Azure) 및 PowerShell cmdlet 중 하나입니다. Azure Active Directory (Azure AD)는 모든 Microsoft 클라우드 서비스에 대 한 id 관리를 지 원하는 hello 기본 인프라입니다. Azure AD는 사용자에 대한 라이선스 할당 상태에 대한 정보를 저장합니다.

지금까지 대규모 관리를 어렵게 만들 수 있는 hello 개별 사용자 수준에서 라이선스만 지정할 수 있습니다. 예를 들어 tooadd / 제거 사용자 라이선스 조직 또는 부서의 사용자가 조인 하거나 그대로 두고 hello와 같은 조직 변경 내용에 따라 관리자 종종 작성 해야 복잡 한 PowerShell 스크립트입니다. 이 스크립트에서는 toohello 클라우드 서비스 개별 호출 합니다.

tooaddress 문제를 제기 하는 것, Azure AD는 이제 그룹 기반 라이선스를 포함합니다. 하나 이상의 제품 라이선스 tooa 그룹을 할당할 수 있습니다. Azure AD는 hello 라이선스 hello 그룹의 구성원 tooall 할당 되어 있는지 확인 합니다. Hello 그룹에 참가 하는 모든 새 멤버로 hello 적절 한 라이선스를 할당 됩니다. Hello 그룹을 벗어날 때 해당 라이선스 제거 됩니다. 따라서 hello 조직 및 사용자 당 기준 부서 구조에서 PowerShell tooreflect 변경 내용을 통해 라이선스 관리를 자동화 하기 위한 hello 필요를 하지 않습니다.

## <a name="features"></a>기능

그룹 기반 라이선스의 주요 기능 hello 다음과 같습니다.

- 라이선스는 Azure AD에서 보안 그룹 tooany 할당할 수 있습니다. Azure AD Connect를 사용하여 보안 그룹을 온-프레미스에서 동기화할 수 있습니다. (클라우드 전용 그룹 라고도 함)는 Azure AD에서 직접 또는 Azure AD hello 동적 그룹 기능을 통해 자동으로 보안 그룹을 만들 수도 있습니다.

- 제품 라이선스는 tooa 그룹에 할당 된 경우 관리자에 게 hello 제품에 하나 이상의 서비스 계획을 비활성화할 수 있습니다. 일반적으로이 hello 조직 없을 때 아직 준비 toostart 제품에 포함 된 서비스를 사용 하 여 수행 됩니다. 예를 들어 관리자에 게 Office 365 tooa 부서를 할당 하지만 hello Yammer 서비스를 일시적으로 해제 될 수 있습니다.

- 사용자 수준 라이선스를 필요로 하는 모든 Microsoft Clouds Services는 지원됩니다. 여기에는 모든 Office 365 제품, Enterprise Mobility + Security 및 Dynamics CRM이 포함됩니다.

- 현재를 사용할 때만 사용할 수는 그룹 기반 라이선스 [Azure 포털 hello](https://portal.azure.com)합니다. 주로 사용자 및 그룹 관리, hello Office 365 포털에 대 한 다른 관리 포털을 사용 하는 경우 지금 toodo를 계속할 수 있습니다. 하지만 hello Azure 포털 toomanage 라이선스 그룹 수준에서 사용 해야 합니다.

- Azure AD는 그룹 멤버 자격 변경으로 인해 발생하는 라이선스 수정을 자동으로 관리합니다. 일반적으로 라이선스 수정은 멤버 자격 변경 후 수분 내에 효과가 발생합니다.

- 사용자는 지정된 라이선스 정책을 사용하는 여러 그룹의 멤버가 될 수 있습니다. 또한 사용자는 그룹 외부에서 직접 할당된 일부 라이선스를 보유할 수도 있습니다. 사용자 상태를 생성 하는 hello에 모든 할당 된 제품 및 서비스 라이선스의 조합입니다.

- 경우에 따라 라이선스 tooa 사용자를 할당할 수 없습니다. 예를 들어 없을 수도 있습니다 사용할 수 있는 충분 한 라이선스 hello 테 넌 트에서 또는 충돌 하는 서비스 수 배정 된 hello에서 동일한 시간입니다. 관리자가 사용자를 Azure AD 완벽 하 게 처리할 수 라이선스 그룹에 대 한 액세스 tooinformation 있습니다. 그런 다음 해당 정보에 따라 수정 작업을 수행할 수 있습니다.

- 공개 미리 보기 동안 Azure AD Basic 또는 Premium edition에 대 한 유료 또는 평가판 구독의 hello 테 넌 트 toouse 그룹 기반의 라이선스 관리 필요 합니다.

## <a name="next-steps"></a>다음 단계

toolearn 그룹 기반의 라이선스를 통해 라이선스가 관리에 대 한 다른 시나리오에 대 한 참조.

* [Azure Active Directory에서 라이선스 시작](active-directory-licensing-get-started-azure-portal.md)
* [Azure Active Directory에서 tooa 그룹 라이선스 할당](active-directory-licensing-group-assignment-azure-portal.md)
* [Azure Active Directory에서 그룹에 대한 라이선스 문제 식별 및 해결](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Toomigrate 개별 toogroup 기반 라이선스 Azure Active Directory에서 사용자가 사용이 허가 된 방법](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory 그룹 기반 라이선스 추가 시나리오](active-directory-licensing-group-advanced.md)
