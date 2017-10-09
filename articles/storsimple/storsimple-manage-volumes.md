---
title: "aaaManage StorSimple 볼륨 | Microsoft Docs"
description: "고 tooadd, 수정, 모니터링 및 StorSimple 볼륨을 삭제 하는 방법에 대해 설명 tootake 필요한 경우 오프 라인입니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ccabd859-590c-4568-a81d-6ff38f125be3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/11/2016
ms.author: v-sharos
ms.openlocfilehash: 8dc646261ee2ad8f2b80291518716f4de55b63f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes"></a>Hello StorSimple 관리자 서비스 toomanage 볼륨을 사용 하 여
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>개요
이 자습서에서는 toouse StorSimple 관리자 서비스 toocreate hello 하 및 hello StorSimple 장치와 StorSimple 가상 장치에서 볼륨을 관리 하는 방법을 설명 합니다.

hello StorSimple Manager 서비스는 hello 단일 웹 인터페이스에서 StorSimple 솔루션을 관리할 수 있는 Azure 클래식 포털의 확장입니다. 더하기 toomanaging 볼륨에서 있습니다 수 StorSimple 관리자 서비스 toocreate hello를 사용 하 여 및 StorSimple 서비스를 관리, 보기 및 장치를 관리, 경고를 볼 및 및 보기 및 관리 백업 정책 hello 백업 카탈로그.

> [!NOTE]
> Azure StorSimple은 씬 프로비저닝된 볼륨만 만들 수 있습니다. Azure StorSimple 시스템에서 완전히 프로비전되거나 부분적으로 프로비전된 볼륨은 만들 수 없습니다.
> 
> 씬 프로비저닝는 사용 가능한 저장소 tooexceed 물리적 리소스를 표시 되는 가상화 기술입니다. 충분 한 저장소를 미리 예약 하는 대신 Azure StorSimple 사용 하 여 씬 프로 비전 tooallocate 데 충분 한 공간이 toomeet 현재 요구 합니다. 클라우드 저장소의 탄력적인 특징 hello Azure StorSimple 거 나 낮출 수 클라우드 저장소 toomeet 변화 하는 요구 하기 때문에이 방법을 지원 합니다.
> 
> 

