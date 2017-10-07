---
title: "aaaTroubleshoot Azure 등록 문제 | Microsoft Docs"
description: "Tootroubleshoot 몇 가지 일반적인 Azure 등록 어떻게 문제에 설명 합니다."
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee649bfc3be7ba1fe2dd863fac09e1c2311d835b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Azure의 등록 문제 해결
Azure에 등록할 수 없는 경우이 문서 tootroubleshoot 일반적인 문제에 hello 팁을 사용 합니다. 등록 시 신용 카드 관련 문제가 발생하면 [Azure 등록 시 사용자의 직불 카드 또는 신용 카드가 거부되었습니다.](billing-credit-card-fails-during-azure-sign-up.md)를 참조하세요. Azure 계정 로그인 할 수 있지만 참조 [내 Azure 구독에 toomanage 로그인 없습니다](billing-cannot-login-subscription.md)합니다.

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>진행 표시줄이 "카드로 ID 확인" 섹션에서 중지됩니다.

브라우저에 대 한 카드로 toocomplete hello id 확인, 타사 쿠키를 허용 되어야 합니다.

![Hello 등록 하는 동안 hanging 카드 섹션별 Id 확인의 스크린 샷](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

다음 단계 tooupdate hello 브라우저의 쿠키 설정을 사용 합니다.

1. Chrome을 사용 하는 경우 너무 이동**설정** > **고급 설정 표시** > **개인 정보 보호** > **콘텐츠 설정**합니다. **타사 쿠키 및 사이트 데이터 차단**을 선택 해제합니다.
2. 가장자리를 사용 하는 경우 너무 이동**설정** > **고급 설정 보기** > **쿠키**합니다. **쿠키를 차단하지 않음**을 선택합니다.
3. Hello Azure 등록 페이지를 새로 고치고 hello 문제가 해결 될 경우를 확인 합니다.
4. Hello 새로 고침 hello 문제를 해결 하지 않은 경우 종료 하 고 브라우저를 다시 시작 후 다시 시도 합니다.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>신용 카드 양식이 내 청구 주소를 지원하지 않습니다.
청구 주소 toobe hello에서 선택한 hello 국가에 필요한 **사용자에 대 한** 섹션. Hello 올바른 국가 선택 했는지 확인 합니다.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>계정 확인을 등록할 때 문자 메시지 또는 호출이 표시되지 않았습니다
빠르게 하기 위하여 이지만, 배달 확인 코드 toobe toofour 분이 걸릴 수도 있습니다. hello 전화 번호 확인을 위한 입력 hello 계정에 대 한 연락처 숫자로 저장 되지 않습니다.

다음은 몇 가지 추가 팁입니다.
* Hello 전화 확인 프로세스에 대 한 VOIP 전화 번호를 사용할 수 없습니다.
* 다시 확인 hello 전화 번호를 비롯 하 여 hello 드롭다운 메뉴에서 선택한 hello 국가 코드를 입력 합니다.
* 휴대폰 문자 메시지 (SMS)를 받지 못하면, 시도 hello **내게 전화 걸기** 옵션입니다.
* 전화가 미국 기반 번호에서 전화 또는 SMS 메시지를 받을 수 있는지 확인합니다.

Hello 문자 메시지 또는 전화 통화를 가져오는 경우 hello 텍스트 상자에 수신 하는 코드를 입력 합니다.

## <a name="credit-card-declined-or-not-accepted"></a>신용 카드가 거부되거나 승인되지 않습니다.
가상 카드, 선불 카드 또는 직불 카드는 Azure 구독의 지불 옵션으로 허용되지 않습니다. 그 외 무엇 거절 하 여 카드 toobe 않을 toosee 참조 [직불 카드 또는 신용 카드 등록 azure 에서도 거부 되며](billing-credit-card-fails-during-azure-sign-up.md)합니다.

## <a name="free-trial-is-not-available"></a>"무료 평가판은 제공되지 않습니다."
Azure 구독에서 지난 hello 사용 했습니까? hello Azure 사용 약관 동의 새 tooAzure 인 사용자에 대해서만 무료 평가판 활성화를 제한 합니다. 다른 유형의 Azure 구독이 있는 경우 무료 평가판을 활성화할 수 없습니다. [종량제 구독](https://azure.microsoft.com/offers/ms-azr-0003p/) 등록을 고려합니다.

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>평가판 계정에 요금이 부과되었습니다.
표시 될 수 있습니다 사용할 경우 약간의 확인 등록 한 후, 3 too5 일 내 제거 되는 신용 카드 계정에 저장 합니다. 비용 관리가 염려되는 경우 [예상치 못한 비용 방지](https://docs.microsoft.com/azure/billing/billing-getting-started)에 대해 자세히 알아봅니다.

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>MSDN, BizSpark, BizSparkPlus 또는 MPN 같은 Azure 혜택 계획을 활성화할 수 없습니다.
Hello 오른쪽 로그인 사용 하 고 있는지 확인 자격 증명입니다. Hello 혜택 프로그램 toomake 적합 하 고 있는지 확인 합니다. 

* MSDN
  * [MSDN 계정 페이지](https://msdn.microsoft.com/subscriptions/manage/default.aspx)에서 자격 상태를 확인합니다.
  * 사용자 상태를 확인할 수 없는 경우, 문의 hello [MSDN 구독 고객 서비스 센터](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * Toohello 로그인 [BizSpark 포털](https://www.microsoft.com/bizspark/default.aspx#start-two) BizSpark 및 BizSpark 더하기에 대 한 자격 상태를 확인 합니다.
  * 사용자 상태를 확인할 수 없는 경우, 다음을 할 수 있습니다 [hello BizSpark 포럼에서 도움말을 보려면](http://aka.ms/bzforums)합니다.
* MPN
  * Toohello 로그인 [MPN 포털](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) 자격 상태를 확인 합니다. 적절 한 hello 있으면 [클라우드 플랫폼 능력](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), 추가 혜택에 대 한 구할 수 있습니다.
  * 자신의 상태를 확인할 수 없는 경우 [MPN 지원](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx)에 문의하세요.

## <a name="cant-activate-new-azure-in-open-subscription"></a>새 Azure In Open 구독을 활성화할 수 없습니다.
toocreate 열기에서 Azure 구독을 하나 이상는 Azure에서 열기 관련된 tooit 토큰을 사용 하 여 유효한 온라인 서비스 활성화 (OSA) 키가 있어야 합니다. OSA 키가 없는 경우 [Microsoft Pinpoint](http://pinpoint.microsoft.com/)에 나열된 Microsoft 파트너 중 한 곳에 문의하세요.

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.
도움이 필요 하면 여전히 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.
