---
title: "aaa \"Azure CDN 사용자 지정 도메인에서 HTTPS를 사용 하도록 설정 | \"Microsoft Docs"
description: "자세한 방법을 사용자 지정 도메인을 사용 하 여 Azure CDN 끝점에 HTTPS tooenable 합니다."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a>Azure CDN 사용자 지정 도메인에서 HTTPS를 사용하도록 설정

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Azure CDN 사용자 지정 도메인에 대 한 HTTPS 지원을 사용 하면 보안 콘텐츠에 대 한 고유한 도메인 이름을 tooimprove hello 데이터의 보안 전송 중에 사용 하 여 SSL 통해 toodeliver 있습니다. 사용자 지정 도메인에 대 한 hello 종단 간 워크플로 tooenable HTTPS를 통해 한 번의 클릭 사용, 전체 인증서 관리 및 추가 비용 없이 포함 된 모두 간소화 됩니다.

중요 한 tooensure hello 개인 정보 및 전송 중에 웹 응용 프로그램 중요 한 데이터의 모든 데이터 무결성. 인터넷 hello HTTPS 프로토콜을 통해 전송 될 때 중요 한 데이터 암호화는 되도록 hello를 사용 하 여 합니다. 신뢰할 수 있는 인증을 제공하며 공격으로부터 웹 응용 프로그램을 보호합니다. 현재 Azure CDN은 CDN 끝점에서 HTTPS를 지원합니다. 예를 들어 Azure CDN(예: https://contoso.azureedge.net )에서 CDN 끝점을 만드는 경우 기본적으로 HTTPS가 사용하도록 설정됩니다. 이제 사용자 지정 도메인 HTTPS를 사용하여 사용자 지정 도메인(예: https://www.contoso.com )에 대해서도 안전한 전달을 사용할 수 있습니다. 

HTTPS 기능의 hello 키 특성은 다음과 같습니다.

- 추가 비용 없음: 인증서 얻기 또는 갱신에 대해 비용이 없으며 HTTPS 트래픽에 대한 추가 비용이 없습니다. Hello CDN에서에서 GB 수신을 위해만 지불합니다.

- 간단한 구현 지원: 하나 클릭 하 여 프로 비전 하는 것은 hello에서 사용할 수 있는 [Azure 포털](https://portal.azure.com)합니다. 또한 REST API 또는 다른 개발자 도구 tooenable hello 기능을 사용할 수 있습니다.

- 완전한 인증서 관리: 사용자를 위해 모든 인증서 조달 및 관리가 처리됩니다. 인증서는 자동으로 프로 비전 하 고 이전 tooexpiration 갱신 합니다. 이 인증서가 만료 결과로 서비스 중단의 위험 hello 완전히 제거합니다.

>[!NOTE] 
>이전 tooenabling HTTPS를 지원 해야 이미 설정한는 [Azure CDN 사용자 지정 도메인](./cdn-map-content-to-custom-domain.md)합니다.

## <a name="step-1-enabling-hello-feature"></a>1 단계: hello 기능 활성화 

1. Hello에 [Azure 포털](https://portal.azure.com), tooyour Verizon 표준 또는 프리미엄 CDN 프로필을 찾습니다.

2. 끝점의 hello 목록에서 사용자 지정 도메인을 포함 하는 hello 끝점을 클릭 합니다.

3. HTTPS tooenable 원하는 hello 사용자 지정 도메인을 클릭 합니다.

    ![끝점 블레이드](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. 클릭 **에** tooenable HTTPS hello 변경 내용을 저장 합니다.

    ![사용자 지정 HTTPS 대화 상자](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a>2단계: 도메인 유효성 검사

>[!IMPORTANT] 
>사용자 지정 도메인에서 HTTPS를 활성화하기 전에 도메인 유효성 검사를 완료해야 합니다. 6 비즈니스 일 tooapprove hello 도메인을 해야합니다. 업무일 기준 6일 이내 도메인이 승인되지 않으면 요청이 취소됩니다.  

사용자 지정 도메인에서 HTTPS를 사용 하도록 설정한 후 DigiCert 우리의 HTTPS 인증서 공급자는 기본적으로 전자 메일 또는 전화를 통해 WHOIS registrant 정보에 따라 해당 도메인에 대해 hello registrant에 연락 하 여 도메인의 소유권을 확인 합니다. DigiCert 주소 아래 hello 확인 전자 메일 toohello도를 보냅니다. WHOIS 등록자 정보가 개인인 경우 이러한 주소 중 하나에서 직접 승인할 수 있는지 확인합니다.

>admin@<your-domain-name.com> administrator@<your-domain-name.com>  
>webmaster@<your-domain-name.com>  
>hostmaster@<your-domain-name.com>  
>postmaster@<your-domain-name.com>


Hello 전자 메일을 받으면 두 가지 옵션이 있습니다 확인:

1. Hello에 동일한 계정 hello를 통해 받은 이후 모든 주문을 승인 예: consoto.com 같은 루트 도메인. 이 권장된 방법 tooadd hello hello에 대 한 향후에 추가 사용자 지정 도메인을 계획 하는 경우 동일한 루트 도메인.
 
2. 이 요청에서 사용 되는 hello 특정 호스트 이름만 승인할 수 있습니다. 이후 요청에 대해 추가 승인이 필요합니다.

    전자 메일 예:
    
    ![사용자 지정 HTTPS 대화 상자](./media/cdn-custom-ssl/domain-validation-email-example.png)

승인 후 DigiCert 사용자 지정 도메인 이름을 toohello SAN 인증서를 추가 합니다. 1 년 동안 hello 인증서는 유효한 되 고 자동 갱신 전에 만료 되었습니다.

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a>3 단계: hello 전파에 대 한 초간 기다린 다음 기능을 사용 하 여 시작

Hello 도메인 이름을 확인 한 후 hello 사용자 지정 도메인 HTTPS 기능 toobe 활성화에 대 한 too6 8 시간이 소요 됩니다. Hello 프로세스가 완료 되 면 hello Azure 포털에서에서 hello "사용자 지정 HTTPS" 상태 "Enabled" 너무 설정 됩니다. 이제 사용자 지정 도메인이 있는 HTTPS를 사용할 준비가 됩니다.

## <a name="frequently-asked-questions"></a>질문과 대답

1. *Hello 인증서 공급자 및 인증서 종류에 사용 되는 누구 입니까?*

    DigiCert가 제공한 주체 대체 이름(SAN) 인증서를 사용합니다. SAN 인증서는 한 개의 인증서로 여러 정규화된 도메인 이름을 보안 지정할 수 있습니다.

2. *전용 인증서를 사용할 수 있나요?*
    
    on hello 로드맵 하지만 현재는 합니다.

3. *경우에 어떻게 hello 도메인 확인 전자 메일 DigiCert에서 받지 못합니다?*

    24시간 이네 전자 메일을 받지 못하면 Microsoft에 문의하세요.

4. *SAN 인증서를 사용하는 것보다 전용 인증서를 사용하는 것이 더 안전한가요?*
    
    다음과 같이 hello 전용된 인증서와 동일한 암호화 및 보안 표준을 준수 하는 SAN 인증서입니다. 발급된 모든 SSL 인증서는 서버 보안 강화를 위해 SHA-256을 사용 중입니다.

5. *Akamai의 Azure CDN에서 사용자 지정 도메인 HTTPS를 사용할 수 있나요?*

    현재 이 기능은 Verizon의 Azure CDN에만 사용할 수 있습니다. 향후 몇 개월 hello Akamai에서 Azure CDN와 함께이 기능을 지 원하는 작업입니다.


## <a name="next-steps"></a>다음 단계

- 자세한 방법을를 tooset는 [Azure CDN 끝점에 사용자 지정 도메인](./cdn-map-content-to-custom-domain.md)


