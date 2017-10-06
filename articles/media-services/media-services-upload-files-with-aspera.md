---
title: "Aspera를 사용 하 여 Azure 미디어 서비스 계정으로 aaaUpload 파일 | Microsoft Docs"
description: "이 자습서에서는 예제 hello를 사용 하 여 미디어 서비스 계정에 연결 된 저장소 계정에 파일을 업로드 hello 단계 * * Aspera 서버에서 요청 시 * * Azure 서비스입니다."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a>Hello Aspera Server On Demand 서비스를 사용 하 여 Azure에서 미디어 서비스 계정에 파일 업로드

## <a name="overview"></a>개요

**Aspera** 는 고속 파일 전송 소프트웨어입니다. Azure용 **Aspera Server On Demand**는 Azure BLOB 개체 저장소에 직접 대용량 파일을 고속으로 업로드 및 다운로드할 수 있게 해줍니다. 에 대 한 내용은 **Aspera On Demand**, hello 참조 [Aspera 클라우드](http://cloud.asperasoft.com/) 사이트입니다. 
  
**Aspera Server On Demand** Azure hello에서 구입할 수에 대 한 [Azure 마켓플레이스](https://azure.microsoft.com/en-us/marketplace/)합니다. 순서로 toocomplete의 구매 **Aspera Server On Demand** Azure에 로그인 한 다음 Windows Live id를 사용 하 여 Azure 마켓플레이스

이 자습서에서는 예제 hello를 사용 하 여 미디어 서비스 계정에 연결 된 저장소 계정에 파일을 업로드 hello 단계 **Aspera Server On Demand** Azure에서 서비스입니다. 

Azure toouse Aspera 및 미디어 서비스와 작동 하는 방법을 보여 주는 예제를 찾을 수 있습니다 [여기](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest)합니다.

>[!NOTE]
>Azure 미디어 서비스로 미디어 프로세서 (Mp) 처리에 지원 제한 toohello 최대 파일 크기를 있습니다. 참조 하십시오 [이](media-services-quotas-and-limitations.md) hello 파일 크기 제한에 대 한 세부 정보에 대 한 항목입니다.
>

## <a name="prerequisites"></a>필수 조건 

toocomplete 해야이 자습서에서는:

* Windows Live ID
* [Azure 계정](https://azure.microsoft.com) 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요. 
* [Azure Media Services 계정](media-services-portal-create-account.md)

## <a name="purchase-aspera-on-demand-for-azure"></a>Azure용 Aspera On Demand 구매

Azure Marketplace에 로그인 하면 이러한 기본 단계 toocomplete Aspera On Demand for Azure의 구입을 수행 합니다.

1. Aspera를 검색하고 'Server On Demand'를 선택합니다.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. Hello 구독 계획을 검토 하 고 ' 등록 ' 클릭

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. 요청 시 구독에서 서버에 대 한 hello 고유 정보를 입력 합니다.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. Hello 클릭 **가격 책정 계층** hello sub 패널에서 원하는 월별 볼륨을 선택 합니다. Hello에 **세부 정보를 계획** 패널에서 **확인**합니다. 그런 다음, hello **가격 책정 계층 선택** 에서 **선택**합니다.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. 클릭 **약관** tooview hello hello sub 패널의 법적 조항에 동의 하 고 있습니다. Hello 약관을 검토 한 후 클릭 **구매**합니다.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. 클릭 하 여 hello 구매를 완료 **만들기**합니다.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. Azure 대시보드 hello 공지 hello 서비스 프로 비전 됩니다.  프로비저닝 완료 되 면 hello hello 서비스 이름에 대 한 리소스를 검색 하 여 hello 새 구독을 찾을 수 있습니다. 발견 하면 hello 서비스를 두 번 클릭 toolaunch hello 서비스 관리 포털.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. Hello Aspera 관리 포털을 시작 합니다. 새 Aspera 서비스를 발견 하면 hello 서비스를 클릭 하 여 액세스 toohello 관리 포털을 얻을 수 있습니다.  새 패널이 시작됩니다. 새 해당 패널 내에서 필요한 hello에 tooclick **리소스 이름** 새 서비스의 합니다.  다음 스크린 샷 hello, hello 리소스 이름은 'AsperaTransferDemo'입니다. Hello 리소스 이름을 클릭 한 후 다른 패널 시작 됩니다. 새로 시작된 패널에 '관리' 링크가 표시됩니다. '관리' 링크 toolaunch hello Aspera 관리 포털 hello 클릭 합니다.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. Hello를 클릭 하 여 관리 링크, 필요한 toohello 등록 페이지를 얻게 됩니다 tooaccess hello 서비스입니다.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. 이 시점에서 액세스 toohello Aspera 서비스 관리 포털 수 선택 키 만들기, 다운로드 Aspera 클라이언트 및 라이선스, 사용법을 참조 하 고 있는 hello Api에 대 한 자세한 내용은 있어야 합니다.

    hello 다음 스크린샷은 hello 액세스 생성 합니다. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    hello 다음 스크린샷은 hello 사용 hello 포털에서 인터페이스를 보고 합니다. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a>Aspera를 사용하여 파일 업로드

1. 다운로드 하 고 hello Aspera 클라이언트 소프트웨어를 설치 합니다.
    
    * [브라우저 플러그 인](http://downloads.asperasoft.com/connect2/)
    * [리치 클라이언트](http://downloads.asperasoft.com/en/downloads/2)

2. 첫 번째 전송을 수행하세요. 순서 toouse hello Aspera 클라이언트 tootransfer hello Aspera 전송 서비스와, toocomplete hello 다음이 필요합니다. 

    1. Hello Aspera 포털을 사용 하는 액세스 키를 만듭니다.  
    2. 다운로드, 설치 및 라이선스 hello Aspera 클라이언트 (소프트웨어 hello Aspera 포털에서 확인할 수 있습니다).  

    >[!NOTE]
    >구성 정보에 대 한 hello Aspera 클라이언트 가이드를 참조 하십시오.
    
    3. Hello를 사용 하 여 Azure 미디어 계정와 연결 된 저장소 계정의 일부 정보를 검색할 [Azure 포털](https://portal.azure.com/)합니다. 특히, 이름 및 키 및 hello 저장소 blob 컨테이너 이름에서 toowhich 원하는 tooplace 콘텐츠입니다. 

        * hello 포털에서 tooget hello 저장소 정보: 저장소 계정의 찾을 hello 액세스 키 및 복사 사용자의 계정 이름 및 hello 키 hello 클릭 하십시오.
        * tooget hello 컨테이너 이름: 저장소 계정 선택 찾기 **Blob**선택, tooupload hello 콘텐츠를 원하는 hello 컨테이너의 hello 이름. 

    다음은 이러한 hello Aspera 클라이언트의 hello 스크린 샷 **연결 관리자** hello 'Azure' 저장소 유형 및 자격 증명으로 hello blob 컨테이너를 지정 해야 합니다.

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a>리소스

다음 리소스는 hello 된이 문서에서 설명 합니다. 

* [브라우저 플러그 인 연결](http://downloads.asperasoft.com/connect2/)
* [가이드 연결](http://downloads.asperasoft.com/en/documentation/8)
* [Aspera 클라이언트](http://downloads.asperasoft.com/en/downloads/2)
* [클라이언트 가이드](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a>다음 단계

이제 [Blob을 저장소 계정에서 AMS 계정으로 복사](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account)할 수 있습니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

