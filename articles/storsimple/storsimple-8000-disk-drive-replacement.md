---
title: "StorSimple 8000 시리즈 장치에 디스크 드라이브 aaaReplace | Microsoft Docs"
description: "StorSimple 기본 인클로저 또는 EBOD 인클로저 tooreplace 디스크 드라이브 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: 09c1bf5e97adf54a609a868e921351bc63e00a83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a>StorSimple 8000 시리즈 장치의 디스크 드라이브 교체

## <a name="overview"></a>개요
이 자습서에서는 Microsoft Azure StorSimple 장치에서 오작동하거나 오류가 발생한 하드 디스크 드라이브를 꺼내고 교체하는 방법을 설명합니다. 디스크 드라이브 tooreplace 해야합니다.

* Hello 변조 방지 잠금 해제
* Hello 디스크 드라이브를 제거 합니다.
* Hello 대체 디스크 드라이브를 설치 합니다.

> [!IMPORTANT]
> 제거 하 고 디스크 드라이브의 교체에 hello 보안 정보를 검토 하기 전에 [StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)합니다.
 

## <a name="disengage-hello-antitamper-lock"></a>Hello 변조 방지 잠금 해제
어떻게 StorSimple 장치에 대 한 hello 변조 방지 잠금을 수 설정 또는 해제 hello 디스크 드라이브를 교체 하는 경우이 절차에 설명 합니다. hello 변조 방지 잠금은 hello 드라이브 캐리어 핸들에 맞추는 고 hello 핸들의 래치 섹션 hello에에서 있는 작은 구멍을 통해 액세스 됩니다. 드라이브는 hello 잠금 세트 toohello 잠긴 위치와 함께 제공 됩니다.

