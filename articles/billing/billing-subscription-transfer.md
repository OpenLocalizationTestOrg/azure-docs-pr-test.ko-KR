---
title: "Azure 구독 소유권 tooanother 계정 aaaTransfer | Microsoft Docs"
description: "어떻게 tootransfer는 Azure 구독 tooanother 사용자와 일부 질문과 대답 (FAQ) hello 프로세스에 대 한 설명"
keywords: "azure 구독에 azure 전송 구독 이전을, azure 구독 tooanother 계정, 구독 소유자 변경 azure, azure 전송 구독 tooanother 계정 이동"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: c8ecdc1e-c9c5-468c-a024-94ae41e64702
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2d9f5d9ccd34738701493e5f31c2f83a02f5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-ownership-of-an-azure-subscription-tooanother-account"></a>Azure 구독 tooanother 계정의 소유권 이전

Hello r e 계정 센터의에서 구독을 종 량 제, Visual Studio, 동작 팩 또는 BizSpark tooanother 사용자 구독을 전송할 수 있습니다. 이러한 구독 형식에 대 한 외부 서비스를 Azure의 hello 전송을 지원합니다. 

하는 경우 Azure 구독의 tootransfer 소유권을 할 수 있습니다.

* 다른 Azure 구독 toosomeone 프로그램의 청구 소유권 toohand가 필요 합니다.
* Toochange hello 계정이 toosign Azure에 대해 사용 합니다. 아마도 하면 Microsoft 계정을 사용 하는 아니지만 toouse 회사 또는 학교 계정 대신 있습니다.
* Toomove tooanother 한 디렉터리에서에서 Azure 구독을 합니다.
* 다른 테 넌 트에 Azure 및 Office 365를 있으며 tooconsolidate 하고자 합니다.

toochange 다른 프로그램 구독 tooa 제공 참조 [Azure 구독 tooanother 제안을 전환](billing-how-to-switch-azure-offer.md)합니다. 

