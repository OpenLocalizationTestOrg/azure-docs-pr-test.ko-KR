---
title: "Azure API 관리에서 사용자 계정을 관리하는 방법 | Microsoft Docs"
description: "Azure API 관리에서 사용자를 만들거나 초대하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d3a50f6d22cbf1797f580078bc0d2cc9cefe5064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a>Azure API 관리에서 사용자 계정을 관리하는 방법
API 관리에서 개발자는 API 관리 사용을 공개하는 API의 사용자입니다. 이 가이드에서는 개발자를 만들고, 개발자가 API 관리 인스턴스로 사용 가능하도록 설정된 API 및 제품을 사용할 수 있도록 초대하는 방법을 보여 줍니다. 프로그래밍 방식으로 사용자 계정 관리에 대한 내용은 [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) 참조에서 [사용자 엔터티](https://msdn.microsoft.com/library/azure/dn776330.aspx) 설명서를 참조하세요.

## <a name="create-developer"> </a>새 개발자 만들기
새 개발자를 만들려면 API 관리 서비스에 대해 Azure Portal에서 **게시자 포털**을 클릭합니다. API 관리 게시자 포털로 이동됩니다. 아직 API Management 서비스 인스턴스를 만들지 않은 경우 [Azure API Management 시작][Get started with Azure API Management] 자습서의 [API Management 서비스 인스턴스 만들기][Create an API Management service instance]를 참조하세요.

![게시자 포털][api-management-management-console]

왼쪽의 **API Management** 메뉴에서 **사용자**를 클릭한 다음 **사용자 추가**를 클릭합니다.

![개발자 만들기][api-management-create-developer]

새 개발자에 대한 **메일**, **암호** 및 **이름**을 입력하고 **저장**을 클릭합니다.

![개발자 만들기][api-management-add-new-user]

기본적으로 새로 만든 개발자 계정은 **활성**이며, **개발자** 그룹과 연결됩니다.

![새 개발자][api-management-new-developer]

**활성** 상태의 개발자 계정은 구독하는 모든 API에 액세스하는 데 사용할 수 있습니다. 새로 만든 개발자와 추가 그룹을 연결하려면 [그룹과 개발자를 연결하는 방법][How to associate groups with developers]을 참조하세요.

## <a name="invite-developer"> </a>개발자 초대
개발자를 초대하려면 왼쪽의 **API Management** 메뉴에서 **사용자**를 클릭한 다음 **사용자 초대**를 클릭합니다.

![개발자 초대][api-management-invite-developer]

개발자의 이름 및 메일 주소를 입력하고 **초대**를 클릭합니다.

![개발자 초대][api-management-invite-developer-window]

확인 메시지가 표시되지만 새로 초대한 개발자는 해당 개발자가 초대를 허용할 때까지 목록에 나타나지 않습니다. 

![초대 확인][api-management-invite-developer-confirmation]

개발자를 초대하면 메일이 개발자에게 전송됩니다. 이 메일은 템플릿을 사용하여 생성되며 사용자 지정 가능합니다. 자세한 내용은 [메일 템플릿 구성][Configure email templates]을 참조하세요.

초대가 허용되면 계정이 활성 상태가 됩니다.

## <a name="block-developer"> </a> 개발자 계정 비활성화 또는 다시 활성화
기본적으로, 새로 만들거나 초대한 개발자 계정은 **활성**상태가 됩니다. 개발자 계정을 비활성화하려면 **차단**을 클릭합니다. 차단된 개발자 계정을 다시 활성화하려면 **활성화**를 클릭합니다. 차단된 개발자 계정에서는 개발자 포털에 액세스하거나 어떤 API도 호출할 수 없습니다. 사용자 계정을 삭제하려면 **삭제**를 클릭합니다.

![개발자 차단][api-management-new-developer]

## <a name="reset-a-user-password"></a>사용자 암호 다시 설정
사용자 계정에 대한 암호를 재설정하려면 계정 이름을 클릭합니다.

![암호 재설정][api-management-view-developer]

**암호 재설정** 을 클릭하면 사용자에게 암호를 재설정할 수 있는 링크가 전송됩니다.

![암호 재설정][api-management-reset-password]

프로그래밍 방식으로 사용자 계정에 대해 작업하려면 [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) 참조에서 [사용자 엔터티](https://msdn.microsoft.com/library/azure/dn776330.aspx) 설명서를 참조하세요. 사용자 계정 암호를 특정 값으로 다시 설정하려면 [사용자 업데이트](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) 작업을 사용하여 원하는 암호를 지정할 수 있습니다.

## <a name="pending-verification"></a>확인 보류 중
![확인 보류 중][api-management-pending-verification]

## <a name="next-steps"> </a>다음 단계
개발자 계정이 생성된 후에는 계정과 역할을 연결하고 해당 계정으로 제품 및 API를 구독할 수 있습니다. 자세한 내용은 [그룹을 만들고 사용하는 방법][How to create and use groups]을 참조하세요.

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
