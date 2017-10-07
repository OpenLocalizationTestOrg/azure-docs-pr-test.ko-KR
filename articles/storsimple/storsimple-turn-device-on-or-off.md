---
title: "aaaTurn StorSimple 8000 시리즈 장치를 끄거나 | Microsoft Docs"
description: "새 StorSimple 장치에 tooturn 종료 되었거나 전원, 분실 된 장치의 설정 및 실행 중인 장치 끄기 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85434bde9377e330cd6ba4797fd5fd68bcee944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a>StorSimple 8000 시리즈 장치 켜기 또는 끄기
## <a name="overview"></a>개요
Microsoft Azure StorSimple 장치 종료는 정상적인 시스템 작업의 일환으로 필요하지 않습니다. 그러나 새 장치 또는 장치 종료 toobe를 tooturn을 할 수 있습니다. 일반적으로 오류가 발생한 하드웨어를 교체, 물리적으로 장치를 이동하거나 장치의 서비스를 중단해야 하는 경우 종료가 필요합니다. 이 자습서를 하 고 다양 한 시나리오에서 StorSimple 장치를 종료 hello 필요한 절차를 설명 합니다.

## <a name="turn-on-a-new-device"></a>새 장치 켜기
hello hello에 대 한 StorSimple 장치 처음 켜는 단계에 따라 다릅니다 hello 장치는 8100 인지 또는 8600 모델. 8100 hello는 hello 8600는 기본 인클로저와 EBOD 인클로저가 있는 이중 인클로저 장치 하는 반면는 단일 기본 인클로저가 있습니다. hello 두 모델에 대 한 자세한 단계에에서 나와 hello 다음 섹션.