## <a name="transfer-ownership-of-an-azure-subscription"></a>Azure 구독의 소유권 양도
> [!VIDEO https://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/Transfer-an-Azure-subscription/player]
>
>

1. <https://account.windowsazure.com/Subscriptions>에 로그인합니다. Toobe hello 계정 관리자 tooperform 소유권 이전 해야합니다. hello hello 구독의 계정 관리자에 게 아웃 toofind 참조 hello [질문과 대답](#faq)합니다.

2. Hello 구독 tootransfer를 선택 합니다.

3. Hello 클릭 **전송 구독** 옵션입니다. 참조 [FAQ](#no-button) hello 단추가 표시 되지 않습니다.

   ![Azure 계정 구독 탭](./media/billing-subscription-transfer/image1.png)
4. Hello 받는 사람을 지정 합니다.

   ![구독 양도 대화 상자](./media/billing-subscription-transfer/image2.PNG)
5. hello 받는 사람 전자 메일을 동의 링크를 자동으로 가져옵니다.

   ![구독 전송이 전자 메일 toorecipient](./media/billing-subscription-transfer/image3.png)
6. hello 받는 사람 hello 링크를 클릭 하 고 지불 정보를 입력 하는 등 hello 지침을 따릅니다.

   ![첫 번째 구독 양도 웹 페이지](./media/billing-subscription-transfer/image4.png)

   ![두 번째 구독 양도 웹 페이지](./media/billing-subscription-transfer/image5.png)
7. 성공! hello 구독은 이제 전송 됩니다.

## <a name="transfer-subscription-ownership-for-enterprise-agreement-ea-customers"></a>EA(기업 계약) 고객의 구독 소유권 양도
엔터프라이즈 관리자 hello 등록 내 구독 소유권을 전송할 수 있습니다. 시작 tooget 참조 [계정 소유권 전송](https://ea.azure.com/helpdocs/changeAccountOwnerForASubscription) hello EA 포털에서 합니다.

## <a name="next-steps-after-accepting-ownership-of-a-subscription"></a>구독 소유권을 수락한 후 다음 단계
1. Hello 계정 관리자가 나타납니다. 검토 하 고 hello 서비스 관리자 및 공동 관리자를 업데이트 합니다. Hello에서 관리자가 사용자 관리 [Azure 클래식 포털](https://manage.windowsazure.com) tooSettings 이동 합니다. [관리자 역할에 대해 알아봅니다](billing-add-change-azure-subscription-administrator.md).

2. 구독 및 서비스에 대해 RBAC(역할 기반 액세스 제어)를 사용할 수도 있습니다. Hello 방문 [Azure 포털](https://portal.azure.com)합니다. [RBAC에 대한 자세한 정보](../active-directory/role-based-access-control-configure.md)

3. 다음을 비롯한 이 구독의 서비스와 연결된 자격 증명을 업데이트합니다.
   
   * 관리 인증서 toosubscription 리소스 hello 사용자 관리 권한 부여입니다. 자세한 내용은 [Create and upload a management certificate for Azure](../cloud-services/cloud-services-certs-create.md)
   
   * 저장소와 같은 서비스에 대한 액세스 키. 자세한 내용은 [Azure Storage 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.
   
   * Azure Virtual Machines 같은 서비스에 대한 원격 액세스 자격 증명. 

4. [이 구독에 대 한 결제 경고를 업데이트](billing-set-up-alerts.md) hello에 [Azure 계정 센터](https://account.windowsazure.com/Subscriptions)합니다. 

5. 파트너를 사용 하는 경우에이 구독에 hello 파트너 ID를 업데이트 하는 것이 좋습니다. Hello에 hello 파트너 ID를 업데이트할 수 있습니다 [Azure 계정 센터](https://account.windowsazure.com/Subscriptions)합니다.

<a id="faq"></a>

## <a name="frequently-asked-questions-faq"></a>질문과 대답(FAQ)
* <a name="whoisaa"></a>**Hello 구독의 계정 관리자에 게 사용 하는?**

  계정 관리자에 게는 hello 사용자에 등록 또는 hello Azure 구독을 구입한입니다. 권한 있는 tooaccess hello 하기가 [r e 계정 센터](https://account.windowsazure.com/Home/Index) 하 고 구독을 만들고, 구독 취소, 구독에 대 한 hello 청구 변경 또는 hello 서비스 관리자 변경와 같은 다양 한 관리 작업을 수행 합니다. 확실 하지 않은 구독에 대 한 계정 관리자에 게 인을 하는 경우 아웃 toofind 단계를 수행 하는 hello를 사용 합니다.

  1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
  2. Hello 허브 메뉴에서 선택 **구독**합니다.
  3. Hello 구독 toocheck을 다음 선택 **설정을**합니다.
  4. **속성**을 선택합니다. hello에 hello 구독의 계정 관리자에 게 표시 되 **계정 관리자** 상자입니다.  

* **모든 것이 양도되나요? 양도 항목에 리소스 그룹, VM, 디스크 및 기타 실행 중인 서비스가 포함되나요?**

  예, 모든 리소스와 Vm, 디스크, 같은 하 고 웹 사이트 toohello 새 소유자를 전송 합니다. 그러나 설정한 [관리자 역할](billing-add-change-azure-subscription-administrator.md) 및 [RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-configure.md) 정책은 다른 디렉터리 간에 양도되지 않습니다.

* <a id="no-button"></a>**볼 수 없는 전송 구독 hello 단추?**

  Hello 표시 되지 않으면 **전송 구독** 단추를 자신의 구독에 대 한 구독 전송이 지원 되지 않습니다. [고객 지원에 문의하세요](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

* **구독 양도로 인해 서비스 가동 중지 시간이 발생합니까?**

  영향 toohello 서비스가 없는 합니다. Hello 구독 전송이 hello hello 현재 계정 관리자는 구독을 취소 하 고 hello 받는 사람의 계정에서 구독을 만듭니다. hello 새 구독이 연결된 toohello 기본 Azure 서비스입니다. hello 구독 ID 유지 hello 동일 합니다.

* **구독에 대 한이 프로세스 toochange hello 디렉터리를 사용 하는 방법**

  Azure 구독에 속한 계정 관리자는 hello hello 디렉터리에 생성 됩니다. hello 대상 디렉터리의 전송 hello 구독 tooa 사용자 계정 toochange hello 디렉터리입니다. 해당 사용자는 hello 단계 tooaccept 전송 완료 되 면 hello 구독은 자동으로 이동된 toohello 대상 디렉터리입니다.

* **다른 조직 으로부터 구독의 청구 소유권을 받으십시오 I 경우 toohave toomy 리소스에 액세스 계속 수행?**

  전송 된 tooanother 테 넌 트 hello 구독을 사용 하는 경우 hello 이전 테 넌 트와 연결 된 hello 사용자 액세스 toohello 구독의 손실입니다. 사용자가 있는 서비스 관리자 또는 공동 관리자 더 이상 포함 될 수 여전히 포함 하 여 다른 보안 메커니즘을 통해 액세스 toohello 구독 하는 경우에:

  * 관리 인증서 toosubscription 리소스 hello 사용자 관리 권한 부여입니다. 자세한 내용은 [Azure용 관리 인증서 만들기 및 업로드](../cloud-services/cloud-services-certs-create.md)를 참조하세요.
  * 저장소와 같은 서비스에 대한 액세스 키. 자세한 내용은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.
  * Azure Virtual Machines 같은 서비스에 대한 원격 액세스 자격 증명.

 Hello 받는 toorestrict tootheir 리소스에 액세스를 필요로 한다면 고려해 보는 것 hello 서비스와 관련 된 모든 암호를 업데이트 합니다. 단계를 수행 하는 hello를 사용 하 여 가장 많은 리소스를 업데이트할 수 있습니다.

    1. Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.
    2. Hello 허브 메뉴에서 선택 **모든 리소스**합니다.
    3. Hello 리소스를 선택 합니다. 
    4. Hello 리소스 블레이드 클릭 **설정을**합니다. 여기서 기존 암호를 보고 업데이트할 수 있습니다.

* **청구 주기 hello hello 가운데에 hello 구독을 전송 하려면 hello 전체 청구에 대 한 받는 사람 급여 hello 주기는?**

  hello 발신자는 hello 전송이 완료 된 toohello 포인트 보고 된 모든 사용에 대 한 지불 합니다. hello 수신자는 hello 시간 이후 전송에서 보고 한 사용 합니다. 양도하기 전에 발생하지만 나중에 보고되는 일부 사용량이 있을 수 있습니다. hello 사용 hello 받는 사람의 청구서에 포함 됩니다.

* **Hello 받는 사람에는 액세스 toousage 및 청구 내역?**

  hello 정보만 사용할 수 있는 toohello 받는 사람 hello 양의 hello 마지막 청구서 또는 첫 번째 hello bill 생성 되기 전 hello 구독 전송 된 경우 현재 잔액이 hello 합니다. hello 사용 및 청구 내역 hello 나머지 hello 구독과 전송 되지 않습니다.

* **Hello 제공을 전송 하는 동안 변경할 수 있습니까?**

  hello 제공 해 있어야 hello 동일 합니다. toochange 제공 참조 [Azure 구독 tooanother 제안을 전환](billing-how-to-switch-azure-offer.md)합니다.

* **다른 국가에 구독 tooa 사용자 계정이 전송할 수 있습니까?**

  아니요, 구독 tooa 사용자 계정을 다른 국가에서 전송도 지원 되지 않습니다. hello 받는 사람의 사용자 계정이 hello에 있어야 합니다. 동일한 국가입니다.

* **Hello 받는 다른 결제 방법을 사용할 수 있습니까?**

  예. 하지만 hello 구독 청구 기록 두 계정에서 분리 됩니다.  

* **Azure 구독을 전송 하려면 후 영향을 지불 방법 hello?**

  tooaccept 구독 전송이, 신용 카드 또는 유사한 결제 방법을 제공 해야 합니다 toopay hello 구독에 대 한 합니다. 예를 들어 Bob 전송 구독 tooJane Jane hello 전송을 허용 하는 경우 Jane는 hello 구독에 대 한 지불 방법을 toopay을 제공 해야 합니다. Hello 전송이 완료 된 후에 Jane hello 구독 하지 Bob에 대해 요금이 청구 됩니다.

* **데이터 및 서비스 내 Azure 구독 toonew 구독에 대 한 마이그레이션 방법**

  구독 소유권을 양도할 수 없는 경우 리소스를 수동으로 마이그레이션할 수 있습니다. 참조 [리소스 toonew 리소스 그룹이 나 구독 이동](../azure-resource-manager/resource-group-move-resources.md)합니다.



## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.
도움이 필요 하면 여전히 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다. 


