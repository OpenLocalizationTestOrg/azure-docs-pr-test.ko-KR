---
title: "aaaHow toouse Blitline 이미지 처리-에 대 한 Azure 기능 가이드"
description: "Toouse hello Blitline Azure 응용 프로그램 내에서 tooprocess 이미지를 서비스 하는 방법에 대해 알아봅니다."
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a>어떻게 toouse Blitline Azure 및 Azure 저장소
이 가이드에서는 설명 하는 방법을 tooaccess Blitline 서비스 및 toosubmit tooBlitline 작업 하는 방법입니다.

## <a name="what-is-blitline"></a>Blitline 정의
Blitline는 toobuild를 비용이 됩니다 hello 가격의 일부분에 엔터프라이즈 수준의 이미지 처리를 제공 하는 서비스를 처리 하는 클라우드 기반 이미지 것 직접 합니다.

hello 사실은 이미지 처리 조건이 반복 해 서, 일반적으로 각 웹 사이트에 대해 명확 하 게 hello에서에서 다시 작성 합니다. 이미지를 수백만 번 다시 빌드했기 때문에 이러한 사실을 알 수 있었습니다. 그러다 문득 모든 사용자를 위해 이 작업을 수행하기로 했습니다. 회원님의 어떻게 toodo 하 고 효율적으로 빠르고 everyone 저장에서 작동 hello 그 동안 toodo 것입니다.

자세한 내용은 [http://www.blitline.com](http://www.blitline.com)(영문)을 참조하십시오.

## <a name="what-blitline-is-not"></a>Blitline이 수행할 수 없는 작업
tooclarify Blitline 무엇이 유용한 정보 Blitline 하지 기능은 무엇입니까 앞으로 이동 하기 전에 보다 쉽게 종종 tooidentify는에 대 한 합니다.

* Blitline는 HTML 위젯 tooupload 이미지는 수 없습니다. 공개적으로 또는 Blitline tooreach에 사용할 수 있는 제한 된 권한으로 사용할 수 있는 이미지를 있어야 합니다.
* Blitline은 Aviary.com처럼 라이브로 이미지를 처리하지 않습니다.
* Blitline 이미지 업로드를 허용 하지 않습니다, 그리고 직접 이미지 tooBlitline를 푸시할 수 없습니다. 밀어넣기 tooAzure 저장소 또는 다른 위치 Blitline 지원 하 고 게 toogo 얻을 Blitline 지시 해야 합니다.
* Blitline은 대량 병렬식이어서 동기식 처리를 하지 않습니다. 즉, postback_url을 보내주어야 처리가 완료되는 시점을 알려줄 수 있습니다.

## <a name="create-a-blitline-account"></a>Blitline 계정 만들기
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a>어떻게 toocreate Blitline 작업
Blitline는 tootake 이미지에 원하는 JSON toodefine hello 동작을 사용 합니다. 이 JSON은 간단한 필드 몇 개로 구성됩니다.

hello 가장 간단한 예제는 다음과 같습니다.

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

"Src" 이미지를 수행 하는 JSON 가지 "... boys.jpeg" 다음 해당 이미지 too240x140 크기를 조정 합니다.

응용 프로그램 ID hello 리에서 찾을 수 있습니다 프로그램 **연결 정보입니다.** 또는 **관리** Azure에서 탭 합니다. 것은 Blitline에 toorun 작업을 허용 하 여 보안 식별자입니다.

"저장" 매개 변수는 hello 저장할 tooput hello 이미지 처리 한 후에 대 한 정보를 식별 합니다. 간단한 이 경우에서는 정의하지 않았습니다. 위치를 정의하지 않으면 Blitline은 고유 클라우드 위치에 이미지를 로컬로(및 일시적으로) 저장합니다. Hello Blitline를 만들면 JSON hello에서 위치 Blitline 반환한 수 tooget 됩니다. hello "이미지" 식별자는 필요 하며 tooidentify이이 특정 이미지를 저장할 때 tooyou 반환 됩니다.

Hello에 대 한 자세한 정보를 찾을 수 *함수* 여기 지원: <http://www.blitline.com/docs/functions>

찾을 수 있습니다 hello에 대 한 설명서 여기에 작업 옵션: <http://www.blitline.com/docs/api>

Toodo 가장 필요한 것은, JSON 있으면 **POST** 것 너무`http://api.blitline.com/job`

다음과 유사한 JSON이 반환됩니다.

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


이 통해 사용자는 Blitline 사용자 요청을 받았습니다, 처리 큐에 넣습니다에 및 완료 되지 않았을 hello 이미지에서 사용할 수 있습니다: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_앱\_ID /CK3f0xBF_2bV6wf7gEZE8w.jpg**

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a>어떻게 toosave 이미지 tooyour Azure 저장소 계정
Azure 저장소 계정이 있는 경우 수 있을 수 있습니다 Blitline 푸시 처리 hello 이미지 Azure 컨테이너에. "Azure_destination"를 추가 하 여 hello 위치 및 Blitline toopush에 대 한 사용 권한을 정의 합니다.

다음은 예제입니다.

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


자신의 hello CAPITALIZED 값을 입력 하 여이 JSON toohttp://api.blitline.com/job 제출할 수 있습니다 하 고 hello "src" 이미지 흐림 효과 필터를 사용 하 여 처리 됩니다 다음 Azure 대상 tooyou 푸시됩니다.

### <a name="please-note"></a>참고:
hello SAS hello 전체 SAS url을 hello 대상 파일의 hello 파일 이름을 포함 하 여 포함 해야 합니다.

예제:

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


Hello Blitline의 Azure 저장소 설명서의 최신 버전을 읽을 수도 있습니다 [여기](http://www.blitline.com/docs/azure_storage)합니다.

## <a name="next-steps"></a>다음 단계
이 다른 모든 기능에 대 한 blitline.com tooread 방문.

* Blitline API 끝점 문서 <http://www.blitline.com/docs/api>(영문)
* Blitline API 함수 <http://www.blitline.com/docs/functions>(영문)
* Blitline API 예제 <http://www.blitline.com/docs/examples>(영문)
* 타사 Nuget 라이브러리 <http://nuget.org/packages/Blitline.Net>(영문)

