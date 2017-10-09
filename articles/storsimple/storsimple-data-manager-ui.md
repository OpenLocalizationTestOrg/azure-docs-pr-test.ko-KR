---
title: Azure StorSimple Data Manager UI aaaMicrosoft | Microsoft Docs
description: "설명 방법을 toouse 데이터 StorSimple 관리자 서비스 UI (비공개 미리 보기)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a>Hello 데이터 StorSimple Manager 서비스 UI (비공개 미리 보기)를 사용 하 여 관리

이 문서에서는 hello StorSimple 8000 시리즈 장치에 있는 데이터에 StorSimple Data Manager UI tooperform 데이터 변환 hello를 사용 하는 방법을 설명 합니다. hello 변환 된 데이터가 다음에서 사용할 수 Azure 미디어 서비스, Azure HDInsight, Azure 기계 학습 및 Azure 검색 등 다른 Azure 서비스입니다. 


## <a name="use-storsimple-data-transformation"></a>StorSimple 데이터 변환 사용

hello StorSimple 데이터 관리자는 hello 리소스는 데이터 변환을 인스턴스화할 수 있습니다. 데이터 변환 서비스 hello를 사용 하면 Azure 저장소에 StorSimple 온-프레미스 장치 tooblobs 프로그램에서 데이터를 이동할 수 있습니다. 따라서 워크플로에서 toospecify hello 세부 정보에 대해 필요한 toomove toohello 저장소 계정 관심 StorSimple 장치와 hello 데이터입니다.

### <a name="create-a-storsimple-data-manager-service"></a>StorSimple 데이터 관리자 서비스 만들기

Hello 단계 toocreate 데이터 StorSimple Manager 서비스를 다음을 수행 합니다.

1. 데이터 StorSimple 관리자 서비스 toocreate 너무 이동[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)

2. Hello 클릭  **+**  아이콘과 StorSimple 데이터 관리자에 대 한 검색 합니다. StorSimple 데이터 관리자 서비스를 클릭한 다음 **만들기**를 클릭합니다.