## <a name="hello-volumes-page"></a>hello 볼륨 페이지
hello **볼륨** 페이지에서는 초기자 (서버)에 대 한 hello Microsoft Azure StorSimple 장치에서 프로 비전 되는 toomanage hello 저장소 볼륨 수 있습니다. StorSimple 장치에 볼륨 목록이 hello를 표시합니다.

 ![볼륨 페이지](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

볼륨은 다음과 같은 특성으로 구성됩니다.

* **이름** –를 설명 하는 이름을 고유 해야 하며 hello 볼륨을 식별 하는 데 도움이 됩니다. 이 이름은 특정 볼륨에 필터링하는 경우 모니터링 보고서에서도 사용됩니다.
* **상태** – 온라인 또는 오프라인 상태가 될 수 있습니다. 오프 라인 볼륨, 없는 경우 허용 되는 액세스 toouse hello 볼륨 표시 tooinitiators (서버)입니다.
* **용량** – hello 대용량 지정 hello 초기자 (서버)에서 인식 됩니다. 용량은 hello 총 hello 초기자 (서버)가 저장 될 수 있는 데이터의 양을 지정 합니다. 볼륨은 씬 프로 비전되며 데이터는 중복 제거됩니다. 이 장치에서 내부적으로 또는 hello 클라우드 tooconfigured 볼륨 용량에 따라 실제 저장소 용량 할당 미리 하지 않는 것을 의미 합니다. hello 볼륨 용량 할당 되 고 필요에 따라 사용 됩니다.
* **형식** – hello 볼륨 종류가 계층화 된 또는 보관 될 수 있습니다 (하위 형식에 계층형)
* **액세스** – toothis 볼륨 액세스를 허용 되는 hello 초기자 (서버)를 지정 합니다. Hello 볼륨와 연결 된 액세스 제어 레코드 (ACR)의 구성원이 아닌 초기자에는 hello 볼륨을 표시 되지 않습니다.
* **모니터링** – 볼륨을 모니터링 하는지 여부를 지정합니다. 볼륨이 만들어질 때 기본적으로 모니터링이 설정됩니다. 하지만 모니터링은 볼륨 클론에 대해서는 해제됩니다. 볼륨에 대 한 모니터링 tooenable 모니터 볼륨에에서 hello 지침을 따르십시오.

볼륨과 연관 hello 가장 일반적인 작업입니다.

* 볼륨 추가
* 볼륨 수정
* 볼륨 삭제
* 볼륨을 오프라인으로 전환
* 볼륨 모니터링

## <a name="add-a-volume"></a>볼륨 추가
StorSimple 솔루션 배포 중 [볼륨을 만들었습니다](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) . 볼륨 추가는 과정이 비슷합니다.

### <a name="tooadd-a-volume"></a>tooadd 볼륨
1. Hello에 **장치** 페이지 hello 장치를 선택, 두 번 클릭 하 고 클릭 hello **볼륨 컨테이너** 탭 합니다.
2. 볼륨 컨테이너를 선택 하 고 hello 해당 행 tooaccess hello와 연결 된 볼륨 hello 컨테이너에서에서 hello 화살표를 클릭 합니다.
3. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다. hello 추가 볼륨 마법사가 시작 됩니다.
   
     ![볼륨 추가 마법사 기본 설정](./media/storsimple-manage-volumes/AddVolume1.png)
4. Hello 볼륨 마법사를 아래에서 추가 **기본 설정**, 다음 hello지 않습니다.
   
   1. 볼륨의 **이름** 을 지정합니다.
   2. Hello 지정 **프로 비전 된 용량** GB 또는 TB에서 볼륨에 대 한 합니다. hello 용량 물리적 장치에 대 한 1GB ~ 64TB 사이 여야 합니다. StorSimple 가상 장치에서 볼륨에 대 한 프로 비전 할 수 있는 hello 최대 용량은 30TB를입니다.
   3. 선택 hello **사용 유형을** 볼륨에 대 한 합니다. 사용 중인 경우 hello를 선택 하면 않는 아카이브 데이터를 계층화 된 볼륨 hello **이 볼륨을 사용 하 여 자주 액세스 하지 않는 아카이브 데이터에 대 한** 확인란 볼륨에 대 한 hello 중복 제거 청크 크기를 변경 합니다. too512 (kb)입니다. 이 옵션을 선택 하지 않으면 해당 계층화 된 볼륨 hello 64KB의 청크 크기를 사용 합니다. 더 큰 중복 제거 청크 크기가 큰 않는 아카이브 데이터 toohello 클라우드의 hello 장치 tooexpedite hello 전송을 수 있습니다. (계층화 된 볼륨 기본 볼륨 이전의 되었습니다.)
   4. Hello 화살표 아이콘을 클릭 ![화살표 아이콘](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)toogo toohello **추가 설정을** 페이지.
      
        ![볼륨 추가 마법사 추가 설정](./media/storsimple-manage-volumes/AddVolume2.png)
5. **추가 설정**에서 새 ACR(액세스 제어 레코드)을 추가합니다.
   
   1. 액세스 제어 레코드 (ACR) hello 드롭 다운 목록에서 선택 합니다. 또는 새 ACR을 추가할 수 있습니다. 일치 하는 hello 하 여 볼륨에 액세스할 수 있는 호스트 Acr 결정 hello 레코드에 나열 된 IQN을 호스트 합니다.
   2. Hello를 선택 하 여 기본 백업을 사용 하도록 설정한 것이 좋습니다 **이 볼륨에 대 한 기본 백업 사용** 확인란 합니다.
   3. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-manage-volumes/HCS_CheckIcon.png) hello로 toocreate hello 볼륨 설정을 지정 합니다.

새 볼륨 toouse 준비 되었습니다.

## <a name="modify-a-volume"></a>볼륨 수정
Tooexpand 또는 hello 볼륨에 액세스 하는 호스트 hello 변경 해야 하는 경우 볼륨을 수정 합니다.

> [!IMPORTANT]
> * Hello 장치에서 hello 볼륨 크기를 수정 하면 hello 볼륨 크기 toobe hello 호스트 에서도 변경 해야 합니다.
> * 여기에 설명 된 hello 호스트 측 단계는 Windows Server 2012 (2012R2) 합니다. Linux 또는 다른 호스트 운영 체제에 대한 절차는 이와 다릅니다. 다른 운영 체제를 실행 하는 호스트의 hello 볼륨을 수정할 때 tooyour 호스트 운영 체제 지침을 참조 하십시오.
> 
> 