* [기본 인클로저만 있는 새 장치](#new-device-with-primary-enclosure-only)
* [EBOD 인클로저가 있는 새 장치](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a>기본 인클로저만 있는 새 장치
StorSimple 8100 hello 모델은 단일 인클로저 장치입니다. 장치에는 예비 전원 및 냉각 모듈(PCM)이 포함됩니다. 두 Pcm을 설치 해야 toodifferent 전원 소스 tooensure 높은 가용성을 연결 합니다.

전원에 대 한 hello 단계 toocable 다음 장치를 수행 합니다.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> 장치 설정 완료 및 지침 케이블 연결에 대 한 이동 너무[StorSimple 8100 장치 설치](storsimple-8100-hardware-installation.md)합니다. Hello 지침을 정확 하 게 수행 하 고 있는지 확인 합니다.
> 
> 

### <a name="new-device-with-ebod-enclosure"></a>EBOD 인클로저가 있는 새 장치
StorSimple 8600 hello 모델에는 기본 인클로저와 EBOD 인클로저 둘 다에 있습니다. 그러려면 hello 단위 toobe SCSI SAS (Serial Attached) 연결 및 전원에 대해 함께 케이블로 연결 합니다.

을 설정할 때 hello에 대 한이 장치를 처음으로 먼저 SAS 케이블 연결 및 전원 케이블 연결에 대 한 다음 전체 hello 단계에 대 한 hello 단계를 수행 합니다.

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> 장치 설정 완료 및 지침 케이블 연결에 대 한 이동 너무[8600 StorSimple 장치 설치](storsimple-8600-hardware-installation.md)합니다. Hello 지침을 정확 하 게 수행 하 고 있는지 확인 합니다.

## <a name="turn-on-a-device-after-shutdown"></a>종료 후 장치 켜기
StorSimple 장치를 종료 한 후 켜는 hello 단계 hello 장치는 8100 인지 또는 8600 모델에 따라 달라 집니다. 8100 hello는 hello 8600는 기본 인클로저와 EBOD 인클로저가 있는 이중 인클로저 장치 하는 반면는 단일 기본 인클로저가 있습니다.

* [기본 인클로저만 있는 장치](#device-with-primary-enclosure-only)
* [EBOD 인클로저가 있는 장치](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a>기본 인클로저만 있는 장치
종료 한 후에 나오는 기본 인클로저와 EBOD 인클로저는 없는 사용 하 여 StorSimple 장치에 따라 프로시저 tooturn hello를 사용 합니다.

#### <a name="tooturn-on-a-device-with-a-primary-enclosure-only"></a>기본 인클로저만 있는 장치에 tooturn
1. 두 전원으로 전환 하는 hello 전원 및 냉각 모듈 (Pcm) hello OFF 위치에 있는지 확인 합니다. Hello 스위치 hello OFF 위치에 없으면 다음 대칭 이동할 toohello OFF 위치 및 lights toogo hello에 대 한 대기 해제 합니다.
2. Hello 전원 스위치를 두 Pcm toohello ON 위치로 전환 하 여 hello 장치를 켭니다. hello 장치가 켜져야 합니다.
3. 다음 장치 hello tooverify 검사 hello가 완전히 켜 졌:
   
   1. 두 PCM 모듈에 hello OK Led가 녹색입니다.
   2. 두 컨트롤러에서 hello 상태 led가 녹색으로 켜져 있습니다.
   3. hello hello 컨트롤러 중 하나의 파란색 LED가 깜박입니다 해당 hello 컨트롤러가 활성 상태임을 나타냅니다.
      
      이러한 조건 중 하나라도 충족되지 않은 경우 장치가 정상이 아닙니다. [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)하세요.

### <a name="device-with-ebod-enclosure"></a>EBOD 인클로저가 있는 장치
종료 한 후에 기본 인클로저와 EBOD 인클로저 StorSimple 장치의 프로시저 tooturn 다음 hello를 사용 합니다. 설명한대로 정확하게 각 단계를 순서대로 수행합니다. 따라서 실패 toodo 데이터가 손실 될 수 있습니다.

#### <a name="tooturn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a>기본 인클로저와 EBOD 인클로저가 있는 장치에 tooturn
1. 해당 hello EBOD 인클로저가 기본 인클로저에 연결 된 toohello 인지 확인 합니다. 자세한 내용은 [StorSimple 8600 장치 설치](storsimple-8600-hardware-installation.md)를 참조하세요.
2. 해당 hello 전원 있는지 확인 하 고 둘 다에서 냉각 모듈 (Pcm) hello EBOD 및 기본 인클로저 hello OFF 위치에 있습니다. Hello 스위치 hello OFF 위치에 없으면 다음 대칭 이동할 toohello OFF 위치 및 lights toogo hello에 대 한 대기 해제 합니다.
3. Hello EBOD 인클로저를 먼저 설정 hello 전원 스위치를 두 Pcm toohello ON 위치로 전환 하 여 합니다. hello PCM led가 녹색 이어야 합니다. 이 장치의 녹색 EBOD 컨트롤러 LED hello EBOD 인클로저가 켜져 있는지 나타냅니다.
4. Hello 전원 스위치를 두 Pcm toohello ON 위치로 전환 하 여 hello 기본 인클로저를 켭니다. hello 전체 시스템에 있어야 합니다.
5. 통해 해당 hello 연결 hello EBOD 인클로저 사이 hello SAS Led가 녹색, 기본 인클로저 hello 양호 확인 합니다.

## <a name="turn-on-a-device-after-a-power-loss"></a>전원 손실 후 장치 켜기
정전 또는 전원 중단으로 StorSimple 장치가 종료될 수 있습니다. hello 정전 hello 전원 공급 장치 중 하나 또는 두 전원 공급 장치 모두에서 발생할 수 있습니다. hello 복구 단계는 hello 장치는 8100 인지 또는 8600 모델에 따라 다릅니다. 8100 hello는 hello 8600는 기본 인클로저와 EBOD 인클로저가 있는 이중 인클로저 장치 하는 반면는 단일 기본 인클로저가 있습니다. 이 섹션에서는 각 시나리오에 대 한 hello 복구 절차를 설명 합니다.

* [기본 인클로저만 있는 장치](#8100)
* [EBOD 인클로저가 있는 장치](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a>기본 인클로저만 있는 장치 <a name="8100">
전원 공급 장치 중 전원 손실 tooone 이면 hello 시스템은 일반적인 작업을 계속 수 있습니다. 그러나 복원 전원 toohello hello 장치의 고가용성 tooensure 전원 공급 장치 최대한 빨리 합니다.

정전이 나 전원 공급 장치 모두에서 정전 있으면 hello 시스템 순차적이 고 제어 된 방식으로 종료 됩니다. Hello 전원이 복원 hello 시스템은 자동으로 설정 됩니다.

### <a name="device-with-ebod-enclosure-a-name8600"></a>EBOD 인클로저가 있는 장치 <a name="8600">
#### <a name="power-loss-on-one-power-supply"></a>하나의 전원 공급 장치에서 전원 손실
hello 기본 인클로저 또는 EBOD 인클로저의 hello에 전원 공급 장치 중 전원 손실 tooone 이면 hello 시스템은 일반적인 작업을 계속 수 있습니다. 그러나 tooensure 고가용성의 hello 장치를 복원 하십시오 전원 toohello 전원 공급 장치 최대한 빨리.

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a>기본 및 EBOD 인클로저의 두 전원 공급 장치에서 전원 손실
전원 공급 장치 모두에서 전원 정전이 나 전원 공급 있으면 hello EBOD 인클로저에서 즉시 종료 하 고 hello 기본 인클로저는 순차적이 고 제어 된 방식으로 종료 됩니다. 전원이 복원 hello 기기 자동으로 시작 됩니다.

Hello 전원이 꺼진 수동으로 경우 다음 단계 toorestore 전원 toohello 시스템 hello를 고려 합니다.

1. Hello EBOD 인클로저를 켭니다.
2. EBOD 인클로저 hello에 되 면 hello 기본 인클로저를 켭니다.

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a>EBOD 인클로저의 두 전원 공급 장치에서 전원 손실
케이블을 설치할 때 EBOD은 해당 hello 연결 만으로 tooa 확인 해야 PDU 구분 합니다. 기본 인클로저 및 EBOD hello hello에 실패 하는 경우 동일한 시간 hello 시스템이 복구 됩니다.

Hello EBOD 인클로저의 두 전원 공급 장치에서 실패 하면만 hello 시스템은 자동으로 복구 되지 않습니다. Hello 단계 tooturn hello 시스템에 다음을 수행 하 고 tooa 정상 상태로 복원:

1. Hello 기본 인클로저가 켜져 있으면 전원 및 냉각 모듈 (Pcm) 모두 해제 합니다.
2. 아래로 시스템 tooshut hello에 대 일 분 정도 기다립니다.
3. Hello EBOD 인클로저를 켭니다.
4. EBOD 인클로저 hello에 되 면 hello 기본 인클로저를 켭니다.

## <a name="turn-on-a-device-after-hello-primary-and-ebod-enclosure-connection-is-lost"></a>장치 사용 hello 후 기본 및 EBOD 인클로저 연결이 손실 됩니다.
Hello 연결이 hello 대기 컨트롤러와 해당 EBOD 컨트롤러 hello 사이의 인 경우 hello 장치 toowork를 계속 합니다. Hello 시스템 활성 컨트롤러와 해당 EBOD 컨트롤러 hello 간의 hello 연결이 손실 된 경우 장애 조치를 실행 하 고 hello 장치 toowork 정상적으로 계속 합니다.

연결 된 SAS (Serial SCSI) 케이블이 모두 분리 되거나 EBOD 인클로저 hello 및 hello 기본 인클로저 간의 hello 연결이 끊어지면, hello 장치 작동이 중지 됩니다. 이 시점에서 hello 다음 단계를 수행 합니다.

### <a name="tooturn-on-hello-device-after-connection-is-lost"></a>연결이 끊어진 후 hello 장치의 tooturn
1. Hello 장치의 후면 hello 액세스 합니다.
2. Hello hello EBOD 인클로저와 hello 기본 인클로저 간의 SAS 케이블 연결 중단 된 경우 hello EBOD 인클로저의 모든 SAS 레인 led가 꺼집니다.
3. Hello EBOD 인클로저와 기본 인클로저 hello에 전원 및 냉각 모듈 (Pcm) 모두를 종료 합니다.
4. Hello 두 hello 인클로저 후면의 모든 hello 표시등 해제할 때까지 기다립니다.
5. Hello SAS 케이블을 다시 삽입 하 고 hello EBOD 인클로저와 기본 인클로저 hello 간의 제대로 연결 되어 있는지 확인 합니다.
6. Hello EBOD 인클로저를 먼저 설정 두 PCM 스위치 toohello ON 위치로 전환 하 여 합니다.
7. Hello EBOD 인클로저 hello 녹색 LED가 ON 켜져 확인 합니다.
8. Hello 기본 인클로저를 켭니다.
9. 기본 인클로저 hello hello 컨트롤러의 녹색 LED가 켜져 있는지 확인 하 여 켜져 확인 합니다.
10. 해당 hello hello 기본 인클로저를 EBOD 인클로저 연결이 좋은 검사 하 여가 해당 hello SAS 레인 Led (EBOD 컨트롤러당 4 개)에 모두 확인 합니다.

> [!IMPORTANT]
> Hello SAS 케이블에 결함이 있거나 hello hello EBOD 인클로저 및 hello 기본 인클로저 간의 연결이 양호 하지 hello 시스템 설정 하면, 복구 모드로 전환 됩니다. 이 경우 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 하십시오.


## <a name="turn-off-a-running-device"></a>실행 중인 장치 끄기
실행 중인 StorSimple 장치 toobe 해야 이동 하는 서비스를 받지 못하게 하거나 오작동 구성 요소가 toobe 교체 해야 하는 경우 종료 합니다. hello 단계 hello StorSimple 장치는 8100 인지 또는 8600 모델에 따라 달라 집니다. 8100 hello는 hello 8600는 기본 인클로저와 EBOD 인클로저가 있는 이중 인클로저 장치 하는 반면는 단일 기본 인클로저가 있습니다. 이 섹션에는 실행 중인 장치 아래로 hello 단계 tooshut 자세히 설명합니다.

* [기본 인클로저가 있는 장치](#8100a)
* [EBOD 인클로저가 있는 장치](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a>기본 인클로저가 있는 장치 <a name="8100a">
질서 있고 제어 되는 방식 hello 장치 아래로 tooshut를 할 수 있는 것 hello Azure 클래식 포털 또는 hello Windows PowerShell을 통해 StorSimple에 대 한 합니다. 

> [!IMPORTANT]
> 종료 하지 마세요 실행 중인 장치 hello hello 장치의 후면에서 hello 전원 단추를 사용 하 여 합니다.
> 
> Hello 장치를 종료 하기 전에 모든 hello 장치 구성 요소가 올바르게 작동 하는지 확인 합니다. Hello Azure 클래식 포털에서 탐색 너무**장치** > **유지 관리** > **하드웨어 상태**, 모든 hello의 해당 상태를 확인 하 고 구성 요소는 녹색입니다. 양호한 시스템에 대해서만 적용됩니다. Hello 시스템이 종료 하 tooreplace 오작동 구성 요소, 오류 (빨간색) 나타납니다 또는 성능 저하 (노란색) 상태 hello에 각 구성 요소의 hello에 대 한 **하드웨어 상태**합니다.
> 
> 

Hello Windows PowerShell for StorSimple 또는 hello Azure 클래식 포털에 액세스 한 후 hello 단계에 따라 [StorSimple 장치를 종료](storsimple-manage-device-controller.md#shut-down-a-storsimple-device)합니다. 

### <a name="device-with-ebod-enclosure-a-name8600a"></a>EBOD 인클로저가 있는 장치 <a name="8600a">
> [!IMPORTANT]
> Hello 기본 인클로저 및 EBOD 인클로저의 hello 종료 하기 전에 모든 hello 장치 구성 요소가 정상 상태 인지 확인 합니다. Hello Azure 포털에서 탐색 너무**장치** > **모니터** > **하드웨어 상태가**, 모든 hello 구성 요소가 정상 상태 인지 확인 합니다.


#### <a name="tooshut-down-a-running-device-with-ebod-enclosure"></a>EBOD 인클로저가 있는 실행 중인 장치 아래로 tooshut
1. 에 나열 된 모든 hello 단계에 따라 [StorSimple 장치를 종료](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) 기본 인클로저 hello에 대 한 합니다.
2. 이후에 hello 기본 인클로저는 종료, 전원 및 냉각 모듈 (PCM) 모두 스위치 꺼서 EBOD hello를 종료 합니다.
3. EBOD hello tooverify 종료, hello EBOD 인클로저의 후면 hello에 불 모든 확인이 해제 되어 있습니다.

> [!NOTE]
> hello 시스템 종료 된 후까지 사용 되는 tooconnect hello EBOD 인클로저 toohello 기본 인클로저는 hello SAS 케이블을 제거할 수 없음.

## <a name="next-steps"></a>다음 단계
[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) 하십시오.

