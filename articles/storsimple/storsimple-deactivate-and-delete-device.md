---
title: "aaaDeactivate StorSimple 장치를 삭제 하 고 | Microsoft Docs"
description: "설명 방법을 tooremove StorSimple 장치에서 서비스를 먼저 비활성화 한 후이 삭제 합니다."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a>StorSimple Manager 서비스를 통해 StorSimple 8000 시리즈 장치 비활성화 및 삭제
## <a name="overview"></a>개요
(예를 들어 교체 하거나 장치를 업그레이드 하는 경우 또는 StorSimple 더 이상 사용 하는 경우) 서비스에서 StorSimple 장치 tootake을 지정할 수 없습니다. Hello 대/소문자 이면 toodeactivate hello 장치를 삭제 하기 전에 해야 합니다. Hello 장치와 StorSimple Manager 서비스를 해당 하는 hello hello 연결을 서버를 비활성화 합니다. 이 자습서에 설명 방법을 tooremove 먼저 비활성화 및 삭제 하 여 서비스에서 StorSimple 장치입니다. 

장치를 비활성화 하면 hello 장치에서 로컬로 저장 된 모든 데이터는 더 이상 액세스할 수 없습니다. Hello 클라우드에 저장 된 hello 장치와 연결 된 hello 데이터만 복구할 수 있습니다.  

> [!WARNING]
> 비활성화는 영구 작업이며 실행 취소할 수 없습니다. 비활성화 된 장치는 먼저 toohello 출하 시 기본 설정 다시 설정 하지 않은 hello StorSimple Manager 서비스에 등록할 수 없습니다. 
> 
> hello 공장 기본 장치에서 로컬로 저장 된 모든 hello 데이터 프로세스 삭제를 설정 합니다. 따라서 반드시 장치를 비장치를 비활성화하기 전에 모든 데이터의 클라우드 스냅숏을 만들어야 합니다. 이렇게 하면 toorecover 이후 단계에서 데이터를 hello 모든 합니다.
> 
> 

이 자습서에서는 다음을 수행하는 방법을 설명합니다.

* 장치를 비활성화 하 고 hello 데이터 삭제
* 장치를 비활성화 하 고 hello 데이터 보존

StorSimple 가상 장치에서 비활성화 및 삭제가 어떻게 작동하는지도 설명합니다.

> [!NOTE]
> StorSimple 물리적 또는 가상 장치를 비활성화 하기 전에 toostop 있는지 확인 하거나 클라이언트와 해당 장치에 종속 된 호스트를 삭제 합니다.
> 
> 

## <a name="deactivate-and-delete-data"></a>데이터 비활성화 및 삭제
Hello 장치를 완전히 삭제 하 고 hello 장치에 tooretain hello 데이터 하지 않을 경우 다음 단계를 수행 하는 hello를 완료 합니다.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate hello 장치 및 delete hello 데이터
1. 이전 toodeactivating 장치, 모든 hello 볼륨 컨테이너 (및 hello 볼륨) hello 장치와 연결 된 삭제 해야 합니다. 연결 된 hello 백업을 삭제 한 후에 볼륨 컨테이너를 삭제할 수 있습니다.
2. 다음과 같이 hello 장치를 비활성화 합니다.
   
   1. Hello StorSimple Manager 서비스에서 **장치** 페이지, 선택 hello 장치 toodeactivate 원하는, hello 페이지의 맨 아래 hello에 클릭 **비활성화**합니다.
   2. 확인 메시지가 표시됩니다. 클릭 **예** toocontinue 합니다. hello 비활성화 프로세스가 시작 되 고 몇 분 toocomplete 수행 합니다.