#### <a name="toounlock-hello-antitamper-lock"></a>toounlock hello 변조 방지 잠금
1. Hello 핸들에 hello 구멍에 및 해당 소켓에 조심 스럽게 hello 잠금 키 (Microsoft에서 제공한 "변조 방지" T10 드라이버)를 삽입 합니다. 
   
   Hello 변조 방지 잠금이 활성화 되 면 hello에 빨간색 표시기 hello 구멍에 표시 됩니다.
  
    ![잠긴 디스크 드라이브](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    **그림 1** 조작 방지 잠금 사용
   
   | 레이블 | 설명 |
   |:--- |:--- |
   | 1 |표시기 입구 |
   | 2 |조작 방지 잠금 |
2. Hello에 빨간색 표시기가 hello 키 위의 구멍 hello에에서 표시 되지 않을 때까지 반대 방향으로 돌립니다에 hello 키를 회전 합니다.
3. Hello 키를 제거 합니다.
   
    ![잠금 해제된 디스크 드라이브](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    **그림 2** 잠금 해제된 디스크 드라이브
4. 이제 hello 디스크 드라이브를 제거할 수 있습니다.

역방향 tooengage hello 잠금의 hello 단계를 수행 합니다.

## <a name="remove-hello-disk-drive"></a>Hello 디스크 드라이브를 제거 합니다.
StorSimple 장치는 RAID 10과 유사한 저장소 공간 구성을 지원합니다. 이는 오류가 발생한 하나의 디스크, SSD(반도체 드라이브) 또는 HDD(하드 디스크 드라이브)에서 정상적으로 작동할 수 있음을 의미합니다.

> [!IMPORTANT]
> * 시스템에 둘 이상의 실패 한 디스크를 제거 하지 마십시오 둘 이상의 SSD 또는 HDD 언제 든 지 hello 시스템에서 시간. 이렇게 하면 데이터가 손실될 수 있습니다.
> * 이전에 SSD가 포함된 슬롯에는 교체 SSD를 넣어야 합니다. 마찬가지로, 이전에 HDD가 포함된 슬롯에는 교체 HDD를 넣습니다.
> * Azure 포털 hello 슬롯 0 – 번호는 11입니다. 따라서 hello 포털 hello 장치에서 슬롯 2의에서 디스크에 오류가 표시 되 면 hello hello 세 번째 슬롯에서 오류가 발생 한 디스크에서에서 찾습니다 hello 창의 상단 왼쪽.
> 
> 

드라이브를 제거 하 고 hello 시스템 작동 하는 동안 대체 될 수 있습니다.

#### <a name="tooremove-a-drive"></a>tooremove 드라이브
1. tooidentify hello 이동 tooyour 장치 hello Azure 포털에서에서 디스크 실패 **설정 > 하드웨어 상태가**합니다. 디스크에서 hello 기본 인클로저 및/또는 EBOD 인클로저 (8600 모델을 사용 하는 경우) 하는 경우 실패할 수 있습니다, 때문에 아래 hello 디스크의 hello 상태 확인 **공유 구성 요소** 고 **EBOD 공유 구성 요소** . 엔클로저 중 하나에서 오류가 발생한 디스크는 빨간색 상태로 표시됩니다.
2. Hello 기본 인클로저 또는 EBOD 인클로저의 hello hello 앞에서 hello 드라이브를 찾습니다. 
3. Hello 디스크가 잠금 해제 된 경우 toohello 다음 단계를 진행 합니다. Hello 디스크 잠겨 있으면 잠금을 해제할 hello 절차에 따라 [hello 변조 방지 잠금 해제](#disengage-the-antitamper-lock)합니다.
4. 키를 눌러 hello 검정 hello 드라이브 캐리어 모듈에 대 한 래치 및 hello 섀시 hello 앞에서 끌어오기 hello 드라이브 캐리어 핸들이 자리를 비울 / 로그 아웃 합니다.
   
    ![디스크 드라이브 핸들 해제](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    **그림 3** hello 드라이브 핸들 해제
5. Hello 드라이브 캐리어 핸들이 완전히 확장 하는 경우에 hello 드라이브 캐리어를 hello 섀시 밖으로 밉니다. 
   
    ![디스크 드라이브 밖으로 디스크 밀기](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    **그림 4** 슬라이딩 hello carrier hello 디스크 드라이브

## <a name="install-hello-replacement-disk-drive"></a>Hello 대체 디스크 드라이브를 설치 합니다.
StorSimple 장치에는 드라이브에 오류가 발생 한 후 제거 했기 프로시저 tooreplace이에 따라 새 드라이브로 것입니다.

#### <a name="tooinsert-a-drive"></a>tooinsert 드라이브
1. 다음 이미지는 hello와 같이 hello 드라이브 캐리어 핸들이 완전히 확장을 확인 합니다.
   
    ![핸들이 확장된 디스크 드라이브](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    **그림 5** 핸들이 확장된 드라이브
2. Hello 드라이브 캐리어를 모든 hello 방식으로 hello 섀시 밀어넣습니다.
   
    ![디스크 드라이브 캐리어 안으로 디스크 밀기](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    **그림 6** hello 섀시 안으로 슬라이딩 hello 드라이브 캐리어
3. Hello 드라이브 캐리어 삽입, 닫기 hello 드라이브 캐리어 핸들이 hello 드라이브 캐리어 핸들이 잠긴된 위치에 고정 될 때까지 hello 섀시에 계속 toopush hello 드라이브 캐리어 하는 동안와.
4. 제공한 Microsoft (변조 방지 Torx 드라이버) toosecure hello 캐리어 핸들에 설정 하 여 잠금 나사 hello는 1/4 시계 반대 방향으로 사용 하 여 hello 잠금 키입니다.
5. Hello 교체에 성공 했 고 hello 드라이브 작동 하는지 확인 합니다. Hello Azure 포털 액세스 하 고 너무 탐색**설정** > **하드웨어 상태가**합니다. 아래 **공유 구성 요소** 또는 **EBOD 공유 구성 요소**, hello 드라이브 상태가 정상 인지를 나타내는 녹색으로 바뀝니다.
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > 소요 몇 시간 정도 hello 디스크 상태 tooturn 녹색 hello 교체 후 합니다.
  
## <a name="next-steps"></a>다음 단계
[StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에 대해 자세히 알아봅니다.

