---
title: "StorSimple에서 액세스 제어 레코드 관리 | Microsoft Docs"
description: "ACR(액세스 제어 레코드)을 사용하여 어떤 호스트가 StorSimple 장치의 볼륨에 연결할 수 있는지 지정하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: a87624b5706c1d9b8c2b9926e5580996a89ce984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a>StorSimple 관리자 서비스를 사용하여 액세스 제어 레코드 관리
## <a name="overview"></a>개요
ACR(액세스 제어 레코드)을 사용하면 어떤 호스트가 StorSimple 장치의 볼륨에 연결할 수 있는지 지정할 수 있습니다. ACR은 특정 볼륨으로 설정되며 호스트의 IQN(iSCSI 정규화된 이름)을 포함합니다. 호스트가 볼륨에 연결하려고 할 때 해당 장치는 IQN 이름에 대한 볼륨과 연결된 ACR을 확인하고 일치하는 경우 이 연결이 확정됩니다. **구성** 페이지의 액세스 제어 레코드를 섹션은 호스트의 해당 IQN으로 모든 액세스 제어 레코드를 표시합니다.

이 자습서에서는 다음과 같은 일반적인 ACR 관련 작업을 설명합니다.

* 액세스 제어 레코드 추가 
* 액세스 제어 레코드 편집 
* 액세스 제어 레코드 삭제 

> [!IMPORTANT]
> * 볼륨에 ACR을 할당할 때 이 볼륨을 손상시킬 수 있으므로 하나 이상의 클러스터되지 않은 호스트에서 동시에 액세스하지 않은 볼륨에 주의를 기울여야 합니다. 
> * 볼륨에서 ACR을 삭제할 때 삭제로 인해 읽기-쓰기 중단이 발생할 수 있기 때문에 해당 호스트가 볼륨에 액세스하지 않는지 확인해야 합니다.
> 
> 

## <a name="add-an-access-control-record"></a>액세스 제어 레코드 추가
StorSimple 관리자 서비스 **구성** 페이지를 사용하여 ACR을 추가합니다. 일반적으로 하나의 볼륨으로 하나의 ACR을 연결합니다.

ACR을 추가하려면 다음 단계를 수행합니다.

#### <a name="to-add-an-access-control-record"></a>액세스 제어 레코드를 추가하려
1. 서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성** 탭을 클릭합니다.
2. **액세스 제어 레코드** 아래 테이블 형식 목록에서 ACR에 대한 **이름**을 지정합니다.
3. **iSCSI 초기자 이름**에서 Windows 호스트의 IQN 이름을 제공합니다. Windows Server 호스트의 IQN을 가져오려면 다음을 수행합니다.
   
   * Windows 호스트에서 Microsoft iSCSI 초기자를 시작합니다.
   * **iSCSI 초기자 속성** 창의 **구성** 탭에서 **초기자 이름** 필드의 문자열을 선택하고 복사합니다.
   * Azure 클래식 포털에 있는 ACR 표의 **iSCSI 초기자 이름** 필드에 이 문자열을 붙입니다.
4. **저장** 을 클릭하여 새로 만들어진 ACR을 저장합니다. 테이블 형식 목록이 이 추가 사항을 반영하도록 업데이트됩니다.

## <a name="edit-an-access-control-record"></a>액세스 제어 레코드 편집
Azure 클래식 포털의 **구성** 페이지에서 ACR을 편집합니다. 

> [!NOTE]
> 현재 사용하지 않고 있는 ACR만 수정할 수 있습니다. 현재 사용 중인 볼륨과 연관된 ACR을 편집하려면 먼저 볼륨을 오프라인으로 전환해야 합니다.
> 
> 

ACR을 편집하려면 다음 단계를 수행합니다.

#### <a name="to-edit-an-access-control-record"></a>액세스 제어 레코드를 편집하려면
1. 서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성** 탭을 클릭합니다.
2. 액세스 제어 레코드의 테이블 형식 목록에서 수정하려는 ACR 위로 커서를 가져갑니다.
3. ACR의 새 이름 및/또는 IQN을 제공합니다.
4. **저장** 을 클릭하여 수정된 ACR을 저장합니다. 테이블 형식 목록이 이 변경 내용을 반영하도록 업데이트됩니다.

## <a name="delete-an-access-control-record"></a>액세스 제어 레코드 삭제
Azure 클래식 포털의 **구성** 페이지에서 ACR을 삭제합니다. 

> [!NOTE]
> 현재 사용하지 않고 있는 ACR만 삭제할 수 있습니다. 현재 사용 중인 볼륨과 연관된 ACR을 삭제하려면 먼저 볼륨을 오프라인으로 전환해야 합니다.
> 
> 

액세스 제어 레코드를 삭제하려면 다음 단계를 수행합니다.

#### <a name="to-delete-an-access-control-record"></a>액세스 제어 레코드를 삭제하려면
1. 서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성** 탭을 클릭합니다.
2. ACR(액세스 제어 레코드)의 테이블 형식 목록에서 삭제하려는 ACR 위로 커서를 가져갑니다.
3. 삭제 아이콘(**x**)이 선택한 ACR의 맨 오른쪽 열에 표시됩니다. **x** 아이콘을 클릭하여 ACR을 삭제합니다.
4. 확인 메시지가 나타나면 **예** 를 클릭하여 삭제를 계속합니다. 테이블 형식 목록이 삭제를 반영하도록 업데이트됩니다.

## <a name="next-steps"></a>다음 단계
* [StorSimple 볼륨 관리](storsimple-manage-volumes.md)에 대해 자세히 알아봅니다.
* [StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.

