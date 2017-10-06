---
title: "aaaMicrosoft Azure StorSimple 데이터 관리자 개요 | Microsoft Docs"
description: "Hello 데이터 StorSimple Manager 서비스 (비공개 미리 보기)에 대 한 개요를 제공합니다."
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
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a>StorSimple 데이터 관리자 개요(비공개 미리 보기)

## <a name="overview"></a>개요

Microsoft Azure StorSimple 주소 hello 일반적으로 파일 공유와 관련 된 구조화 되지 않은 데이터의 복잡성을 하는 하이브리드 클라우드 저장소 솔루션입니다. StorSimple의 hello 확장 온-프레미스 솔루션 및 hello 온-프레미스 저장소와 클라우드 저장소에서 데이터를 자동으로 눈금으로 클라우드 저장소를 사용 합니다. 데이터 보호와 통합 된 로컬 및 클라우드 스냅숏, 대 한 저장소 인프라에 대 한 hello 필요성을 제거 합니다. 보관 및 재해 복구 역할을 오프 사이트 위치 hello 클라우드로 원활 하 게 이기도 합니다.

이 문서에 도입 하는 hello 데이터 변환 서비스 있습니다 tooseamlessly 액세스 hello를 StorSimple 클라우드의 데이터를 hello 수 있습니다. 이 서비스는 StorSimple에서 Api tooextract 데이터를 제공 하 고 Azure tooother 제공할 서비스를 쉽게 사용할 수 있는 형식입니다. 이 미리 보기에서 지 원하는 hello 형식은 Azure blob 및 Azure 미디어 서비스 자산입니다. 이 변환에는 StorSimple 8000 시리즈 온-프레미스 장치에서 Azure 미디어 서비스, Azure HDInsight, Azure 기계 학습 및 Azure 검색 toooperate 데이터 등의 서비스를 있습니다 tooeasily 연결할을 수 있습니다.

이를 보여 주는 높은 수준의 블록 다이어그램은 아래와 같습니다.

![높은 수준의 다이어그램](./media//storsimple-data-manager-overview/high-level-diagram.png)

이 문서에서는 이 서비스의 비공개 미리 보기에 등록할 수 있는 방법을 설명합니다. 또한 hello 클라우드에서 StorSimple 데이터 및 기타 Azure 서비스를 사용 하는이 서비스 toowrite 응용 프로그램을 사용 하는 방법을 설명 합니다.

## <a name="sign-up-for-data-manager-preview"></a>데이터 관리자 미리 보기에 등록
Hello 데이터 관리자 서비스에 등록 하기 전에 hello 다음 필수 구성 요소를 검토 합니다.

### <a name="prerequisites"></a>필수 조건

이 연습에서는 사용자에게 다음 항목이 있다고 가정합니다.
* 활성 Azure 구독
* 액세스 tooa StorSimple 8000 시리즈 장치 등록
* 모든 hello hello StorSimple 8000 시리즈 장치에 연관 된 키입니다.

### <a name="sign-up"></a>등록

StorSimple 데이터 관리자 hello 비공개 미리 보기 버전에서입니다. Hello 단계 toosign이이 서비스의 비공개 미리 보기에 대해 다음을 수행 합니다.

1.  에 로그인 hello Azure 포털에서 StorSimple Data Manager 확장 hello: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)합니다. Azure 자격 증명 toolog 프로그램을 사용 합니다.

2.  Hello 클릭  **+**  아이콘 toocreate 서비스입니다. 클릭 **저장소** 클릭 하 고 **모든 참조** 가 열리면 hello 블레이드에서 합니다.

    ![StorSimple 데이터 관리자 아이콘 검색](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. Hello StorSimple 데이터 관리자 아이콘을 표시 합니다.

    ![StorSimple 데이터 관리자 아이콘 선택](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. StorSimple 데이터 관리자 아이콘을 클릭한 다음 **만들기**를 클릭합니다. Hello 구독 tooenable hello 비공개 미리 보기를 선택 하 고 클릭 선택 **보기 등록 합니다!**

    ![등록하기](./media/storsimple-data-manager-overview/sign-me-up.png)

5. 이 전송 요청 tooonboard 있습니다. 최대한 빨리 등록하겠습니다. 구독을 사용하도록 설정한 후에 StorSimple 데이터 관리자 서비스를 만들 수 있습니다.

6. tooeasily hello 데이터 StorSimple Manager 서비스에 액세스, 별 모양 아이콘 toopin hello 클릭 것 tooyour 즐겨찾기 합니다.

    ![StorSimple 데이터 관리자에 액세스](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a>다음 단계

[데이터 tootransform StorSimple 데이터 관리자 UI를 사용 하 여](storsimple-data-manager-ui.md)합니다.
