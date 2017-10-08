---
title: "aaaManage hello StorSimple 8000 시리즈 장치에 StorSimple 볼륨 컨테이너 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스 볼륨 컨테이너 페이지 tooadd, 수정 또는 볼륨 컨테이너 삭제 hello를 사용 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a>Hello StorSimple 장치 관리자 서비스 toomanage StorSimple 볼륨 컨테이너를 사용 하 여

## <a name="overview"></a>개요
이 자습서에서는 toouse StorSimple 장치 관리자 서비스 toocreate hello 하 및 StorSimple 볼륨 컨테이너를 관리 하는 방법을 설명 합니다.

Microsoft Azure StorSimple 장치의 볼륨 컨테이너는 저장소 계정, 암호화 및 대역폭 소비 설정을 공유하는 하나 이상의 볼륨을 포함합니다. 장치는 모든 볼륨에 대해 여러 볼륨 컨테이너가 있을 수 있습니다. 

볼륨 컨테이너에는 hello 특성 뒤에 있습니다.

* **볼륨** – hello 계층 또는 로컬로 hello 볼륨 컨테이너에 포함 된 StorSimple 볼륨을 고정 합니다. 
* **암호화** -각 볼륨 컨테이너에 대해 암호화 키를 정의할 수 있습니다. 이 키는 StorSimple 장치 toohello 클라우드 보내지는 hello 데이터 암호화에 사용 됩니다. 에 군용 수준의 a e S-256 비트 키 hello 사용자가 입력 한 키로 사용 됩니다. toosecure 데이터 권장 항상 클라우드 저장소 암호화 사용 하는 합니다.
* **저장소 계정** – Azure 저장소 계정으로 사용 되는 toostore hello 데이터 hello 합니다. 볼륨 컨테이너에 있는 모든 hello 볼륨에는이 저장소 계정을 공유 합니다. 기존 목록에서 저장소 계정을 선택 하거나 hello 볼륨 컨테이너를 만들고 해당 계정에 대 한 hello 액세스 자격 증명을 지정 하는 경우 새 계정을 만들 수 있습니다.
* **클라우드 대역폭** – hello 대역폭 hello 장치가 hello hello 장치에서 전송 된 데이터 toohello 클라우드 때 사용 합니다. 이 컨테이너를 만드는 경우 1Mbps ~ 1000Mbps 사이의 값을 지정하여 대역폭 제어를 적용할 수 있습니다. 사용 가능한 모든 대역폭 hello 장치 tooconsume 하려는 경우이 필드 설정 너무**무제한**합니다. 만들고 및 일정에 따라 대역폭 템플릿 tooallocate 대역폭을 적용 수도 있습니다.

hello 다음 절차에서는 설명 방법을 toouse hello StorSimple **볼륨 컨테이너** 블레이드 toocomplete hello 일반적인 작업을 수행 합니다.

* 볼륨 컨테이너 추가
* 볼륨 컨테이너 수정
* 볼륨 컨테이너 삭제

## <a name="add-a-volume-container"></a>볼륨 컨테이너 추가
Hello 단계 tooadd 볼륨 컨테이너를 다음을 수행 합니다.

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a>볼륨 컨테이너 수정
Hello 단계 toomodify 볼륨 컨테이너를 다음을 수행 합니다.

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>볼륨 컨테이너 삭제
볼륨 컨테이너 내에 볼륨이 있습니다. 에 포함 된 모든 hello 볼륨을 먼저 삭제 되는 경우에 삭제할 수 있습니다. Hello 단계 toodelete 볼륨 컨테이너를 다음을 수행 합니다.

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a>다음 단계
* [StorSimple 볼륨 관리](storsimple-8000-manage-volumes-u2.md)에 대해 자세히 알아봅니다. 
* 에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.

