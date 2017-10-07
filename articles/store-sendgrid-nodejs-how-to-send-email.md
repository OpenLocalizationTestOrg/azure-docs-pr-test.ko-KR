---
title: "aaaHow toouse hello SendGrid 전자 메일 서비스 (Node.js) | Microsoft Docs"
description: "자세한 내용은 Azure에서 SendGrid 전자 메일 서비스 hello로 전자 메일을 보내려면 어떻게 합니다. 코드 샘플 hello Node.js API를 사용 하 여 작성 합니다."
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a>어떻게 tooSend Node.js에서 사용 하 여 SendGrid 전자 메일
이 가이드에서는 tooperform 일반적인 프로그래밍 작업 SendGrid Azure에서 서비스 메일 하는 방법을 보여 줍니다. hello 샘플 hello Node.js API를 사용 하 여 기록 됩니다. hello 가이드에서 다루는 시나리오 포함 **전자 메일 구성**, **메일을 보내는**, **첨부 파일 추가**, **필터를 사용 하 여**, 및 **속성 업데이트**합니다. SendGrid 및 전자 메일에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.

## <a name="what-is-hello-sendgrid-email-service"></a>Hello SendGrid 전자 메일 서비스는 무엇입니까?
SendGrid는 사용자 지정 통합을 쉽게 만드는 유연한 API와 함께 신뢰할 만한 [트랜잭션 전자 메일 배달], 확장성 및 실시간 분석을 제공하는 [클라우드 기반 전자 메일 서비스]입니다. 일반적인 SendGrid 사용 시나리오는 다음과 같습니다.

* 자동으로 확인 메일 toocustomers 보내기
* 월간 전자 전단 및 판촉 행사를 고객에게 보내기 위한 분산 목록 관리
* 차단된 전자 메일, 고객 응답 같은 항목의 실시간 메트릭 수집
* Toohelp 추세를 파악 하는 보고서 생성
* 고객 문의 전달
* 응용 프로그램의 전자 메일 알림

자세한 내용은 [https://sendgrid.com](https://sendgrid.com)을 참조하세요.

## <a name="create-a-sendgrid-account"></a>SendGrid 계정 만들기
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a>참조 hello SendGrid Node.js 모듈
Node.js 용 hello SendGrid 모듈 hello 다음 명령을 사용 하 여 hello 노드 패키지 관리자 (npm)를 통해 설치할 수 있습니다.

    npm install sendgrid

설치 후 코드 다음 hello를 사용 하 여 응용 프로그램에서 hello 모듈을 요구할 수 있습니다.

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

hello SendGrid 모듈이 내보내는 hello **SendGrid** 및 **전자 메일** 함수입니다.
**SendGrid**는 Web API를 통해 전자 메일을 보내는 역할을 맡고, **Email**은 전자 메일 메시지를 캡슐화합니다.

## <a name="how-to-create-an-email"></a>방법: 전자 메일 만들기
Hello SendGrid 모듈을 사용 하 여 전자 메일 메시지를 만들면 먼저 hello 전자 메일 함수를 사용 하 고 다음 hello SendGrid 함수를 사용 하 여 보내는 전자 메일 메시지를 만드는 과정이 포함 됩니다. hello 다음은 hello 전자 메일 함수를 사용 하 여 새 메시지를 만드는 예입니다.

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

클라이언트 hello html 속성을 설정 하 여 지원에 대 한 HTML 메시지를 지정할 수도 있습니다. 예:

    html: This is a sample <b>HTML<b> email message.

Hello 텍스트 및 html 속성이 모두 설정 HTML 메시지를 지원할 수 없는 클라이언트에 대 한 정상적인 대체 텍스트 콘텐츠를 제공 합니다.

Hello 전자 메일 함수에서 지 원하는 모든 속성에 대 한 자세한 내용은 참조 하십시오. [sendgrid nodejs][sendgrid-nodejs]합니다.

## <a name="how-to-send-an-email"></a>방법: 전자 메일 보내기
전자 메일 함수 hello를 사용 하 여 전자 메일 메시지를 만든 후 hello SendGrid에서 제공 하는 웹 API를 사용 하 여 보낼 수 있습니다. 

### <a name="web-api"></a>Web API
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> 위의 예제는 hello 표시 메일 개체와 콜백 함수에 전달 하는 동안에 직접 직접 전자 메일 속성을 지정 하 여 hello 보내기 함수를 호출할 수 있습니다. 예:  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a>방법: 첨부 파일 추가
첨부 파일 hello에 hello 파일 이름 및 경로 지정 하 여 tooa 메시지 추가할 수 있습니다 **파일** 속성입니다. 다음 예제는 hello 첨부 파일을 전송 하는 방법을 보여 줍니다.

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> Hello를 사용 하는 경우 **파일** 속성 hello 파일을 통해 액세스할 수 있어야 [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile)합니다. Blob 컨테이너와 같이 Azure 저장소에 tooattach hello 파일이 호스트 되는 경우 먼저 복사 해야 hello 파일 toolocal 저장소 또는 Azure 드라이브 tooan hello를 사용 하 여 첨부 파일로 보내기 전에 **파일** 속성입니다.
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a>방법: 추적 및 tooEnable 바닥글에는 필터를 사용 하
SendGrid는 hello 필터 사용을 통해 추가 전자 메일 기능을 제공합니다. 이 클릭 추적, Google 분석, 추적, 구독을 설정 하는 등 특정 기능을 사용 하도록 설정 하려면 tooan 전자 메일 메시지를 추가할 수 있는 설정 등입니다. 전체 필터 목록은 [필터 설정][Filter Settings](영문)을 참조하십시오.

필터는 hello를 사용 하 여 적용 된 tooa 메시지 수 **필터** 속성입니다.
각 필터는 필터별 설정을 포함하는 해시에 의해 지정됩니다.
hello 다음 예제 hello 바닥글을 보여 주고 추적 필터를 클릭:

### <a name="footer"></a>바닥글
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a>클릭 추적
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a>방법: 전자 메일 속성 업데이트
사용 하 여 일부 전자 메일 속성을 덮어쓸 수  **설정*속성** *를 사용 하 여 추가 또는  **추가*속성** *입니다. 예를 들어 다음을 사용하여 받는 사람을 더 추가할 수 있습니다.

    email.addTo('jeff@contoso.com');

또는 다음을 사용하여 필터를 설정할 수 있습니다.

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

자세한 내용은 참조 [sendgrid nodejs][sendgrid-nodejs]합니다.

## <a name="how-to-use-additional-sendgrid-services"></a>방법: 추가 SendGrid 서비스 사용
SendGrid 웹 기반 Api 제공 tooleverage 추가 SendGrid 기능을 Azure 응용 프로그램에서 사용할 수 있습니다. 전체 세부 정보에 대 한 참조 hello [SendGrid API 설명서][SendGrid API documentation]합니다.

## <a name="next-steps"></a>다음 단계
Hello SendGrid 전자 메일 서비스의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* SendGrid Node.js 모듈 리포지토리: [sendgrid nodejs][sendgrid-nodejs]
* SendGrid API 설명서: <https://sendgrid.com/docs>
* Azure 고객을 위한 SendGrid 특가 제공: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[클라우드 기반 전자 메일 서비스]: https://sendgrid.com/email-solutions
[트랜잭션 전자 메일 배달]: https://sendgrid.com/transactional-email