3. 구독을 하도록 구성 되어이 서비스를 만드는 다음 블레이드 hello를 표시 됩니다.

    ![StorSimple 데이터 관리자 리소스 만들기](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. Hello 입력을 입력 하 고 클릭 **만들기**합니다. hello 지정 위치 hello 저장소 계정 및 StorSimple Manager 서비스를 저장 하는 하나 여야 합니다. 현재 미국 서부 및 유럽 서부에서만 지원됩니다. 따라서 StorSimple Manager 서비스, 데이터 관리자 서비스 및 hello 연결 된 저장소 계정 모두 hello 위의 지원 영역에 있어야 합니다. 분 toocreate hello 서비스에 대 한 필요합니다.

### <a name="create-a-data-transformation-job-definition"></a>데이터 변환 작업 정의 만들기

데이터 StorSimple 관리자 서비스 내에서 toocreate 데이터 변환 작업 정의 해야합니다. 작업 정의 hello 네이티브 형식에서 저장소 계정에 이동 하 여 관심 있는 hello 데이터의 세부 정보를 지정 합니다. 

Hello 단계 toocreate 새 데이터 변환 작업 정의 다음을 수행 합니다.

1.  Toohello 만든 서비스를 이동 합니다. **+작업 정의**를 클릭합니다.

    ![+작업 정의 클릭](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. hello 새 작업 정의 블레이드를 엽니다. 작업 정의에 이름을 지정하고 **원본**을 클릭합니다. Hello에 **구성 데이터 원본** 블레이드에서 StorSimple 장치의 hello 세부 정보를 지정 하 고 관심 있는 데이터를 hello 합니다.

    ![작업 정의 만들기](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. 새 데이터 관리자 서비스이기 때문에 데이터 리포지토리가 구성되지 않습니다. tooadd을 데이터 저장소로 StorSimple Manager 클릭 **새로 추가** 데이터 저장소 드롭다운 hello와 클릭 **데이터 저장소 추가**합니다.

4. 선택 **StorSimple 8000 시리즈 관리자** hello 저장소로 입력 하 고 hello 속성을 입력 하면 **StorSimple Manager**합니다. Hello에 대 한 **리소스 Id** tooenter hello 번호 hello 하기 전에 필요한 필드 **:** StorSimple manager의 hello 등록 키에 있습니다.

    ![데이터 원본 만들기](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  완료되면 **확인**을 클릭합니다. 이렇게 하면 데이터 리포지토리를 절약하고 이러한 매개 변수를 다시 입력하지 않고 다른 작업 정의에서 이 StorSimple Manager를 다시 사용할 수 있습니다. 클릭 한 후 몇 초 **확인** hello 드롭다운에서 StorSimple Manager tooshow hello에 대 한 합니다.

6.  Hello에 **구성 데이터 원본** 블레이드에서 hello 장치 이름을 입력 하 고 hello 관심 있는 데이터에 있는 볼륨 이름입니다.

7.  Hello에 **필터** 하위 섹션에서 관심 있는 데이터를 포함 하는 hello 루트 디렉터리를 입력 (로 시작 해야이 필드는 `\`). 여기에서 파일 필터를 추가할 수 있습니다.

8.  hello 데이터 변환 서비스 toohello Azure 통해 스냅숏이 푸시됩니다 hello 데이터에서 작동 합니다. 이 작업을 실행할 때 선택할 수 있습니다 tootake 백업 될 때마다 (최신 데이터에 대해 toowork)를 실행 되는이 작업 또는 toouse hello hello 클라우드의 마지막 기존 백업을 (보관 된 일부 데이터에서 작업 하는) 하는 경우.

    ![새 데이터 원본 세부 정보](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. 다음으로 hello 대상 설정 구성 toobe가 필요 합니다. 지원되는 대상에는 Azure Storage 계정 및 Azure Media Services 계정이라는 두 가지 유형이 있습니다. 해당 계정에 blob을 저장소 계정 tooput 파일을 선택 합니다. 해당 계정에 자산에 미디어 서비스 계정 tooput 파일을 선택 합니다. 다시, tooadd 리포지토리가 필요합니다. Hello 드롭다운에서 선택 **새로 추가** 차례로 **설정을 구성**합니다.

    ![데이터 싱크 만들기](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. 여기에서는 hello 유형의 저장소 tooadd 및 hello hello 리포지토리와 연결 된 다른 매개 변수를 선택할 수 있습니다. 두 경우 모두 저장소 큐 hello 작업이 실행 될 때 만들어집니다. 이 큐는 준비가 완료된 변환 Blob에 대한 메시지로 채워집니다. 이 큐의 hello 이름 hello 작업 정의의 hello 이름과 달라 서 hello 됩니다. 선택 하는 경우 **미디어 서비스** hello 리포지토리 유형으로 다음을 입력할 수도 있습니다 저장소 계정 자격 증명 hello 큐를 만들 위치입니다.

    ![새 데이터 싱크 세부 정보](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. (적용 하는 몇 초 정도) hello 데이터 저장소를 추가한 후 hello에 hello 드롭다운에서에서 hello 리포지토리를 찾을 수 있습니다 **대상 계정 이름이**합니다.  필요한 hello 대상을 선택 합니다.

12. 클릭 **확인** toocreate hello 작업 정의 합니다. 이제 작업 정의가 설정되었습니다. 이 작업 정의 hello UI 통해 여러 번 사용할 수 있습니다.

    ![새 작업 정의 추가](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a>Hello 작업 정의 실행 합니다.

Tooinvoke 해야는 hello 작업 정의에 지정 된 StorSimple toohello 저장소 계정에서 toomove 데이터를 할 것입니다. Hello 작업을 호출할 때마다 hello 매개 변수 변경에 더 일부 유연성을 제공 합니다. hello 단계는 다음과 같습니다.

1. 데이터 StorSimple Manager 서비스를 선택 하 고 너무 이동**모니터링**합니다. **지금 실행**을 클릭합니다.

    ![작업 정의 트리거](./media/storsimple-data-manager-ui/run-now.png)

2. Hello 작업 정의 선택 toorun 되도록 합니다. 클릭 **실행 설정** toomodify이이 작업 실행에 대해 toochange 수도 있는 모든 설정 합니다.

    ![작업 설정 실행](./media/storsimple-data-manager-ui/run-settings.png)

3. 클릭 **확인** 클릭 하 고 **실행** toolaunch 작업 합니다. toomonitor이 작업을 이동 toohello **작업** 프로그램 StorSimple 데이터 관리자의 페이지입니다.

    ![작업 목록 및 상태](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. Hello에 더하기 toomonitoring에서 **작업** 블레이드에서 있습니다도에서 수신할 수 hello 저장소 큐 StorSimple toohello 저장소 계정에서 파일을 이동 될 때마다 메시지가 추가 합니다.


## <a name="next-steps"></a>다음 단계

[.NET SDK toolaunch StorSimple Data Manager 작업을 사용 하 여](storsimple-data-manager-dotnet-jobs.md)합니다.
