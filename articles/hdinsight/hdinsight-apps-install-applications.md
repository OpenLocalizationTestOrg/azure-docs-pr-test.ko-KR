---
title: "Azure HDInsight의 aaaInstall 타사 Hadoop 응용 프로그램 | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall 타사 Hadoop 응용 프로그램에서 Azure HDInsight의 합니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: eaf5904d-41e2-4a5f-8bec-9dde069039c2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/16/2017
ms.author: jgao
ms.openlocfilehash: 00071517c81a17c01dccedf9e8dd5d0cabb38567
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-third-party-hadoop-applications-on-azure-hdinsight"></a>Azure HDInsight에 타사 Hadoop 응용 프로그램 설치

이 문서에서는 설명 어떻게 tooinstall Azure HDInsight에 이미 게시 된 제 3 자 Hadoop 응용 프로그램입니다. 사용자 고유의 응용 프로그램을 설치하는 방법에 대한 지침은 [사용자 지정 HDInsight 응용 프로그램 설치](hdinsight-apps-install-custom-applications.md)를 참조하세요.

HDInsight 응용 프로그램은 Linux 기반 HDInsight 클러스터에 사용자가 설치할 수 있는 응용 프로그램입니다. Microsoft, ISV(독립 소프트웨어 공급 업체) 또는 사용자가 직접 이러한 응용 프로그램을 개발할 수 있습니다.  

현재 네 개의 게시된 응용 프로그램이 있습니다.

* **HDInsight의 DATAIKU DDS**: Dataiku DSS (데이터 과학 Studio)는 데이터를 허용 하는 소프트웨어 전문가 (데이터 과학자, 비즈니스 분석가, 개발자...) tooprototype 빌드하고 원시 데이터를 변환 하는 매우 특정 서비스 배포 주의깊게 비즈니스 예측 합니다.
* **Datameer**: [Datameer](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft) 분석가 대화형 방법 toodiscover 제공 분석 및 hello 결과 빅 데이터를 시각화 합니다. 쉽게 toodiscover 새 관계 추가 데이터 원본 끌어옵니다 답변을 구할 hello 신속 하 게 해야 합니다.
* **HDnsight에 대 한 데이터 수집기 Streamsets** 있는 모든 기능을 갖춘 통합된 개발 환경 (IDE) 스트림 및 일괄 처리 데이터를 메시 파이프라인 수집와 있습니다 디자인, 테스트, 배포 및 관리 any-에-any는 다양 한 제공 스트림 변환-toowrite 사용자 지정 코드를 필요 없이 합니다. 
* **HDInsight에 대 한 CDAP cask** hello 데이터 응용 프로그램 및 데이터 호수 hello 시간 tooproduction 80%로 줄어듭니다 빅 데이터에 대 한 통합 플랫폼을 먼저 통합을 제공 합니다. 이 응용 프로그램은 표준 HBase 3.4 클러스터만을 지원합니다.
* **HDInsight (베타)에 대 한 인공 인텔리전스 H2O** H2O Sparkling 물 지원 분산된 알고리즘을 수행 하는 hello: GLM, Naïve Bayes, 분산 임의 포리스트, 그라데이션 승격 컴퓨터, 심층 신경망, 학습, k-means PCA, 딥 낮은 순위 모델, 이상 탐지 및 Autoencoders 범용으로 설정 합니다.
* **Kyligence Analytics Platform** KAP(Kyligence Analytics Platform)는 Apache Kylin 및 Apache Hadoop 기반의 엔터프라이즈 지원 데이터 웨어하우스로, 대규모 데이터 집합에 대해 1초 미만의 쿼리 대기 시간을 보장하고 비즈니스 사용자 및 분석가를 위해 데이터 분석을 간소화합니다. 
* **SnapLogic Hadooplex** hello SnapLogic Hadooplex HDInsight에서 실행 중인 고객 tooget toobusiness insights 더 빠르게 제공 하 여 가능 셀프 서비스 데이터를 수집 및 Microsoft Azure 클라우드 거의 모든 소스 toohello에서 준비 플랫폼입니다.
* **KNIME Spark 실행자에 대 한 작업 서버 Spark** KNIME Spark 실행자에 대 한 Spark 작업 서버를 사용 하는 tooconnect hello KNIME 분석 플랫폼 tooHDInsight 클러스터입니다.

