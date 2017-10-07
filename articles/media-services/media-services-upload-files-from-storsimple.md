---
title: "Azure StorSimple에서 Azure 미디어 서비스 계정으로 aaaUpload 파일 | Microsoft Docs"
description: "이 문서에서는 Azure StorSimple 데이터 관리자를 간략하게 설명합니다. hello 문서는 방법을 보여 주는 tootutorials 링크도 StorSimple에서 tooextract 데이터 자산 tooan Azure 미디어 서비스 계정으로 업로드 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a>Azure StorSimple의 Azure Media Services 계정에 파일 업로드

이 문서에서는 Azure StorSimple 데이터 관리자를 간략하게 설명합니다. hello 문서는 방법을 보여 주는 tootutorials 링크도 StorSimple에서 tooextract 데이터 자산 tooan Azure 미디어 서비스 (AMS) 계정으로이 데이터를 업로드 합니다.

> 
> [!NOTE]
> 현재 Azure StorSimple 데이터 관리자는 비공개 미리 보기 상태입니다. 
> 

## <a name="overview"></a>개요

미디어 서비스에서 자산에 디지털 파일을 업로드합니다. 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 닫힌된 캡션 파일 (및 이러한 파일에 대 한 hello 메타 데이터) hello 자산 포함 될 수 있습니다. Hello 파일 업로드 되 면 콘텐츠 추가 처리 및 스트리밍에 대 한 hello 클라우드에 안전 하 게 저장 됩니다.

[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) hello의 확장 온-프레미스 솔루션 고 hello 온-프레미스 저장소와 클라우드 저장소에서 데이터를 자동으로 눈금 클라우드 저장소를 사용 합니다. hello StorSimple 장치 dedupes 및 큰 파일 toohello 클라우드를 보내기 위한 매우 효율적으로 만드는 toohello 클라우드를 보내기 전에 데이터를 압축 합니다. hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) 서비스는 StorSimple의 있습니다 tooextract 데이터를 사용 하 고 AMS 자산으로 제공 하는 Api를 제공 합니다.

## <a name="get-started"></a>시작

1. [미디어 서비스 계정 만들기](media-services-portal-create-account.md) 넣을 tootransfer hello 자산입니다.
2. Hello에 설명 된 대로 데이터 관리자 미리 보기에 등록 [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) 문서.
3. StorSimple 데이터 관리자 계정을 만듭니다.
4. 데이터 변환 작업을 실행할 때 만들고 StorSimple 장치에서 데이터를 추출하고 AMS 계정에 자산으로 전송합니다. 

    Hello 작업 실행을 시작할 때 저장소 큐 생성 됩니다. 이 큐는 준비가 완료된 변환 Blob에 대한 메시지로 채워집니다. 이 큐의 hello 이름 hello 작업 정의의 hello 이름과 달라 서 hello 됩니다. 이 큐 toodetermine를 사용할 수 있습니다 때 자산 그대로 준비를 호출 하 여 원하는 미디어 서비스 작업 toorun 것입니다. 예를 들어이 큐 tootrigger hello 필요한 미디어 서비스 코드에 있는 Azure 함수를 사용할 수 있습니다.

## <a name="see-also"></a>참고 항목

[사용 하 여.Net SDK hello hello 데이터 관리자에서에서 tootrigger 작업](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>다음 단계

이제 업로드된 자산을 인코딩할 수 있습니다. 자세한 내용은 [자산 인코딩](media-services-portal-encode.md)을 참조하세요.