### <a name="toomodify-a-volume"></a>toomodify 볼륨
1. Hello에 **장치** 페이지 hello 장치를 선택, 두 번 클릭 하 고 클릭 hello **볼륨 컨테이너** 탭 합니다. 이 페이지는 hello 장치와 관련 된 모든 hello 볼륨 컨테이너가 표 형식으로 나열 됩니다.
2. 볼륨 컨테이너를 선택 하 고 hello 컨테이너 내의 모든 hello 볼륨 toodisplay hello 목록을 클릭 합니다.
3. Hello에 **볼륨** 페이지 볼륨을 선택 하 고 클릭 **수정**합니다.
4. Hello 볼륨 마법사를 아래에서 수정 **기본 설정**를 할 수 있는 hello 다음:
   
   * Hello 편집 **이름** 및 **형식** 원하는 toomodify 계층화 된 볼륨 tooan 보관 볼륨 hello를 선택 하 여 **이 볼륨을 사용 하 여 자주 액세스 하지 않는 아카이브 데이터에 대 한** 볼륨에 대 한 확인란 toochange hello 중복 제거 청크 크기 too512 (kb)입니다.
   * Hello 증가 **프로 비전 된 용량**합니다. hello **프로 비전 된 용량** 늘릴 수만 있습니다. 만든 후에는 볼륨을 축소할 수 없습니다.
     
     > [!NOTE]
     > Tooa 볼륨 할당 한 후에 hello 볼륨 컨테이너를 변경할 수 없습니다.
     > 
     > 
