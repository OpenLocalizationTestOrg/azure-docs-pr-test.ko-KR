---
title: "aaaAzure 클라우드 셸 (미리 보기) 제한 사항 | Microsoft Docs"
description: "Azure Cloud Shell의 제한 사항 개요"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Azure Cloud Shell의 제한 사항
Azure 클라우드 셸에 hello 다음과 같은 알려진 제한 사항:

## <a name="system-state-and-persistence"></a>시스템 상태 및 지속성
클라우드 셸 세션을 제공 하는 hello 컴퓨터는 일시적 이며 재활용 되는 세션이 비활성화 된 후 20 분 동안 합니다. 클라우드 셸 탑재 하는 파일 공유 toobe가 필요 합니다. 결과적으로, 구독을 저장소 리소스 tooaccess 클라우드 셸 수 tooset 이어야 합니다. 기타 고려 사항은 다음과 같습니다.
* 탑재된 저장소에서 `$Home` 디렉터리 또는 `clouddrive` 디렉터리 내 수정 사항만 유지됩니다.
* 파일 공유는 [할당된 지역](persisting-shell-storage.md#mount-a-new-clouddrive) 내에서만 탑재될 수 있습니다.
* Azure 파일은 로컬 중복 저장소 및 지역 중복 저장소 계정만 지원합니다.

## <a name="user-permissions"></a>사용자 권한
권한은 sudo 액세스 권한이 없는 일반 사용자로 설정됩니다. 사용자 `$Home` 디렉터리 외부에서의 설치는 유지되지 않습니다.
내에서 특정 명령을 hello 있지만 `clouddrive` 디렉터리와 같은 `git clone`, 적절 한 권한 없는 사용자 `$Home` 디렉터리에 권한이 합니다.

## <a name="browser-support"></a>브라우저 지원
클라우드 셸 hello Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox 및 Apple Safari의 최신 버전을 지원합니다. Safari는 개인 모드에서 지원되지 않습니다.

## <a name="copy-and-paste"></a>복사 및 붙여넣기
Ctrl + C 및 Ctrl + V 복사/붙여넣기 바로 가기 클라우드 셸에서 Windows 컴퓨터에서 Ctrl + Insert 및 Shift + Insert toocopy를 사용 하 고 각각 붙여 대로 작동 하지 않습니다.

오른쪽 클릭 복사-붙여넣기 옵션도 사용할 수 있지만 마우스 오른쪽 단추 클릭 함수는 주체 toobrowser 특정 클립보드 액세스 합니다.

## <a name="editing-bashrc"></a>.bashrc 편집
.bashrc를 편집할 때는 Cloud Shell에 예기치 않은 오류가 발생할 수 있으니 주의하세요.

## <a name="bashhistory"></a>.bash_history
Cloud Shell 세션 중단 또는 동시 세션으로 인해 bash 명령의 기록이 일관되지 않을 수 있습니다.

## <a name="usage-limits"></a>사용 제한
Cloud Shell은 대화형 사용 사례를 위한 것입니다. 따라서 비대화형 세션을 오래 실행하면 경고 없이 종료됩니다.

## <a name="network-connectivity"></a>네트워크 연결
클라우드 셸에서 대기 시간 주체 toolocal 인터넷에 연결을 클라우드 셸은 모든 명령 전송 tooattempt toocarry 계속 됩니다.

## <a name="next-steps"></a>다음 단계
[Cloud Shell 빠른 시작](quickstart.md)
