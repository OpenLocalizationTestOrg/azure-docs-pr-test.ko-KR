---
title: "Linux 기반 HDInsight 클러스터-Azure에 대 한 aaaConfigure OS 패치 일정 | Microsoft Docs"
description: "Linux 기반 HDInsight에 대 한 tooconfigure OS 패치 일정 클러스터 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: 1598d64e594d7e8a68573fc63dd86051a5a9d025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="os-patching-for-hdinsight"></a>HDInsight의 OS 패치 
관리 되는 Hadoop 서비스로 hello HDInsight 클러스터에서 사용 하는 기본 Vm의 OS hello 패치 HDInsight 담당 합니다. 2016 년 8 월 1 일을 기준으로 하는 Linux 기반 HDInsight 클러스터 (버전 3.4 이상)에 대 한 hello 게스트 OS 패치 정책을 변경 했습니다. hello hello 새 정책의 ´ ֲ ° toosignificantly 재부팅 hello 횟수를 줄이는 due toopatching 합니다. 새 정책 hello toopatch linux 가상 컴퓨터 (Vm)는 모든 월요일 또는 목요일 오전 12 시 UTC 시차를 두고 진행 방식에서에서 시작 하 여 어떤 특정된 클러스터의 노드에서 클러스터 계속 됩니다. 그러나 지정 된 모든 VM 최대 30 일 마다 tooguest OS 패치 인해만 다시 부팅 됩니다. 또한 새로 만들어진된 클러스터에 대 한 첫 번째 다시 부팅 hello hello 클러스터를 만든 날짜 로부터 30 일 보다 자주 발생 하지 않습니다. 패치는 hello Vm 다시 부팅 되 면 적용 됩니다.

## <a name="how-tooconfigure-hello-os-patching-schedule-for-linux-based-hdinsight-clusters"></a>Tooconfigure는 Linux 기반 HDInsight 클러스터에 대 한 OS 패치 일정 hello 하는 방법
HDInsight 클러스터에서 가상 컴퓨터 hello toobe 중요 한 보안 패치를 설치할 수 있도록 경우에 따라 다시 부팅 필요 합니다. 2016 년 8 월 1 일을 기준으로 일정에 따라 hello를 사용 하 여 새 Linux 기반 HDInsight 클러스터 (버전 3.4 이상) 재부팅 됩니다.

1. Hello 클러스터에서 가상 컴퓨터만 다시 부팅할 수 패치에 대 한 최대 30 일 기간 내에 한 번입니다.
2. hello 재부팅 발생 오전 12 시 UTC부터 시작 합니다.
3. hello 다시 부팅 프로세스 hello 다시 부팅 프로세스 중 hello 클러스터는 계속 사용할 수 있도록 hello 클러스터의 가상 컴퓨터에서 지연 됩니다.
4. 새로 만들어진된 클러스터에 대 한 첫 번째 다시 부팅 hello hello 클러스터를 만든 날짜 후 30 일 보다 자주 발생 하지 않습니다.

이 문서에 설명 된 hello 스크립트 작업을 사용 하 여 hello OS 패치 일정을 다음과 같이 수정할 수 있습니다.
1. 자동 다시 부팅 사용 또는 사용 안 함
2. Hello 경과한 후 재부팅 (재부팅 사이 일)
3. 다시 부팅 하는 hello 주의 hello 요일 설정

> [!NOTE]
> 2016년 8월 1일 이후에 만들어진 Linux 기반 HDInsight 클러스터에서만 이 스크립트 작업이 작동합니다. VM이 다시 부팅되는 경우에만 패치가 적용됩니다. 
>

## <a name="how-toouse-hello-script"></a>Toouse 스크립트 hello 하는 방법 

이 스크립트를 사용 하 여 필요한 경우 다음 정보는 hello:
1. 스크립트 위치 hello: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh 합니다.  이 URI toofind를 사용 하 여 hello 클러스터의 모든 hello 가상 컴퓨터에서 hello 스크립트를 실행 하는 HDInsight.
  
2. hello hello 스크립트에 적용 되는 클러스터 노드 형식: 헤드 노드에, workernode, 사육 합니다. 이 스크립트는 hello 클러스터에 적용 된 tooall 노드 형식 이어야 합니다. 이 아닌 경우 적용 된 tooa 노드 유형 가상 hello toouse hello 이전 패치 일정 노드 형식에 대 한 컴퓨터에 계속 됩니다.


3.  매개 변수: 이 스크립트는 세 가지 숫자 매개 변수를 수락합니다.

    | 매개 변수를 포함해야 합니다. | 정의 |
    | --- | --- |
    | 자동 다시 부팅 사용/사용 안 함 |0 또는 1입니다. 0 값은 자동 다시 부팅을 사용하지 않는 반면 1은 자동 다시 부팅을 해제합니다. |
    | Frequency(빈도) |7 too90 (포함)입니다. 다시 부팅 해야 하는 패치를 hello 가상 컴퓨터를 다시 부팅 하기 전에 일 toowait hello 수입니다. |
    | 요일 |1 too7 (포함)입니다. 1 값 hello 다시 부팅 한 월요일에 발생 해야 하며 매개 변수를 사용 하 여 Sunday.For 예제에서는 값의 1 60 2 결과를 자동 재부팅 60 일 마다 (최대) 화요일에 배포 합니다. |
    | 지속성 |스크립트 동작 tooan 기존 클러스터를 적용할 때 유지 hello 스크립트를 표시할 수 있습니다. 지속형된 스크립트는 새 workernodes 작업 크기 조정을 통해 toohello 클러스터에 추가 될 때 적용 됩니다. |

> [!NOTE]
> 유지 tooan 기존 클러스터를 적용할 때이 스크립트를 표시 해야 합니다. 그렇지 않으면 작업 크기 조정을 통해 만든 모든 새 노드 hello 기본 일정을 패치를 사용 합니다.
Hello 클러스터를 만드는 프로세스의 일부로 hello 스크립트를 적용 하는 경우 자동으로 유지 됩니다.
>

## <a name="next-steps"></a>다음 단계

Hello 다음 hello에 대 한 섹션을 참조 하는 hello 스크립트 동작을 사용 하 여에 특정 단계 [스크립트 동작을 사용 하 여 사용자 지정 Linuz 기반 HDInsight 클러스터](hdinsight-hadoop-customize-cluster-linux.md):

* [클러스터를 만드는 동안 스크립트 작업 사용](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [클러스터를 실행 하는 스크립트 작업 tooa 적용](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
