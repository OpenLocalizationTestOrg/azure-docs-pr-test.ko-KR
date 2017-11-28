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
# <a name="send-events-tooazure-event-hubs-using-c"></a><span data-ttu-id="9fd68-103">C를 사용 하 여 tooAzure 이벤트 허브 이벤트를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-103">Send events tooAzure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="9fd68-104">소개</span><span class="sxs-lookup"><span data-stu-id="9fd68-104">Introduction</span></span>
<span data-ttu-id="9fd68-105">이벤트 허브는 수백만 개의 초당 응용 프로그램 tooprocess 활성화 이벤트를 수집 하 고 연결 된 장치 및 응용 프로그램에서 생성 되는 데이터의 양이 hello를 분석할 수 있는 확장성이 높은 수집 시스템.</span><span class="sxs-lookup"><span data-stu-id="9fd68-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="9fd68-106">이벤트 허브로 수집된 데이터는 실시간 분석 공급자나 저장소 클러스터를 사용하여 변환하고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="9fd68-107">자세한 내용은 참조 하십시오. [이벤트 허브 개요] hello [이벤트 허브 개요].</span><span class="sxs-lookup"><span data-stu-id="9fd68-107">For more information, please see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="9fd68-108">이 자습서에서는 살펴보겠습니다 toosend 이벤트 tooan 이벤트 허브 C. tooreceive 이벤트에는 콘솔 응용 프로그램을 사용 하 여 hello 왼쪽 목차에서 hello 적절 한 받는 언어를 선택 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-108">In this tutorial, you will learn how toosend events tooan event hub using a console application in C. tooreceive events, click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="9fd68-109">toocomplete이이 자습서에서는 다음 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-109">toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="9fd68-110">C 개발 환경.</span><span class="sxs-lookup"><span data-stu-id="9fd68-110">A C development environment.</span></span> <span data-ttu-id="9fd68-111">이 자습서에서는 Ubuntu 14.04는 Azure Linux VM에 대 한 hello gcc 스택을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-111">For this tutorial, we will assume hello gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="9fd68-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="9fd68-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="9fd68-113">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="9fd68-113">An active Azure account.</span></span> <span data-ttu-id="9fd68-114">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9fd68-115">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9fd68-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="9fd68-116">TooEvent 허브 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="9fd68-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="9fd68-117">이 섹션에서는 C 앱 toosend 이벤트 tooyour 이벤트 허브를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-117">In this section we write a C app toosend events tooyour event hub.</span></span> <span data-ttu-id="9fd68-118">hello 코드 hello에서 hello Proton AMQP 라이브러리를 사용 하 여 [Apache Qpid 프로젝트](http://qpid.apache.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-118">hello code uses hello Proton AMQP library from hello [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="9fd68-119">이것이 유사 toousing 서비스 버스 큐 및 항목 C에서 AMQP 표시 된 것 처럼 [여기](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-119">This is analogous toousing Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="9fd68-120">자세한 내용은 [Qpid Proton 설명서](http://qpid.apache.org/proton/index.html)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9fd68-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="9fd68-121">Hello에서 [Qpid AMQP 메신저 페이지](https://qpid.apache.org/proton/messenger.html), 사용자 환경에 따라 hello 지침 tooinstall Qpid Proton를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-121">From hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow hello instructions tooinstall Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="9fd68-122">toocompile는 Proton 라이브러리 hello, hello 다음 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-122">toocompile hello Proton library, install hello following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="9fd68-123">Hello 다운로드 [Qpid Proton 라이브러리](http://qpid.apache.org/proton/index.html), 예를 들어 압축을 풀고 및:</span><span class="sxs-lookup"><span data-stu-id="9fd68-123">Download hello [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="9fd68-124">빌드 디렉터리를 만들고 컴파일하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="9fd68-125">작업 디렉터리에 새 파일을 만들 **sender.c** 코드 다음 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-125">In your work directory, create a new file called **sender.c** with hello following code.</span></span> <span data-ttu-id="9fd68-126">이벤트 허브 이름 및 네임 스페이스 이름에 대 한 toosubstitute hello 값을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-126">Remember toosubstitute hello value for your event hub name and namespace name.</span></span> <span data-ttu-id="9fd68-127">또한 hello에 대 한 hello 키의 URL로 인코딩된 버전으로 대체 해야 **SendRule** 앞에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-127">You must also substitute a URL-encoded version of hello key for hello **SendRule** created earlier.</span></span> <span data-ttu-id="9fd68-128">[여기](http://www.w3schools.com/tags/ref_urlencode.asp)(영문)에서 URL로 인코드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
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
6. <span data-ttu-id="9fd68-129">Hello 파일을 컴파일하여 가정 **gcc**:</span><span class="sxs-lookup"><span data-stu-id="9fd68-129">Compile hello file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="9fd68-130">이 코드에서는 아웃 1 tooforce hello 메시지는 보내는 창을 최대한 빨리 사용.</span><span class="sxs-lookup"><span data-stu-id="9fd68-130">In this code, we use an outgoing window of 1 tooforce hello messages out as soon as possible.</span></span> <span data-ttu-id="9fd68-131">일반적으로 응용 프로그램 toobatch 메시지 tooincrease 처리량을 시도해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-131">In general, your application should try toobatch messages tooincrease throughput.</span></span> <span data-ttu-id="9fd68-132">Hello 참조 [Qpid AMQP 메신저 페이지](https://qpid.apache.org/proton/messenger.html) toouse Qpid Proton 라이브러리가 예제와 다른 환경 및 바인딩이 제공 되는 플랫폼에서 hello 하는 방법에 대 한 정보에 대 한 (현재 Perl, PHP, Python 및 Ruby).</span><span class="sxs-lookup"><span data-stu-id="9fd68-132">See hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how toouse hello Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9fd68-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9fd68-133">Next steps</span></span>
<span data-ttu-id="9fd68-134">Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd68-134">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="9fd68-135">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="9fd68-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="9fd68-136">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="9fd68-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="9fd68-137">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="9fd68-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
