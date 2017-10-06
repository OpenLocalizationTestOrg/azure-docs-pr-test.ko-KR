---
title: "StorSimple 8000 시리즈 장치에 섀시 aaaReplace | Microsoft Docs"
description: "Tooremove 및 바꾸기 StorSimple 기본 인클로저 또는 EBOD 인클로저 섀시 hello 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a>StorSimple 장치에 hello 섀시 교체
## <a name="overview"></a>개요
이 자습서에 설명 어떻게 tooremove StorSimple 8000 시리즈 장치에 섀시를 바꿉니다. StorSimple 8100 hello 모델 반면 hello 8600 이중 인클로저 장치 (두 개의 섀시)는 단일 인클로저 장치 (하나의 섀시)은입니다. 8600 모델의 경우는 hello 장치에서 장애 사용할 수 있는 두 개의 섀시 잠재적으로: hello 기본 인클로저의 섀시 또는 EBOD 인클로저의 hello에 대 한 hello 섀시 hello 합니다.

어떤 경우 든 Microsoft에서 제공 되는 hello 교체 섀시 비어 있습니다. PCM(전원 및 냉각 모듈), 컨트롤러 모듈, SSD(반도체 디스크 드라이브), HDD(하드 디스크 드라이브) 또는 EBOD 모듈은 포함되지 않습니다.

> [!IMPORTANT]
> 분리 및 교체 hello 섀시 hello 보안 정보를 검토 하기 전에 [StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)합니다.
> 
> 

## <a name="remove-hello-chassis"></a>Hello 섀시를 제거 합니다.
Hello 단계 tooremove hello 섀시 StorSimple 장치에서 다음을 수행 합니다.

#### <a name="tooremove-a-chassis"></a>tooremove 섀시
1. Hello StorSimple 장치 종료 되 고 모든 hello 전원에서 연결이 해제 되어 있는지 확인 합니다.
2. 해당 하는 경우 모든 hello 네트워크 및 SAS 케이블을 제거 합니다.
3. Hello 랙에서 hello 단위를 제거 하십시오.
4. 각 hello 드라이브를 제거 하 고 제거 되는 hello 슬롯을 기록해 둡니다. 자세한 내용은 참조 [hello 디스크 드라이브를 제거](storsimple-disk-drive-replacement.md#remove-the-disk-drive)합니다.
5. Hello EBOD 인클로저 (hello 발생 한 섀시 인 경우), hello EBOD 컨트롤러 모듈을 제거 합니다. 자세한 내용은 [EBOD 컨트롤러 꺼내기](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller)를 참조하세요. 
   
    Hello에 기본 인클로저 (hello 발생 한 섀시 인 경우) hello 컨트롤러를 제거 하 고 확인 hello 슬롯 제거 됩니다. 자세한 내용은 [컨트롤러 꺼내기](storsimple-controller-replacement.md#remove-a-controller)를 참조하세요.

## <a name="install-hello-chassis"></a>Hello 섀시를 설치 합니다.
Hello 단계 tooinstall hello 섀시 StorSimple 장치에서 다음을 수행 합니다.

#### <a name="tooinstall-a-chassis"></a>tooinstall 섀시
1. Hello 섀시 hello 랙에 탑재 합니다. 자세한 내용은 [StorSimple 8100 장치 랙 탑재](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) 또는 [StorSimple 8600 장치 랙 탑재](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device)를 참조하세요.
2. Hello 섀시, hello 랙에 탑재 한 후에 이전에 설치한에 배치 동일 hello hello 컨트롤러 모듈을 설치 합니다.
3. 설치 hello는 이전에 설치한에 배치 하 고 슬롯이 동일한 hello에서 구동 합니다.
   
   > [!NOTE]
   > Hello Ssd hello 슬롯을 먼저 설치 하 고 다음 hello Hdd를 설치 하는 것이 좋습니다.
   > 
   > 
4. Hello 사용 hello 랙에 장치 탑재 및 hello 구성 요소를 설치 하 고, 사용자 장치 toohello 적절 한 전원에 연결 하 고 hello 장치를 켭니다. 자세한 내용은 [StorSimple 8100 장치 케이블 연결](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) 또는 [StorSimple 8600 장치 케이블 연결](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device)을 참조하세요.

## <a name="next-steps"></a>다음 단계
[StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)에 대해 자세히 알아봅니다.

