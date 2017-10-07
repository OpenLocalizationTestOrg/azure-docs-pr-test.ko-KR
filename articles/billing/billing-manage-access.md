---
title: "역할을 사용 하 여 청구 aaaManage 액세스 tooAzure | Microsoft Docs"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a>역할 기반 액세스 제어를 사용 하 여 Azure에 대 한 액세스 toobilling 정보 관리

Hello 사용자 역할 tooyour 구독을 다음 중 하나를 할당 하 여 팀의 청구 정보 toomembers Azure에 대 한 액세스를 부여할 수 있습니다: 계정 관리자, 서비스 관리자, 공동 관리자, 소유자, 참가자, 판독기 및 청구 판독기입니다. Hello에 대 한 액세스 toobilling 정보를 갖게 됩니다 [Azure 포털](https://portal.azure.com/), hello 사용 [청구 Api](billing-usage-rate-card-overview.md) tooprogrammatically (한 번 옵트인) 송장 및 사용 현황 정보를 얻습니다. 역할을 부여할 수 있는 사람, 역할로 수행할 수 있는 작업에 대한 자세한 내용은 [Azure RBAC의 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.

## <a name="opt-in"></a>추가 사용자 tooaccess 송장 허용

hello 계정 관리자 해야 옵트인 hello를 사용 하 여 [Azure 포털](https://portal.azure.com/) API를 통해 및 다른 사용자에 대 한 액세스 tooinvoices을 허용 합니다.

1. 계정 관리자 hello, hello에서 구독 선택 [구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) Azure 포털에서 합니다.

1. 선택 **송장** 차례로 **tooinvoices 액세스**합니다.

    ![스크린샷은은 toodelegate tooinvoices를 액세스 하는 방법을 보여 줍니다.](./media/billing-manage-access/AA-optin.png)

1. 설정 **에** hello 액세스 뒤에 구독 범위가 지정 된 역할 toodownload 송장 tooallow 사용자 hello 변경 내용을 저장 합니다.

    ![스크린샷은 온-오프 toodelegate 액세스 tooinvoice](./media/billing-manage-access/AA-optinAllow.png)

옵트인 서비스 관리자, 공동 관리자, 소유자, 참가자, 판독기 및 청구 판독기 hello hello Azure 포털에서에서 구독 toodownload PDF 송장에 있습니다. 그러나 2016 년 12 월 보다 오래 된 송장 지금은 사용할 수 있는 유일한 toohello 계정 관리자는.

hello 계정 관리자 전자 메일을 통해 전송 toohave 송장 구성할 수도 있습니다. toolearn 더 참조 [청구서 전자 메일에서 가져올](billing-download-azure-invoice-daily-usage-date.md)합니다.

## <a name="adding-users-toohello-billing-reader-role"></a>사용자가 toohello 청구 읽기 역할 추가

hello 청구 읽기 역할에 Azure 포털에서 읽기 전용 액세스 toosubscription 청구 정보 및 Vm 및 저장소 계정과 같은 없습니다 액세스 tooservices 있습니다. 할당 되지 기능 toomanage Azure hello 하지만 toohello 구독 청구 정보에 액세스 하는 hello 청구 판독기 역할 toosomeone 서비스입니다. 이 역할은 Azure 구독에 대해 재무 및 비용 관리만 수행하는 조직의 사용자에게 적합합니다.

1. Hello에서 구독을 선택 [구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) Azure 포털에서 합니다.

1. **Access Control(IAM)**를 선택하고 **추가**를 클릭합니다.

    ![스크린샷은은 hello 구독 블레이드에서 IAM를 보여 줍니다.](./media/billing-manage-access/select-iam.PNG)

1. 선택 **청구 판독기** hello에 **역할 선택** 페이지.

    ![스크린샷은 hello 팝업 뷰에 청구 판독기](./media/billing-manage-access/select-roles.PNG)

1. 원하는 tooinvite, 다음 클릭 hello 사용자에 대 한 hello 전자 메일을 입력 **확인** toosend hello 초대 합니다.

    ![다른 사람이 tooenter 전자 메일 tooinvite을 보여 주는 스크린샷](./media/billing-manage-access/add-user.PNG)

1. 청구 판독기로의 hello 초대 메일 toolog에 지침을 따르십시오.

    ![Azure 포털에서 볼 수 기능 hello 청구 판독기를 보여 주는 스크린샷](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> hello 청구 판독기 기능은 미리 보기 상태에서 이며 엔터프라이즈 (EA) 구독 또는 비전역 클라우드가 아직 지원 하지 않습니다.

## <a name="adding-users-tooother-roles"></a>사용자가 tooother 역할 추가

소유자 또는 참가자 등의 다른 역할의 사용자는 청구 정보에 액세스할 수만 있고 Azure 서비스에는 액세스할 수 없습니다. 이러한 역할 참조 toomanage [hello 구독 또는 서비스를 관리 하는 Azure 관리자 역할을 추가 또는 변경](billing-add-change-azure-subscription-administrator.md)합니다.

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a>Hello 액세스할 수 있는 사용자 [r e 계정 센터](https://account.windowsazure.com)?

Hello 계정 관리자만 toohello r e 계정 센터에 기록할 수 있습니다. hello 계정 관리자에는 hello 법적 hello 구독 소유자입니다. 기본적으로에 등록 또는 hello Azure 구독을 구입한 hello 사람 표시 되지 않으면 계정 관리자 hello hello [구독 소유권을 전송 된](billing-subscription-transfer.md) toosomebody 다른 합니다. hello 계정 관리자 구독을 만들, 구독 취소, 구독에 대 한 hello 요금 청구서 주소를 hello 구독에 대 한 액세스 정책을 관리 합니다.

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.

여전히 있는 경우 추가 질문의 대답 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.
