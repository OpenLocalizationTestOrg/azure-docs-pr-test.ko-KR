---
title: "StorSimple에 대 한 액세스 제어 레코드 aaaManage | Microsoft Docs"
description: "Toouse 액세스 제어 (Acr) toodetermine tooa 볼륨 hello StorSimple 장치에 연결할 수 있는 호스트를 기록 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Hello StorSimple 관리자 서비스 toomanage 액세스 제어 레코드를 사용 하 여
## <a name="overview"></a>개요
액세스 제어 레코드 (Acr) toospecify tooa 볼륨 hello StorSimple 장치에 연결할 수 있는 호스트를 허용 합니다. Acr tooa 특정 볼륨을 설정 하 고 hello iSCSI 포함 hello 호스트의 정규화 된 이름 (iqn이 포함). 호스트 tooconnect tooa 볼륨 오류 값을 hello 장치 hello ACR 해당 볼륨에 연결 된 일치 하는 경우 hello 연결이 설정 되 고 hello IQN 이름을 확인 합니다. hello 액세스 제어 레코드 섹션 hello에 **구성** hello 호스트의 iqn이 포함에 해당 하는 hello로 hello 액세스 제어 레코드를 모든 페이지에 표시 됩니다.

이 자습서에서는 일반적인 ACR 관련 작업을 수행 하는 hello를 설명 합니다.

* 액세스 제어 레코드 추가 
* 액세스 제어 레코드 편집 
* 액세스 제어 레코드 삭제 

> [!IMPORTANT]
> * ACR tooa 볼륨을 할당할 때 주의 해야이 hello 볼륨 손상 될 수 있으므로 hello 볼륨 하나 이상의 클러스터 되지 않은 호스트에서 동시에 액세스 하지 않은 합니다. 
> * 볼륨에서 ACR을 삭제할 때는 해당 호스트에서 해당 hello 하지에 액세스 하는 hello 볼륨 hello 삭제 읽기-쓰기 중단이 발생할 수 있기 때문에 있는지 확인 합니다.
> 
> 

## <a name="add-an-access-control-record"></a>액세스 제어 레코드 추가
Hello StorSimple Manager 서비스를 사용 하 여 **구성** tooadd Acr 페이지입니다. 일반적으로 하나의 볼륨으로 하나의 ACR을 연결합니다.

Hello 단계 tooadd ACR 다음을 수행 합니다.

#### <a name="tooadd-an-access-control-record"></a>tooadd 액세스 제어 레코드
1. Hello 서비스 방문 페이지에서 서비스를 선택 합니다. hello 서비스 이름을 두 번 클릭 하 고 클릭 hello **구성** 탭 합니다.
2. 아래 나열 하는 테이블 형식 hello에 **액세스 제어 레코드**지정는 **이름** ACR에 대 한 합니다.
3. Windows 호스트의 IQN 이름을 hello 제공 **iSCSI 초기자 이름**합니다. Windows Server 호스트의 IQN tooget hello 다음 hello지 않습니다.
   
   * Windows 호스트에 hello Microsoft iSCSI 초기자를 시작 합니다.
   * Hello에 **iSCSI 초기자 속성** 창의 hello에 **구성** 탭 선택 하 고 hello에서 hello 문자열을 복사 **초기자 이름** 필드입니다.
   * Hello에이 문자열을 붙여 넣습니다. **iSCSI 초기자 이름** hello Azure 클래식 포털의에서 hello Acr 테이블에 필드입니다.
4. 클릭 **저장** toosave hello 새로 ACR을 생성 합니다. hello 나열 하는 테이블 형식 될 업데이트 된 tooreflect이이 추가 됩니다.

## <a name="edit-an-access-control-record"></a>액세스 제어 레코드 편집
Hello를 사용 하 여 **구성** hello Azure 클래식 포털 tooedit Acr의에서 페이지입니다. 

> [!NOTE]
> 현재 사용하지 않고 있는 ACR만 수정할 수 있습니다. 현재 사용 중인 볼륨와 연결 된 ACR tooedit를 먼저 수행 해야 hello 볼륨 오프 라인으로.
> 
> 

Hello 단계 tooedit ACR 다음을 수행 합니다.

#### <a name="tooedit-an-access-control-record"></a>tooedit 액세스 제어 레코드
1. Hello 서비스 방문 페이지에서 서비스를 선택 합니다. hello 서비스 이름을 두 번 클릭 하 고 클릭 hello **구성** 탭 합니다.
2. Hello 액세스 제어 레코드의 테이블 형식 목록 hello에서에서 hello toomodify 하려는 ACR 가리킵니다.
3. ACR hello에 대 한 새 이름 및/또는 IQN을 제공 합니다.
4. 클릭 **저장** toosave hello ACR을 수정 합니다. hello 나열 하는 테이블 형식 업데이트 tooreflect이이 변경할 수 있습니다.

## <a name="delete-an-access-control-record"></a>액세스 제어 레코드 삭제
Hello를 사용 하 여 **구성** hello Azure 클래식 포털 toodelete Acr의에서 페이지입니다. 

> [!NOTE]
> 현재 사용하지 않고 있는 ACR만 삭제할 수 있습니다. 현재 사용 중인 볼륨와 연결 된 ACR toodelete를 먼저 수행 해야 hello 볼륨 오프 라인으로.
> 
> 

Hello 단계 toodelete 액세스 제어 레코드를 다음을 수행 합니다.

#### <a name="toodelete-an-access-control-record"></a>toodelete 액세스 제어 레코드
1. Hello 서비스 방문 페이지에서 서비스를 선택 합니다. hello 서비스 이름을 두 번 클릭 하 고 클릭 hello **구성** 탭 합니다.
2. Hello (Acr) hello 액세스 제어 레코드의 테이블 형식 목록에서 hello toodelete 하려는 ACR 가리킵니다.
3. 삭제 아이콘 (**x**) ACR 선택 하는 hello에 대 한 hello 맨 오른쪽 열에 표시 됩니다. Hello 클릭 **x** 아이콘 toodelete hello ACR 합니다.
4. 확인 메시지가 나타나면 클릭 **예** toocontinue hello 삭제 합니다. hello 테이블 형식 목록에는 업데이트 된 tooreflect hello 삭제 됩니다.

## <a name="next-steps"></a>다음 단계
* [StorSimple 볼륨 관리](storsimple-manage-volumes.md)에 대해 자세히 알아봅니다.
* 에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.