3. 비활성화 한 후 hello 장치를 완전히 삭제할 수 있습니다. 장치 삭제 장치 toohello 연결 된 서비스의 hello 목록에서 제거 됩니다. 그런 다음 hello 서비스 삭제 hello 장치를 더 이상 관리할 수 없습니다. 다음 단계 toodelete hello 장치 hello를 사용 합니다.
   
   1. Hello StorSimple Manager 서비스에서 **장치** 페이지에서 원하는 toodelete 비활성화 된 장치를 선택 합니다.
   2. Hello hello 페이지 아래쪽에서 클릭 **삭제**합니다.
   3. 확인하라는 메시지가 표시됩니다. 클릭 **예** toocontinue 합니다.
      
      삭제 하는 hello 장치 toobe 몇 분 정도 걸릴 수 있습니다.

## <a name="deactivate-and-retain-data"></a>데이터 비활성화 및 보존
관심 있는 hello 장치를 삭제 해도 tooretain hello 데이터를 원하는 경우 다음 단계를 수행 하는 hello를 완료 합니다.

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>장치 toodeactivate hello 데이터를 유지 합니다.
1. Hello 장치를 비활성화 합니다. 모든 볼륨 컨테이너를 hello 및 hello 장치의 hello 스냅숏은 유지 됩니다.
   
   1. Hello StorSimple Manager 서비스에서 **장치** 페이지, 선택 hello 장치 toodeactivate 원하는, hello 페이지의 맨 아래 hello에 클릭 **비활성화**합니다.
   2. 확인 메시지가 표시됩니다. 클릭 **예** toocontinue 합니다. hello 비활성화 프로세스가 시작 되 고 몇 분 toocomplete 수행 합니다.
2. 이제 hello 볼륨 컨테이너와 연결 된 hello 스냅숏을 조치할 수 있습니다. 너무 절차를 보려면[StorSimple 장치에 대 한 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다.
3. 비활성화 및 장애 조치 후 hello 장치를 완전히 삭제할 수 있습니다. 장치 삭제 장치 toohello 연결 된 서비스의 hello 목록에서 제거 됩니다. 그런 다음 hello 서비스 삭제 hello 장치를 더 이상 관리할 수 없습니다. 다음 단계 toodelete hello 장치 hello를 완료 합니다.
   
   1. Hello StorSimple Manager 서비스에서 **장치** 페이지에서 원하는 toodelete 비활성화 된 장치를 선택 합니다.
   2. Hello hello 페이지 아래쪽에서 클릭 **삭제**합니다.
   3. 확인하라는 메시지가 표시됩니다. 클릭 **예** toocontinue 합니다.
      
      삭제 하는 hello 장치 toobe 몇 분 정도 걸릴 수 있습니다.

## <a name="deactivate-and-delete-a-virtual-device"></a>가상 장치 비활성화 및 삭제
StorSimple 가상 장치에 대 한 비활성화 hello 가상 컴퓨터를 할당 취소 합니다. 그런 다음 hello 가상 컴퓨터 및 프로 비전 된 경우 생성 된 hello 리소스를 삭제할 수 있습니다. Hello 가상 장치를 비활성화 한 후 수 없습니다 tooits 이전 상태로 복원 합니다. 

작업을 수행 하는 hello에 비활성화 결과:

* hello StorSimple 가상 장치 제거 됩니다.
* hello OSDisk 및 hello StorSimple 가상 장치에 대해 생성 된 데이터 디스크 제거 됩니다.
* hello 호스 티 드 서비스 및 가상 네트워크를 프로 비전 중에 만들어진 유지 됩니다. 이러한 엔터티를 사용하지 않는 경우 수동으로 삭제해야 합니다.
* Hello StorSimple 가상 장치에서 만든 클라우드 스냅숏은 유지 됩니다.

## <a name="next-steps"></a>다음 단계
* toorestore 비활성화 된 장치 toofactory 기본값 hello, 너무 이동[hello 장치 toofactory 기본 설정으로 초기화](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)합니다.
* 기술 지원을 받으려면 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)하세요.
* toouse hello StorSimple Manager 서비스 너무 이동 하는 방법에 대해 더 알아봅니다을 toolearn[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다. 

