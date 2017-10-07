---
title: "aaaUpgrade HDInsight 클러스터 tooa 최신 버전이-Azure | Microsoft Docs"
description: "어떻게 tooUpgrade HDInsight 클러스터 tooa 최신 버전에 알아봅니다."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a>HDInsight 클러스터 tooa 새 버전 업그레이드
tootake 활용 hello 최신 HDInsight 기능, HDInsight 클러스터 업그레이드 toolatest 버전 것이 좋습니다. HDInsight 클러스터 버전이 아래 지침 tooupgrade hello를 따릅니다.

> [!NOTE]
> HDInsight 클러스터 버전 3.2 및 3.3은 곧 사용이 중단될 예정입니다. 지원되는 HDInsight 버전에 대한 자세한 내용은 [HDInsight 구성 요소 버전](hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.
>
>

## <a name="upgrade-tasks"></a>업그레이드 작업
hello 워크플로 tooupgrade HDInsight 클러스터는 다음과 같습니다.

![업그레이드 워크플로 다이어그램](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. HDInsight 클러스터를 업그레이드 하는 경우 필요할 수 있는 toounderstand 변경 내용을이 문서의 각 섹션을 읽습니다.
2. 클러스터를 테스트/품질 보증 환경으로 만듭니다. 클러스터를 만드는 방법에 대 한 자세한 내용은 참조 하세요. [어떻게 toocreate Linux 기반 HDInsight 클러스터에 대해 알아봅니다](hdinsight-hadoop-provision-linux-clusters.md)
3. 기존 작업, 데이터 원본 및 싱크 toohello 새 환경 복사본입니다. 참조 [데이터 복사 tooTest 환경](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) 내용을 확인 합니다.
4. Toomake 작업 hello 새 클러스터에서 예상 대로 작동 하는지 테스트 하는 유효성 검사를 수행 합니다.


예상 대로 작동 하는 것을 확인 한 후 hello 마이그레이션에 대 한 가동 중지 시간을 예약 합니다. 이 작동 중단이 시간 동안 다음 작업 hello지 않습니다.

1.  Hello 클러스터 노드에서 로컬에 저장 된 임시 데이터를 백업 합니다. 예를 들어 헤드 노드에 직접 저장된 데이터가 있는 경우입니다.
2.  Hello 기존 클러스터를 삭제 합니다.
3.  클러스터 만들기 hello에 동일한 기본 데이터 저장소에 사용 되는 이전 클러스터 hello hello VNET 최신 (또는 지원 되는) 서브넷 HDI 버전 사용 하 여 동일한 합니다. 이렇게 하면 hello 새 클러스터 toocontinue 기존 프로덕션 데이터에 대해 작동 합니다.
4.  백업한 모든 임시 데이터를 가져옵니다.
5.  시작 작업/계속 hello 새 클러스터를 사용 하 여 처리 합니다.

## <a name="next-steps"></a>다음 단계
* [어떻게 toocreate Linux 기반 HDInsight 클러스터에 대해 알아봅니다](hdinsight-hadoop-provision-linux-clusters.md)
* [TooHDInsight SSH를 사용 하 여 연결](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Ambari를 사용하여 Linux 기반 클러스터 관리](hdinsight-hadoop-manage-ambari.md)

