---
title: "aaaPublish HDInsight 응용 프로그램-Azure | Microsoft Docs"
description: "자세한 내용은 방법 toocreate HDInsight 응용 프로그램을 게시 합니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7da0aa53828563e50ef372df901e1ba541fb40be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a>Azure 마켓플레이스 hello에 HDInsight 응용 프로그램 게시
HDInsight 응용 프로그램은 Linux 기반 HDInsight 클러스터에 사용자가 설치할 수 있는 응용 프로그램입니다. Microsoft, ISV(독립 소프트웨어 공급 업체) 또는 사용자가 직접 이러한 응용 프로그램을 개발할 수 있습니다. 이 문서에서는 설명 어떻게 toopublish hello Azure 마켓플레이스로 HDInsight 응용 프로그램입니다.  Hello Azure 마켓플레이스에서 게시에 대 한 일반 정보를 참조 하십시오. [제공 toohello Azure 마켓플레이스에서 게시](../marketplace-publishing/marketplace-publishing-getting-started.md)합니다.

HDInsight 응용 프로그램 사용 hello *Bring Your 자체 라이선스 (BYOL)* 여기서 응용 프로그램 공급자는 hello 응용 프로그램 tooend-사용자, 라이선스 해야 하 고 최종 사용자만 Azure에서에 부과 hello 리소스는 모델에서 hello HDInsight 클러스터와 해당 Vm/노드가 같은 만듭니다. 현재, 자체 hello 응용 프로그램에 대 한 청구 Azure를 통해 수행 되지 않습니다.

다른 HDInsight 응용 프로그램 관련 문서:

* [HDInsight 응용 프로그램을 설치](hdinsight-apps-install-applications.md): tooinstall HDInsight 응용 프로그램 tooyour 클러스터 하는 방법에 대해 알아봅니다.
* [사용자 지정 HDInsight 응용 프로그램을 설치](hdinsight-apps-install-custom-applications.md): 자세한 방법을 tooinstall 및 테스트 사용자 지정 HDInsight 응용 프로그램입니다.

## <a name="prerequisites"></a>필수 조건
toosubmit 사용자 지정 응용 프로그램 toohello 마켓플레이스를 만들고를 사용자 지정 응용 프로그램을 테스트 해야 합니다. Hello 다음 문서를 참조 하십시오.

* [사용자 지정 HDInsight 응용 프로그램을 설치](hdinsight-apps-install-custom-applications.md): 자세한 방법을 tooinstall 및 테스트 사용자 지정 HDInsight 응용 프로그램입니다.

또한 개발자 계정을 등록했어야 합니다. 참조 [제공 toohello Azure 마켓플레이스에서 게시](../marketplace-publishing/marketplace-publishing-getting-started.md) 및 [Microsoft 개발자 계정을 만들려면](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)합니다.

## <a name="define-application"></a>응용 프로그램 정의
응용 프로그램 toohello Azure 마켓플레이스에서 게시 하기 위한 관련 된 두 단계가 있습니다.  먼저 정의 **createUiDef.json** 응용 프로그램 클러스터는 파일 tooindicate;와 호환 되 고 hello Azure 포털에서에서 hello 서식 파일을 게시 합니다. 다음 섹션 hello 샘플 createUiDef.json 파일입니다.

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| 필드 | 설명 | 가능한 값 |
| --- | --- | --- |
| types |hello 응용 프로그램와 호환 되는 hello 클러스터 유형입니다. |Hadoop, HBase, Storm, Spark(또는 이들의 조합) |
| tiers |hello 응용 프로그램와 호환 되는 hello 클러스터 계층입니다. |Standard, Premium(또는 둘 다) |
| versions |hello 응용 프로그램와 호환 되는 hello HDInsight 클러스터 유형입니다. |3.4 |

## <a name="application-install-script"></a>응용 프로그램 설치 스크립트
응용 프로그램이 설치 될 때마다 (기존 또는 새) 클러스터에서 가장자리 노드 만들어지고 hello 응용 프로그램 설치 스크립트에서 실행 됩니다.
  > [!IMPORTANT]
  > hello 응용 프로그램 설치 스크립트 이름이의 hello 이름 형식에 따라 hello로 특정 클러스터에 대 한 고유 해야 합니다.
  > 
  > name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"
  > 
  > 여기에 메모는 세 부분 toohello 스크립트 이름:
  > 
  > 1. 스크립트 이름 접두사-hello 응용 프로그램 이름 또는 이름 toohello 관련 응용 프로그램을 포함 합니다.
  > 2. 가독성을 위한 "-".
  > 3. 매개 변수를 hello hello 응용 프로그램 이름 사용 하는 고유 문자열 함수입니다.
  > 
  > 예로 위의 hello 결국 되 고: 색상-설치-v0-4wkahss55hlas hello에 지속형 스크립트 동작 목록입니다. 샘플 JSON 페이로드는 [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json)를 참조하세요.
  > 