5. 아래 **추가 설정을**를 할 수 있는 hello 다음:
   
   * Hello 볼륨은 오프 라인 hello Acr을 수정 합니다. Tootake 해야는 hello 볼륨이 온라인 상태 이면이 오프 라인 첫 번째입니다. 참조의 toohello 단계 [볼륨을 오프 라인](#take-a-volume-offline) 이전 toomodifying hello ACR 합니다.
   * Hello 볼륨은 오프 라인 후 hello Acr 목록을 수정 합니다.
     
     > [!NOTE]
     > Hello를 변경할 수 없습니다 **이 볼륨에 대 한 기본 백업 사용** hello 볼륨에 대 한 옵션입니다.
     > 
     > 
6. Hello 확인 아이콘을 클릭 하 여 변경 내용을 저장합니다 ![check-icon](./media/storsimple-manage-volumes/HCS_CheckIcon.png)에서도 확인할 수 있습니다. hello Azure 클래식 포털에서 업데이트 볼륨 메시지를 표시 합니다. Hello 볼륨 성공적으로 업데이트 되었을 때 성공 메시지가 표시 됩니다.
7. 볼륨을 확장 하는 경우 hello Windows 호스트 컴퓨터에서 다음 단계를 완료 합니다.
   
   1. 너무 이동**컴퓨터 관리** ->**디스크 관리**합니다.
   2. **디스크 관리**를 마우스 오른쪽 단추로 클릭하고 **디스크 다시 검사**를 선택합니다.
   3. 디스크의 hello 목록에서 업데이트 된 hello 볼륨, 마우스 오른쪽 단추를 선택한 후 선택 **볼륨 확장**합니다. hello 볼륨 확장 마법사를 시작합니다. **다음**을 누릅니다.
   4. Hello 기본값을 적용 하는 hello 마법사를 완료 합니다. Hello 마법사가 완료 되 면 hello 볼륨 hello 증가 크기를 나타내야 합니다.

![동영상 사용 가능](./media/storsimple-manage-volumes/Video_icon.png) **동영상 사용 가능**

toowatch 보여 주는 비디오에서 tooexpand 볼륨을 클릭 하는 방법을 [여기](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/)합니다.

## <a name="take-a-volume-offline"></a>볼륨을 오프라인으로 전환
계획할 때 toomodify 하거나 삭제 tootake 볼륨을 오프 라인으로 작업을 할 수 있습니다 것입니다. 볼륨이 오프라인 상태인 경우 읽기 전용 액세스를 사용할 수 없습니다. Tootake hello 볼륨을 오프 hello 장치 뿐 아니라 hello 호스트 해야 합니다. Hello 단계 tootake 볼륨을 오프 라인으로 다음을 수행 합니다.

### <a name="tootake-a-volume-offline"></a>tootake 오프 라인 볼륨
1. Hello 볼륨이 오프 라인으로 전환 하기 전에 있지 않은지 확인 합니다.
2. 첫 번째 hello 호스트에서 hello 볼륨을 오프 라인입니다. 따라서 hello 볼륨에서 데이터가 손상 될 위험이 제거 됩니다. 특정 단계에 대 한 호스트 운영 체제에 대 한 toohello 지침을 참조 하십시오.
3. Hello 호스트 오프 라인 상태 이면 후 hello 다음 단계를 수행 하 여 hello 볼륨 hello 장치에 오프 라인에서 수행 합니다.
   
   1. Hello에 **장치** 페이지 hello 장치를 선택, 두 번 클릭 하 고 클릭 hello **볼륨 컨테이너** 탭 hello **볼륨 컨테이너** 모든 표 형식으로 목록 탭 hello 장치와 관련 된 hello 볼륨 컨테이너
   2. 볼륨 컨테이너를 선택 하 고 hello 컨테이너 내의 모든 hello 볼륨 toodisplay hello 목록을 클릭 합니다.
   3. 볼륨을 선택하고 **오프라인으로 전환**을 클릭합니다.
   4. 확인하라는 메시지가 표시되면 **예**를 클릭합니다. hello 볼륨 이제 오프 라인 상태 여야 합니다.
      
      볼륨이 오프 라인 상태 이면 후 hello **온라인 상태로 만들기** 옵션을 사용할 수 있습니다.

> [!NOTE]
> hello **오프 라인으로 전환** 명령은 요청 toohello 장치 tootake hello 볼륨을 오프 라인으로 보냅니다. 호스트는 hello 볼륨을 사용 하는 경우이 인해 연결이 끊어지지만된 하지만 hello 볼륨을 오프 라인 실패 하지 않습니다.
> 
> 

## <a name="delete-a-volume"></a>볼륨 삭제
> [!IMPORTANT]
> 오프라인 상태인 경우에만 볼륨을 삭제할 수 있습니다.
> 
> 

다음 단계 toodelete 볼륨 hello를 완료 합니다.

### <a name="toodelete-a-volume"></a>toodelete 볼륨
1. Hello에 **장치** 페이지 hello 장치를 선택, 두 번 클릭 하 고 클릭 hello **볼륨 컨테이너** 탭 합니다.
2. 원하는 toodelete hello 볼륨이 있는 hello 볼륨 컨테이너를 선택 합니다. Hello 볼륨 컨테이너 tooaccess hello 클릭 **볼륨** 페이지.
3. 이 컨테이너와 연결 된 모든 hello 볼륨 표 형식으로 표시 됩니다. Hello 상태를 확인 하려는 toodelete hello 볼륨의 합니다. Toodelete hello 볼륨을 오프 라인 없으면 라인 오프 라인 첫 번째, 다음 hello 단계 [볼륨을 오프 라인](#take-a-volume-offline)합니다.
4. Hello 볼륨이 오프 라인 상태 이면 클릭 **삭제** hello hello 페이지 맨 아래에 있습니다.
5. 확인하라는 메시지가 표시되면 **예**를 클릭합니다. hello 볼륨 이제 삭제 되 고 hello **볼륨** 페이지에는 업데이트 하는 hello hello 컨테이너 내의 볼륨 목록을 표시 합니다.

## <a name="monitor-a-volume"></a>볼륨 모니터링
볼륨 모니터링 toocollect 볼륨에 대 한 통계를 O 관련 있습니다. 기본적으로 hello에 대해 모니터링이 활성화를 만들면 처음 32 개 볼륨입니다. 추가 볼륨의 모니터링은 기본적으로 사용하지 않도록 설정됩니다. 복제된 볼륨의 모니터링도 기본적으로 사용하지 않도록 설정됩니다.

다음 단계 tooenable hello 하거나 볼륨에 대 한 모니터링을 사용 하지 않도록 설정 합니다.

### <a name="tooenable-or-disable-volume-monitoring"></a>볼륨 모니터링을 비활성화 또는 tooenable
1. Hello에 **장치** 페이지 hello 장치를 선택, 두 번 클릭 하 고 클릭 hello **볼륨 컨테이너** 탭 합니다.
2. hello 볼륨 상주 하는 hello 볼륨 컨테이너를 선택 하 고 클릭 hello 볼륨 컨테이너 tooaccess hello **볼륨** 페이지.
3. 이 컨테이너와 연결 된 모든 hello 볼륨 hello 표 형식의 디스플레이에 나열 됩니다. 클릭 하 고 hello 볼륨 또는 볼륨 복제본을 선택 합니다.
4. Hello hello 페이지의 아래쪽에 있는 클릭 **수정**합니다.
5. Hello 볼륨 수정 마법사에서 아래 **기본 설정**을 선택 **사용** 또는 **사용 하지 않도록 설정** hello에서 **모니터링** 드롭 다운 목록입니다.
   
    ![볼륨 기본 설정 수정](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[StorSimple 볼륨을 복제](storsimple-clone-volume.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.

