---
title: "이벤트 허브 aaaSend 이벤트 tooAzure C를 사용 하 여 | Microsoft Docs"
description: "C를 사용 하 여 tooAzure 이벤트 허브 이벤트를 전송 합니다."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: c
ms.devlang: csharp
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: bb53300c070debb4a3658a38df9d3966f08e81ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-c"></a>C를 사용 하 여 tooAzure 이벤트 허브 이벤트를 전송 합니다.

## <a name="introduction"></a>소개
이벤트 허브는 수백만 개의 초당 응용 프로그램 tooprocess 활성화 이벤트를 수집 하 고 연결 된 장치 및 응용 프로그램에서 생성 되는 데이터의 양이 hello를 분석할 수 있는 확장성이 높은 수집 시스템. 이벤트 허브로 수집된 데이터는 실시간 분석 공급자나 저장소 클러스터를 사용하여 변환하고 저장할 수 있습니다.

자세한 내용은 참조 하십시오. [이벤트 허브 개요] hello [이벤트 허브 개요].

이 자습서에서는 살펴보겠습니다 toosend 이벤트 tooan 이벤트 허브 C. tooreceive 이벤트에는 콘솔 응용 프로그램을 사용 하 여 hello 왼쪽 목차에서 hello 적절 한 받는 언어를 선택 하는 방법입니다.

toocomplete이이 자습서에서는 다음 hello 필요 합니다.

* C 개발 환경. 이 자습서에서는 Ubuntu 14.04는 Azure Linux VM에 대 한 hello gcc 스택을 가정 합니다.
* [Microsoft Visual Studio](https://www.visualstudio.com/).
* 활성 Azure 계정. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.

## <a name="send-messages-tooevent-hubs"></a>TooEvent 허브 메시지 보내기
이 섹션에서는 C 앱 toosend 이벤트 tooyour 이벤트 허브를 작성할 수 있습니다. hello 코드 hello에서 hello Proton AMQP 라이브러리를 사용 하 여 [Apache Qpid 프로젝트](http://qpid.apache.org/)합니다. 이것이 유사 toousing 서비스 버스 큐 및 항목 C에서 AMQP 표시 된 것 처럼 [여기](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504)합니다. 자세한 내용은 [Qpid Proton 설명서](http://qpid.apache.org/proton/index.html)(영문)를 참조하세요.

1. Hello에서 [Qpid AMQP 메신저 페이지](https://qpid.apache.org/proton/messenger.html), 사용자 환경에 따라 hello 지침 tooinstall Qpid Proton를 수행 합니다.
2. toocompile는 Proton 라이브러리 hello, hello 다음 패키지를 설치 합니다.
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. Hello 다운로드 [Qpid Proton 라이브러리](http://qpid.apache.org/proton/index.html), 예를 들어 압축을 풀고 및:
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. 빌드 디렉터리를 만들고 컴파일하고 설치합니다.
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. 작업 디렉터리에 새 파일을 만들 **sender.c** 코드 다음 hello로 합니다. 이벤트 허브 이름 및 네임 스페이스 이름에 대 한 toosubstitute hello 값을 기억 합니다. 또한 hello에 대 한 hello 키의 URL로 인코딩된 버전으로 대체 해야 **SendRule** 앞에서 만든 합니다. [여기](http://www.w3schools.com/tags/ref_urlencode.asp)(영문)에서 URL로 인코드할 수 있습니다.
   
    ```c
    #include "proton/message.h"
    #include "proton/messenger.h"
   
    #include <getopt.h>
    #include <proton/util.h>
    #include <sys/time.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <stdlib.h>
   
    #define check(messenger)                                                     
      {                                                                          
        if(pn_messenger_errno(messenger))                                        
        {                                                                        
          printf("check\n");                                                     
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); 
        }                                                                        
      }  
   
    pn_timestamp_t time_now(void)
    {
      struct timeval now;
      if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");
      return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);
    }  
   
    void die(const char *file, int line, const char *message)
    {
      printf("Dead\n");
      fprintf(stderr, "%s:%i: %s\n", file, line, message);
      exit(1);
    }
   
    int sendMessage(pn_messenger_t * messenger) {
        char * address = (char *) "amqps://SendRule:{Send Rule key}@{namespace name}.servicebus.windows.net/{event hub name}";
        char * msgtext = (char *) "Hello from C!";
   
        pn_message_t * message;
        pn_data_t * body;
        message = pn_message();
   
        pn_message_set_address(message, address);
        pn_message_set_content_type(message, (char*) "application/octect-stream");
        pn_message_set_inferred(message, true);
   
        body = pn_message_body(message);
        pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));
   
        pn_messenger_put(messenger, message);
        check(messenger);
        pn_messenger_send(messenger, 1);
        check(messenger);
   
        pn_message_free(message);
    }
   
    int main(int argc, char** argv) {
        printf("Press Ctrl-C toostop hello sender process\n");
   
        pn_messenger_t *messenger = pn_messenger(NULL);
        pn_messenger_set_outgoing_window(messenger, 1);
        pn_messenger_start(messenger);
   
        while(true) {
            sendMessage(messenger);
            printf("Sent message\n");
            sleep(1);
        }
   
        // release messenger resources
        pn_messenger_stop(messenger);
        pn_messenger_free(messenger);
   
        return 0;
    }
    ```
6. Hello 파일을 컴파일하여 가정 **gcc**:
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > 이 코드에서는 아웃 1 tooforce hello 메시지는 보내는 창을 최대한 빨리 사용. 일반적으로 응용 프로그램 toobatch 메시지 tooincrease 처리량을 시도해 야 합니다. Hello 참조 [Qpid AMQP 메신저 페이지](https://qpid.apache.org/proton/messenger.html) toouse Qpid Proton 라이브러리가 예제와 다른 환경 및 바인딩이 제공 되는 플랫폼에서 hello 하는 방법에 대 한 정보에 대 한 (현재 Perl, PHP, Python 및 Ruby).


## <a name="next-steps"></a>다음 단계
Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [이벤트 허브 개요](event-hubs-what-is-event-hubs.md
)
* [이벤트 허브 만들기](event-hubs-create.md)
* [Event Hubs FAQ](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