hello 설치 스크립트에 다음 특징 hello가 있어야 합니다.
1. Hello 스크립트 idempotent 인지 확인 합니다. 동일한 결과 hello toohello 스크립트 생성 해야 하는 여러 번 호출 합니다.
2. hello 스크립트는 제대로 버전 이어야 합니다. 업그레이드 하거나 tooinstall hello 응용 프로그램을 시도 하 고 있는 고객에 영향을 받지 않는 있도록 변경 내용을 테스트 하는 경우에 hello 스크립트에 대 한 다른 위치를 사용 합니다. 
3. 각 지점에서 적절 한 로깅 toohello 스크립트를 추가 합니다. 일반적으로 스크립트 로그 hello는 유일한 방법은 toodebug hello 응용 프로그램 설치 문제가 있습니다.
4. 있어야 호출 tooexternal 서비스 또는 리소스 적절 한 재시도 hello 설치는 일시적인 네트워크 문제로 인해 영향을 받지 않습니다.
5. 스크립트 hello 노드에서 서비스의 시작 하는 경우 확인 hello 서비스를 모니터링 하 고 toostart 노드 재부팅 시 자동으로 구성 합니다.

## <a name="package-application"></a>패키지 응용 프로그램
HDInsight 응용 프로그램을 설치하는 데 필요한 모든 파일을 포함하는 zip 파일을 만듭니다. Zip 파일의 hello 필요 [응용 프로그램 게시](#publish-application)합니다.

* [createUiDefinition.json](#define-application).
* mainTemplate.json. [사용자 지정 HDInsight 응용 프로그램 설치](hdinsight-apps-install-custom-applications.md)의 샘플을 참조하세요.
* 모든 필수 스크립트입니다.

> [!NOTE]
> 응용 프로그램 파일 (있는 경우 웹 응용 프로그램 파일 포함) hello 공개적으로 액세스할 수 있는 모든 끝점에 위치할 수 있습니다.
> 

## <a name="publish-application"></a>응용 프로그램 게시
Hello 단계 toopublish HDInsight 응용 프로그램에 다음을 수행 합니다.

1. Toohello 로그온 [Azure 게시 포털](https://publish.windowsazure.com/)합니다.
2. 클릭 **솔루션 템플릿을** hello 왼쪽된 toocreate 새 솔루션 템플릿에서에서 합니다.
3. 제목을 입력한 다음 **새 솔루션 템플릿 만들기**를 클릭합니다.
4. 클릭 **만들기 개발 센터 계정 및 조인 hello Azure 프로그램** tooregister 그렇게 하지 않은 경우 회사입니다.  [Microsoft 개발자 계정 만들기](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md)를 참조하세요.
5. 클릭 **일부 토폴로지 tooget Started 정의**합니다. 솔루션 템플릿을 "부모" tooall 해당 토폴로지 됩니다. 하나의 제품/솔루션 템플릿에서 여러 토폴로지를 정의할 수 있습니다. 제안을 toostaging 푸시됩니다, 모든 토폴로지에서 푸시됩니다. 
6. 토폴로지 이름을 입력 하 고 hello 더하기 기호를 클릭 합니다.
7. 새 버전을 입력 하 고 hello 더하기 기호를 클릭 합니다.
8. 업로드 hello zip 파일에서 준비한 [응용 프로그램 패키지](#package-application)합니다.  
9. **인증 요청**을 클릭합니다. Microsoft 인증 팀 hello hello 파일을 검토 하 고 hello 토폴로지를 인증 합니다.

## <a name="next-steps"></a>다음 단계
* [HDInsight 응용 프로그램을 설치](hdinsight-apps-install-applications.md): tooinstall HDInsight 응용 프로그램 tooyour 클러스터 하는 방법에 대해 알아봅니다.
* [사용자 지정 HDInsight 응용 프로그램을 설치](hdinsight-apps-install-custom-applications.md): 자세한 방법을 toodeploy 게시 되지 않은 HDInsight 응용 프로그램 tooHDInsight 합니다.
* [스크립트 동작을 사용 하 여 Linux 기반 HDInsight 클러스터를 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md): 자세한 방법을 toouse 스크립트 동작 tooinstall 추가 응용 프로그램입니다.
* [Azure 리소스 관리자 템플릿을 사용 하 여 HDInsight의 Linux 기반 Hadoop 클러스터를 만들어](hdinsight-hadoop-create-linux-clusters-arm-templates.md): 방법을 toocall 리소스 관리자 템플릿 toocreate HDInsight 클러스터에 대해 알아봅니다.
* [빈 가장자리 노드를 사용 하 여 HDInsight의](hdinsight-apps-use-edge-node.md): 방법을 toouse 빈 가장자리 노드 HDInsight 클러스터에 액세스, HDInsight 응용 프로그램 테스트 및 호스팅에 대 한 자세한 내용은 HDInsight 응용 프로그램입니다.

