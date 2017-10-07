---
title: "aaaInstall Azure HDInsight의 Hadoop 응용 프로그램 사용자 지정 | Microsoft Docs"
description: "자세한 내용은 방법 HDInsight 응용 프로그램에서 tooinstall HDInsight 응용 프로그램입니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ed3148f2c4d4d2b568d84e44fa6d76bb5a001902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a>Azure HDInsight에 사용자 지정 Hadoop 응용 프로그램 설치

이 문서에서는 tooinstall 되지 않은 Azure HDInsight에서 Hadoop 응용 toohello Azure 포털을 게시 하는 방법을 배웁니다. 이 문서에 설치할 hello 응용 프로그램은 [색상](http://gethue.com/)합니다.

HDInsight 응용 프로그램은 Linux 기반 HDInsight 클러스터에 사용자가 설치할 수 있는 응용 프로그램입니다.  Microsoft, ISV(독립 소프트웨어 공급 업체) 또는 사용자가 직접 이러한 응용 프로그램을 개발할 수 있습니다.  

다른 관련 문서:

* [HDInsight 응용 프로그램을 설치](hdinsight-apps-install-applications.md): tooinstall HDInsight 응용 프로그램 tooyour 클러스터 하는 방법에 대해 알아봅니다.
* [HDInsight는 응용 프로그램 게시](hdinsight-apps-publish-applications.md): 자세한 방법을 toopublish 사용자 사용자 지정 HDInsight 응용 프로그램 tooAzure 마켓플레이스입니다.
* [MSDN: HDInsight 응용 프로그램을 설치 하](https://msdn.microsoft.com/library/mt706515.aspx): 자세한 방법을 toodefine HDInsight 응용 프로그램입니다.

## <a name="prerequisites"></a>필수 조건
기존 HDInsight 클러스터에서 tooinstall HDInsight 응용 프로그램을 사용 하도록 하려는 경우에 HDInsight 클러스터가 있어야 합니다. 하나의 toocreate 참조 [클러스터를 만들어](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)합니다. HDInsight 클러스터를 만들 경우 HDInsight 응용 프로그램도 설치할 수 있습니다.

## <a name="install-hdinsight-applications"></a>HDInsight 응용 프로그램 설치
클러스터 또는 tooan 기존 HDInsight 클러스터를 만들 때 HDInsight 응용 프로그램을 설치할 수 있습니다. Azure Resource Manager 템플릿 정의는 [MSDN: HDInsight 응용 프로그램 설치](https://msdn.microsoft.com/library/mt706515.aspx)를 참조하세요.

이 응용 프로그램 (색상)를 배포 하는 데 필요한 hello 파일:

* [azuredeploy.json](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): hello 리소스 관리자 템플릿을 HDInsight 응용 프로그램을 설치 합니다. Azure Resource Manager 템플릿을 직접 개발하려면 [MSDN: HDInsight 응용 프로그램 설치](https://msdn.microsoft.com/library/mt706515.aspx) 를 참조하세요.
* [색상 install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): hello hello 가장자리 노드를 구성 하기 위한 리소스 관리자 템플릿을 hello에 의해 호출 되는 스크립트 동작 합니다.
* [색상 binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): hello 색상을 나타내는 이진 파일 hui install_v0.sh에서 호출 됩니다.
* [색상을 나타내는 이진 파일-14 04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): hello 색상을 나타내는 이진 파일 hui install_v0.sh에서 호출 됩니다.
* [webwasb-tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz): hui-install_v0.sh에서 호출되는 샘플 웹 응용 프로그램(Tomcat).

**tooinstall 색상 tooan 기존 HDInsight 클러스터**

1. Hello tooAzure에 이미지 toosign와 hello Azure 포털에서에서 열기 hello 리소스 관리자 템플릿을 다음를 클릭 합니다.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    이 단추는 hello Azure 포털에서 리소스 관리자 템플릿을 엽니다.  hello 리소스 관리자 템플릿을에 위치한 [https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue)합니다.  toolearn 어떻게 toowrite이 리소스 관리자 템플릿을 참조 [MSDN: HDInsight 응용 프로그램을 설치](https://msdn.microsoft.com/library/mt706515.aspx)합니다.
2. Hello에서 **매개 변수** 블레이드에서 hello 다음을 입력 합니다.

   * **ClusterName**: tooinstall hello 응용 프로그램을 원하는 hello 클러스터의 hello 이름을 입력 합니다. 이 클러스터는 기존 클러스터여야 합니다.
3. 클릭 **확인** toosave hello 매개 변수입니다.
4. Hello에서 **사용자 지정 배포** 블레이드에서 입력 **리소스 그룹**합니다.  hello 리소스 그룹은 hello 클러스터, hello 종속 저장소 계정 및 기타 리소스를 그룹화 하는 컨테이너입니다. 필요한 toouse hello hello 클러스터와 동일한 리소스 그룹입니다.
5. **약관**을 클릭한 다음 **만들기**를 클릭합니다.
6. Hello 확인 **Pin toodashboard** 확인란을 선택한 다음 클릭 **만들기**합니다. Hello 타일 고정 된 toohello 포털 대시보드 및 hello 포털 알림 (hello 포털의 hello 상단에서 hello 종 모양 아이콘을 클릭 합니다.)에서 hello 설치 상태를 볼 수 있습니다.  약 10 분 tooinstall hello 응용 프로그램을 사용합니다.

**클러스터를 만드는 동안 tooinstall 색상**

1. Hello tooAzure에 이미지 toosign와 hello Azure 포털에서에서 열기 hello 리소스 관리자 템플릿을 다음를 클릭 합니다.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    이 단추는 hello Azure 포털에서 리소스 관리자 템플릿을 엽니다.  hello 리소스 관리자 템플릿을에 위치한 [https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json)합니다.  toolearn 어떻게 toowrite이 리소스 관리자 템플릿을 참조 [MSDN: HDInsight 응용 프로그램을 설치](https://msdn.microsoft.com/library/mt706515.aspx)합니다.
2. Hello 명령 toocreate 클러스터를 수행 하 고 색상을 설치 합니다. HDInsight 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.

또한 toohello Azure 포털을 사용할 수도 있습니다 [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) 및 [Azure CLI](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) toocall 리소스 관리자 템플릿을 합니다.

## <a name="validate-hello-installation"></a>Hello 설치 유효성 검사
Azure 포털 toovalidate hello 응용 프로그램 설치 hello에 hello 응용 프로그램 상태를 확인할 수 있습니다. 또한 확인할 수도 모든 HTTP 끝점 준을 예상 대로 및 hello 웹 페이지 있는 경우:

**tooopen hello 색상 포털**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에 있습니다.  표시되지 않으면 **찾아보기**를 클릭한 다음 **HDInsight 클러스터**를 클릭합니다.
3. Hello 클러스터 hello 응용 프로그램을 설치 하는 위치를 클릭 합니다.
4. Hello에서 **설정** 블레이드에서 클릭 **응용 프로그램** hello에서 **일반** 범주입니다. 표시 **색상** hello에 나열 된 **설치 된 앱** 블레이드입니다.
5. 클릭 **색상** hello 목록 toolist hello 속성에서 합니다.  
6. Hello 웹 페이지 링크 toovalidate hello 웹 사이트를 클릭 합니다. 브라우저 toovalidate hello 색상 웹 UI에서 SSH를 사용 하 여 열기 hello SSH 끝점에에서 hello HTTP 끝점을 엽니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

## <a name="troubleshoot-hello-installation"></a>Hello 설치 문제 해결
Hello 포털 알림에서 hello 응용 프로그램 설치 상태를 확인할 수 있습니다 (hello 포털의 hello 상단에서 hello 종 모양 아이콘 클릭).

응용 프로그램 설치에 실패 한 경우에 hello 오류 메시지가 표시 하 고 3 위치의 정보를에서 디버그할 수 있습니다.

* HDInsight 응용 프로그램: 일반 오류 정보입니다.

    Hello 클러스터 hello 포털에서 열고 hello 설정 블레이드에서 응용 프로그램을 클릭 합니다.

    ![hdinsight 응용 프로그램 응용 프로그램 설치 오류](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* HDInsight 스크립트 동작: hello HDInsight 응용 프로그램의 오류 메시지가 표시 되는 스크립트 작업 실패, 경우 hello 스크립트 오류에 대 한 자세한 내용은 hello 스크립트 작업 창에 표시 됩니다.

    Hello 설정 블레이드에서에서 스크립트 동작을 클릭 합니다. 스크립트 동작 기록을 hello 오류 메시지가 표시 됩니다.

    ![hdinsight 응용 프로그램 스크립트 작업 오류](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* Ambari Web UI: hello 설치 스크립트 hello 실패의 원인을 hello 되었으면 Ambari 웹 UI toocheck hello 설치 스크립트에 대 한 전체 로그 사용 합니다.

    자세한 내용은 [문제 해결](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)을 참조하세요.

## <a name="remove-hdinsight-applications"></a>HDInsight 응용 프로그램 제거
여러 가지 방법으로 toodelete HDInsight 응용 있습니다.

### <a name="use-portal"></a>포털 사용
**tooremove hello 포털을 사용 하는 응용 프로그램**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에 있습니다.  표시되지 않으면 **찾아보기**를 클릭한 다음 **HDInsight 클러스터**를 클릭합니다.
3. Hello 클러스터 hello 응용 프로그램을 설치 하는 위치를 클릭 합니다.
4. Hello에서 **설정** 블레이드에서 클릭 **응용 프로그램** hello에서 **일반** 범주입니다. 설치된 응용 프로그램 목록이 표시됩니다. 이 자습서에서는 **색상** hello에 나열 된 **설치 된 앱** 블레이드입니다.
5. Tooremove을 차례로 클릭 hello 응용 프로그램을 마우스 오른쪽 단추로 클릭 **삭제**합니다.
6. 클릭 **예** tooconfirm 합니다.

Hello 포털에서 hello 클러스터를 삭제 하거나 hello 응용 프로그램을 포함 하는 hello 리소스 그룹을 삭제할 수도 있습니다.

### <a name="use-azure-powershell"></a>Azure PowerShell 사용
Azure PowerShell을 사용 하 여 hello 클러스터를 삭제 하거나 hello 리소스 그룹을 삭제할 수 있습니다. [Azure PowerShell을 사용하여 클러스터 삭제](hdinsight-administer-use-powershell.md#delete-clusters)를 참조하세요.

### <a name="use-azure-cli"></a>Azure CLI 사용
Azure CLI를 사용 하 여 hello 클러스터를 삭제 하거나 hello 리소스 그룹을 삭제할 수 있습니다. [Azure CLI를 사용하여 클러스터 삭제](hdinsight-administer-use-command-line.md#delete-clusters)를 참조하세요.

## <a name="next-steps"></a>다음 단계
* [MSDN: HDInsight 응용 프로그램을 설치](https://msdn.microsoft.com/library/mt706515.aspx): 자세한 방법을 toodevelop 리소스 관리자 템플릿을 HDInsight 응용 프로그램을 배포 합니다.
* [HDInsight 응용 프로그램을 설치](hdinsight-apps-install-applications.md): tooinstall HDInsight 응용 프로그램 tooyour 클러스터 하는 방법에 대해 알아봅니다.
* [HDInsight는 응용 프로그램 게시](hdinsight-apps-publish-applications.md): 자세한 방법을 toopublish 사용자 사용자 지정 HDInsight 응용 프로그램 tooAzure 마켓플레이스입니다.
* [스크립트 동작을 사용 하 여 Linux 기반 HDInsight 클러스터를 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md): 자세한 방법을 toouse 스크립트 동작 tooinstall 추가 응용 프로그램입니다.
* [리소스 관리자 템플릿을 사용 하 여 HDInsight의 Linux 기반 Hadoop 클러스터를 만들어](hdinsight-hadoop-create-linux-clusters-arm-templates.md): 방법을 toocall 리소스 관리자 템플릿 toocreate HDInsight 클러스터에 대해 알아봅니다.
* [빈 가장자리 노드를 사용 하 여 HDInsight의](hdinsight-apps-use-edge-node.md): 방법을 toouse 빈 가장자리 노드 HDInsight 클러스터에 액세스, HDInsight 응용 프로그램 테스트 및 호스팅에 대 한 자세한 내용은 HDInsight 응용 프로그램입니다.
