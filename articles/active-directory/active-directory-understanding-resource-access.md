---
title: "Azure에서 리소스 액세스 aaaUnderstanding | Microsoft Docs"
description: "이 항목에서는 구독 관리자가 toocontrol 리소스 액세스를 사용 하 여 hello에 대 한 개념을 설명 전체 Azure 포털"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a>Azure의 리소스 액세스 이해
> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. hello Azure 포털에서 제공 [역할 기반 액세스 제어](role-based-access-control-configure.md) Azure 리소스를 보다 정확 하 게 관리할 수 있도록 합니다.
> 
> 

2013 년 10 월 hello Azure 클래식 포털 및 서비스 관리 Api는 Azure Active Directory와 통합 되었습니다 tooAzure 리소스에 액세스를 관리 하기 위한 hello 사용자 환경을 개선 하기 위한 순서 toolay hello 기반이에서. Azure Active Directory는 이미 사용자 관리, 온-프레미스 디렉터리 동기화, 다단계 인증 및 응용 프로그램 액세스 제어와 같은 훌륭한 기능을 제공합니다. 물론 이러한 기능들로 Azure 리소스를 전반적으로 관리할 수 있습니다.

Azure의 액세스 제어는 결제 관점에서 시작합니다. hello를 방문 하 여 액세스 하는 Azure 계정의 소유자 hello [Azure 계정 센터](https://account.windowsazure.com/subscriptions)는 hello AA (계정 관리자)입니다. 구독은 결제를 위한 컨테이너 이지만 보안 경계로도 작동 합니다: 각 구독에는 서비스 관리자 (SA) 추가, 제거 및 hello를 사용 하 여 해당 구독의 Azure 리소스를 수정할 수 있는 [Azure클래식포털](https://manage.windowsazure.com/). 새 구독의 기본 SA hello hello AA 이지만 AA hello hello Azure 계정 센터에서에서 hello SA를 변경할 수 있습니다.

<br><br>![Azure 계정][1]

또한 구독은 디렉터리와 연결되어 있습니다. hello 디렉터리 사용자 집합을 정의합니다. Hello 회사 또는 학교 hello 디렉터리를 만든 사용자가 될 수 있습니다. 또는 외부 사용자 (즉, Microsoft 계정) 될 수 있습니다. 구독을 서비스 관리자 (SA) 또는 CA (공동 관리자);에 지정 된 해당 디렉터리 사용자의 하위 집합에서 액세스할 수 있습니다. hello 예외만, 레거시의 이유로 Microsoft 계정 (이전의 Windows Live ID) 할당할 수 있는 SA 또는 CA로 hello 디렉터리에 없는 합니다.

<br><br>![Azure의 액세스 제어][2]

Hello Azure 클래식 포털 내에서 기능을 통해 구독 hello를 사용 하 여 연결 된 Microsoft 계정 toochange hello 디렉터리를 사용 하 여 로그인 하는 Sa **디렉터리 편집** hello 명령을**구독** 페이지 **설정을**합니다. 이 작업은 해당 구독의 hello 액세스 제어에 미치는 영향 메모 합니다.

> [!NOTE]
> hello **디렉터리 편집** hello Azure 클래식 포털을 사용할 수 있는 toousers는 작업을 사용 하 여 로그인 없습니다 또는 학교 계정을 해당 계정이 속한만 toohello 디렉터리 toowhich 로그인 할 수 있으므로 명령입니다.
> 
> 

<br><br>![간단한 사용자 로그인 흐름][3]

Hello 단순한 경우, 조직 (예: Contoso) 청구를 적용 한 액세스 제어를 한 구독 설정 같은 hello 합니다. 즉, hello 디렉터리는 단일 Azure 계정이 소유한 관련된 toosubscriptions입니다. 성공한 로그인 toohello Azure 클래식 포털 하면 사용자는 두 개의 리소스 (hello 앞의 그림에서 주황색으로 표시 된) 컬렉션을 볼:

* 사용자 계정이 있는 디렉터리 (원본 또는 외래 사용자로 추가). Note 로그인에 사용 되는 해당 hello 디렉터리 없는 관련 toothis 계산 하므로 사용자가 로그인 하는 것에 관계 없이 디렉터리가 항상 표시 됩니다.
* 연결 된 로그인에 사용 되는 hello 디렉터리는 hello 사용자 구독의 일부인 리소스 (여기서은 SA 또는 CA) 액세스할 수 있습니다.

<br><br>![여러 구독 및 디렉터리가 있는 사용자][4]

여러 디렉터리에 구독이 있는 사용자 hello 기능 tooswitch hello 현재 컨텍스트가 제공 hello Azure 클래식 포털의 hello 구독 필터를 사용 하 여 합니다. Hello 내부적으로 별도 로그인 tooa 다른 디렉터리에 있는이 발생 하지만이 위해서는 single sign on (SSO) 원활 하 게 사용 합니다.

구독 간에 리소스를 이동하는 등의 작업은 구독의 단일 디렉터리 보기의 결과로 더 어려울 수 있습니다. tooperform hello 리소스 전송 해야 toofirst hello를 사용 하 여 **디렉터리 편집** hello 구독 페이지에서 명령을 **설정을** tooassociate hello 구독 toohello 동일한 디렉터리 .

## <a name="next-steps"></a>다음 단계
* toochange 관리자는 Azure 구독에 대 한 참조 하는 방법에 대해 더 알아봅니다을 toolearn [어떻게 tooadd 또는 변경 Azure 관리자 역할](../billing/billing-add-change-azure-subscription-administrator.md)
* Azure Active Directory tooyour Azure 구독 연결 되는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 구독은 Azure Active Directory와 연결](active-directory-how-subscriptions-associated-directory.md)
* 방법에 대 한 자세한 내용은 Azure AD에서 tooassign 역할 참조 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