이 문서에서 제공 하는 hello 지침은 Azure 포털을 사용 합니다. 수 hello 포털에서 hello Azure 리소스 관리자 템플릿 내보내기 또는 공급 업체의 hello 리소스 관리자 템플릿의 복사본이 있고 Azure PowerShell 및 Azure CLI toodeploy hello 템플릿을 사용 합니다.  [Resource Manager 템플릿을 사용하여 HDInsight의 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-arm-templates.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건
기존 HDInsight 클러스터에서 tooinstall HDInsight 응용 프로그램을 사용 하도록 하려는 경우에 HDInsight 클러스터가 있어야 합니다. 하나의 toocreate 참조 [클러스터를 만들어](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)합니다. HDInsight 클러스터를 만들 경우 HDInsight 응용 프로그램도 설치할 수 있습니다.

## <a name="install-applications-tooexisting-clusters"></a>응용 프로그램 tooexisting 클러스터를 설치 합니다.
hello 다음 단계에서는 tooinstall HDInsight 응용 프로그램 tooan 기존 HDInsight 클러스터입니다.

**tooinstall HDInsight 응용 프로그램**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에 있습니다.  표시되지 않으면 **더 많은 서비스**를 클릭한 다음 **HDInsight 클러스터**를 클릭합니다.
3. HDInsight 클러스터를 클릭합니다.  HDInsight 클러스터가 없는 경우 만듭니다.  see [클러스터 만들기](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)를 참조하세요.
4. 클릭 **응용 프로그램** hello에서 **구성을** 범주입니다. 설치된 응용 프로그램 목록이 표시됩니다. 응용 프로그램을 찾을 수 없으면, 즉 하는이 버전의 hello HDInsight 클러스터에 대 한 응용 프로그램이 없습니다.
   
    ![HDInsight 응용 프로그램 포털 메뉴](./media/hdinsight-apps-install-applications/hdinsight-apps-portal-menu.png)
5. 클릭 **추가** hello 블레이드 메뉴에서 합니다. 
   
    ![HDInsight 응용 프로그램 설치된 앱](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps.png)
   
    기존 HDInsight 응용 프로그램 목록이 표시됩니다.
   
    ![HDInsight 응용 프로그램 사용 가능한 응용 프로그램](./media/hdinsight-apps-install-applications/hdinsight-apps-list.png)
6. Hello 응용 프로그램 중 하나를 클릭 하 고 hello 약관에 동의 클릭 **선택**합니다.

Hello 포털 알림에서 hello 설치 상태를 볼 수 있습니다 (hello 포털의 hello 상단에서 hello 종 모양 아이콘 클릭). Hello 후 hello 응용 프로그램이 설치 된 앱 블레이드 hello에 표시 됩니다 응용 프로그램이 설치 됩니다.

## <a name="install-applications-during-cluster-creation"></a>클러스터 생성 중에 응용 프로그램 설치
클러스터를 만들 때 hello 옵션 tooinstall HDInsight 응용 프로그램 해야 합니다. Hello 과정에서 HDInsight 응용 프로그램에는 hello 클러스터 만들고 hello 실행 중 상태에 설치 됩니다. hello 다음 단계에서는 클러스터를 만들 때 tooinstall HDInsight 응용 프로그램입니다.

**tooinstall HDInsight 응용 프로그램**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. **새로 만들기**, **데이터 + 분석** 및 **HDInsight**를 차례로 클릭합니다.
3. **클러스터 이름**입력: 이 이름은 전역적으로 고유해야 합니다.
4. 클릭 **구독** tooselect hello hello 클러스터에 사용 되는 Azure 구독.
5. **클러스터 유형 선택**을 클릭한 후 다음을 선택합니다.
   
   * **클러스터 유형**: 어떤 toochoose를 모르는 경우 선택 **Hadoop**합니다. Hello 가장 인기 있는 클러스터 형식입니다.
   * **운영 체제**: **Linux**를 선택합니다.
   * **버전**: 어떤 toochoose 모르는 경우 hello 기본 버전을 사용 합니다. 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.
   * **계층 클러스터**: 두 가지 범주의 hello 빅 데이터 클라우드 서비스를 제공 하는 Azure HDInsight: 표준 계층과 고급 계층입니다. 자세한 내용은 [클러스터 계층](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers)을 참조하세요.
6. 클릭 **응용 프로그램**, 클릭 hello 중 응용 프로그램을 게시 한 다음 클릭 **선택**합니다.
7. 클릭 **자격 증명** hello 관리: 사용자에 대 한 암호를 입력 합니다. 또한 tooenter 해야는 **SSH 사용자 이름이** 및 중 하나는 **암호** 또는 **공개 키**, 사용 되는 tooauthenticate hello SSH 사용자는 합니다. 공개 키를 사용 하 여 hello 권장 접근법입니다. 클릭 **선택** hello 아래쪽 toosave hello 자격 증명 구성 시.
8. 클릭 **데이터 소스**hello 기존 저장소 계정 중 하나를 선택 하거나 hello 클러스터에 대 한 hello 기본 저장소 계정으로 사용 되는 새 저장소 계정 toobe 만듭니다.
9. 클릭 **리소스 그룹** tooselect 기존 리소스 그룹 또는 클릭 **새로** toocreate 새 리소스 그룹
10. Hello에 **새 HDInsight 클러스터** 블레이드에서 되도록 **Pin tooStartboard** 을 선택한 다음 클릭 **만들기**합니다. 

## <a name="list-installed-hdinsight-apps-and-properties"></a>설치된 HDInsight 앱 및 속성 나열
hello 포털 HDInsight 클러스터 및 hello 속성 설치 된 각 응용 프로그램의 응용 프로그램을 설치 하는 hello의 목록을 보여 줍니다.

**toolist HDInsight 응용 프로그램 및 디스플레이 속성**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에 있습니다.  표시되지 않으면 **찾아보기**를 클릭한 다음 **HDInsight 클러스터**를 클릭합니다.
3. HDInsight 클러스터를 클릭합니다.
4. Hello에서 **설정** 블레이드에서 클릭 **응용 프로그램** hello에서 **일반** 범주입니다. hello 설치 된 앱 블레이드를 설치 하는 hello에 대 한 응용 프로그램을 모두 나열합니다. 
   
    ![HDInsight 응용 프로그램 설치된 앱](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps-with-apps.png)
5. Hello 설치 된 응용 프로그램 tooshow hello 속성 중 하나를 클릭 합니다. hello 속성 블레이드 목록:
   
   * 앱 이름: 응용 프로그램 이름입니다.
   * 상태: 응용 프로그램 상태입니다. 
   * Toohello 가장자리 노드를 배포 했다고 hello 웹 응용 프로그램의 웹 페이지: hello URL입니다. hello 자격 증명은 hello hello 클러스터에 대해 구성한 hello HTTP 사용자 자격 증명에 것과 동일 합니다.
   * HTTP 끝점: hello 자격 증명은 hello hello 클러스터에 대해 구성한 hello HTTP 사용자 자격 증명에 것과 동일 합니다. 
   * SSH 끝점: SSH tooconnect toohello 가장자리 노드를 사용할 수 있습니다. hello SSH 자격 증명이 hello hello 클러스터에 대해 구성한 hello SSH 사용자 자격 증명에 것과 동일 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.
6. 응용 프로그램 toodelete hello 응용 프로그램을 마우스 오른쪽 단추로 클릭 **삭제** hello 상황에 맞는 메뉴에서입니다.

## <a name="connect-toohello-edge-node"></a>Toohello 가장자리 노드를 연결 합니다.
HTTP와 SSH를 사용 하 여 toohello 가장자리 노드를 연결할 수 있습니다. hello에서 hello 끝점 정보를 찾을 수 [포털](#list-installed-hdinsight-apps-and-properties)합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

hello HTTP 끝점 자격 증명은 hello HDInsight 클러스터;에 대해 구성 된 hello HTTP 사용자 자격 증명 hello SSH 끝점 자격 증명은 hello SSH 자격 hello HDInsight 클러스터에 대해 구성한 것입니다.

## <a name="troubleshoot"></a>문제 해결
참조 [hello 설치 문제 해결](hdinsight-apps-install-custom-applications.md#troubleshoot-the-installation)합니다.

## <a name="next-steps"></a>다음 단계
* [사용자 지정 HDInsight 응용 프로그램을 설치](hdinsight-apps-install-custom-applications.md): 자세한 방법을 toodeploy 게시 되지 않은 HDInsight 응용 프로그램 tooHDInsight 합니다.
* [HDInsight는 응용 프로그램 게시](hdinsight-apps-publish-applications.md): 자세한 방법을 toopublish 사용자 사용자 지정 HDInsight 응용 프로그램 tooAzure 마켓플레이스입니다.
* [MSDN: HDInsight 응용 프로그램을 설치 하](https://msdn.microsoft.com/library/mt706515.aspx): 자세한 방법을 toodefine HDInsight 응용 프로그램입니다.
* [스크립트 동작을 사용 하 여 Linux 기반 HDInsight 클러스터를 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md): 자세한 방법을 toouse 스크립트 동작 tooinstall 추가 응용 프로그램입니다.
* [리소스 관리자 템플릿을 사용 하 여 HDInsight의 Linux 기반 Hadoop 클러스터를 만들어](hdinsight-hadoop-create-linux-clusters-arm-templates.md): 방법을 toocall 리소스 관리자 템플릿 toocreate HDInsight 클러스터에 대해 알아봅니다.
* [빈 가장자리 노드를 사용 하 여 HDInsight의](hdinsight-apps-use-edge-node.md): 방법을 toouse 빈 가장자리 노드 HDInsight 클러스터에 액세스, HDInsight 응용 프로그램 테스트 및 호스팅에 대 한 자세한 내용은 HDInsight 응용 프로그램입니다.

