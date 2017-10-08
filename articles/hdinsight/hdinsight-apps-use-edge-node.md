---
title: "aaaUse 빈 Azure HDInsight의 Hadoop 클러스터에 지 노드에 | Microsoft Docs"
description: "어떻게 tooadd 빈 가장자리 노드 tooan HDInsight 클러스터를 클라이언트로 사용할 수 및 다음 테스트/호스트 HDInsight 응용 프로그램입니다."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a>HDInsight의 Hadoop 클러스터에서 빈 에지 노드 사용

Tooadd 빈 노드 tooan HDInsight 클러스터를 가장자리 하는 방법에 대해 알아봅니다. 빈 가장자리 노드는 없는 Hadoop 서비스를 실행 하면서도 같은 클라이언트 도구는 설치 하 고 hello headnodes 처럼 구성 하는 hello로 Linux 가상 컴퓨터. Hello 클러스터에 액세스, 클라이언트 응용 프로그램을 테스트 하 고, 클라이언트 응용 프로그램을 호스팅하기 위한 hello 가장자리 노드를 사용할 수 있습니다. 

Hello 클러스터를 만들 때 빈 가장자리 노드 tooan 기존 HDInsight 클러스터에 tooa 새 클러스터를 추가할 수 있습니다. 빈 에지 노드는 Azure Resource Manager 템플릿을 사용하여 추가합니다.  hello 다음 샘플을 수행 하는 방법을 템플릿을 사용 하 여:

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

Hello 예제와 같이 필요에 따라를 호출할 수 있습니다는 [태스크 스크립팅할](hdinsight-hadoop-customize-cluster-linux.md) tooperform 등의 추가 구성을 설치 [Apache 색상을 나타내는](hdinsight-hadoop-hue-linux.md) hello 가장자리 노드에 있습니다. hello 스크립트 동작 스크립트 hello 웹에서 공개적으로 액세스할 수 있어야 합니다.  예를 들어 hello 스크립트는 Azure 저장소에 저장 되 면 공용 컨테이너 또는 공용 blob 중 하나를 사용 합니다.

hello 가장자리 노드 가상 컴퓨터 크기는 hello HDInsight 클러스터 작업자 노드 vm 크기 요구 사항을 충족 해야 합니다. Hello 권장 되는 작업자 노드 vm 크기에 대 한 참조 [HDInsight 클러스터를 만드는 Hadoop](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)합니다.

가장자리 노드를 만든 후에 toohello 가장자리 노드 SSH를 사용 하 여 연결 하 고 HDInsight의 클라이언트 도구 tooaccess hello Hadoop 클러스터를 실행할 수 있습니다.

> [!WARNING] 
> HDInsight에서 빈 에지 노드를 사용하는 기능은 현재 미리 보기로 제공됩니다. Microsoft에서 상업적으로 적절 한 지원을 받을 하는 hello 가장자리 노드에 설치 되어 있는 사용자 지정 구성 요소. 이를 통해 발생한 문제가 해결될 수도 있습니다. 또는 추가 지원을 요청에 대 한 참조 toocommunity 리소스 수 있습니다. hello 커뮤니티에서 도움말을 가져오기 위한 대부분의 활성 사이트 hello hello 다음과가 같습니다.
>
> * [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * [http://stackoverflow.com](http://stackoverflow.com).
>
> Apache 기술을 사용 하는 것일 수 있습니다 수 toofind 지원을 통해 hello Apache 프로젝트 사이트에 [http://apache.org](http://apache.org), hello 같은 [Hadoop](http://hadoop.apache.org/) 사이트입니다.

## <a name="add-an-edge-node-tooan-existing-cluster"></a>가장자리 노드 tooan 기존 클러스터를 추가 합니다.
이 섹션에서는 리소스 관리자 템플릿 tooadd 가장자리 노드 tooan 기존 HDInsight 클러스터를 사용합니다.  hello 리소스 관리자 템플릿을 찾을 수 [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/)합니다. hello 리소스 관리자 템플릿 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh에 있는 스크립트 작업을 호출 합니다. hello 스크립트는 모든 작업을 수행 하지 않습니다.  것 toodemonstrate 리소스 관리자 템플릿으로 스크립트 작업을 호출 합니다.

**tooadd 빈 가장자리 노드 tooan 기존 클러스터**

1. 아직 없는 경우 HDInsight 클러스터를 만듭니다.  [Hadoop 자습서: HDInsight에서 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.
2. Hello tooAzure에 이미지 toosign와 hello Azure 포털에서에서 열기 hello Azure 리소스 관리자 템플릿을 다음를 클릭 합니다. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Hello 다음과 같은 속성을 구성 합니다.
   
   * **구독**: hello 클러스터를 만드는 데 사용 되는 Azure 구독을 선택 합니다.
   * **리소스 그룹**: hello 기존 HDInsight 클러스터에 사용 되는 선택 hello 리소스 그룹입니다.
   * **위치**: hello 기존 HDInsight 클러스터의 hello 위치를 선택 합니다.
   * **클러스터 이름**: 기존 HDInsight 클러스터의 hello 이름을 입력 합니다.
   * **노드 크기를 가장자리**: hello VM 크기 중 하나를 선택 합니다. hello vm 크기는 hello 작업자 노드 vm 크기 요구 사항을 충족 해야 합니다. Hello 권장 되는 작업자 노드 vm 크기에 대 한 참조 [HDInsight 클러스터를 만드는 Hadoop](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)합니다.
   * **노드 접두사 가장자리**: hello 기본값은 **새**합니다.  Hello 기본값을 사용 하 여 hello 가장자리 노드 이름이 **새 edgenode**합니다.  Hello 접두사 hello 포털에서 사용자 지정할 수 있습니다. 또한 hello 템플릿에서 hello 전체 이름을 사용자 지정할 수 있습니다.

4. 확인 **toohello 약관 위에서 설명한 동의**, 클릭 하 고 **구매** toocreate hello 가장자리 노드.

>[!IMPORTANT]
> Hello 기존 HDInsight 클러스터에 대 한 있는지 tooselect hello Azure 리소스 그룹을 확인 합니다.  그렇지 않으면 오류가 hello 메시지 "을 수행할 수 없습니다 중첩 된 리소스에 대해 요청 된 작업입니다. 부모 리소스 '&lt;ClusterName>' 찾을 수 없음"이라는 오류 메시지를 받습니다.

## <a name="add-an-edge-node-when-creating-a-cluster"></a>클러스터를 만들 때 에지 노드 추가
이 섹션에서는 리소스 관리자 템플릿 toocreate HDInsight 클러스터를 사용 하 여 가장자리 노드 사용.  hello에 hello 리소스 관리자 템플릿을 찾을 수 [Azure 빠른 시작 템플릿 갤러리](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/)합니다. hello 리소스 관리자 템플릿 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh에 있는 스크립트 작업을 호출 합니다. hello 스크립트는 모든 작업을 수행 하지 않습니다.  것 toodemonstrate 리소스 관리자 템플릿으로 스크립트 작업을 호출 합니다.

**tooadd 빈 가장자리 노드 tooan 기존 클러스터**

1. 아직 없는 경우 HDInsight 클러스터를 만듭니다.  [HDInsight에서 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.
2. Hello tooAzure에 이미지 toosign와 hello Azure 포털에서에서 열기 hello Azure 리소스 관리자 템플릿을 다음를 클릭 합니다. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Hello 다음과 같은 속성을 구성 합니다.
   
   * **구독**: hello 클러스터를 만드는 데 사용 되는 Azure 구독을 선택 합니다.
   * **리소스 그룹**: hello 클러스터에 사용 되는 새 리소스 그룹을 만듭니다.
   * **위치**: hello 리소스 그룹에 대 한 위치를 선택 합니다.
   * **클러스터 이름**: 새 클러스터 toocreate hello에 대 한 이름을 입력 합니다.
   * **클러스터 로그인 사용자 이름**: hello Hadoop HTTP 사용자 이름을 입력 합니다.  기본 이름은 hello **admin**합니다.
   * **로그인 암호 클러스터**: hello Hadoop HTTP 사용자 암호를 입력 합니다.
   * **Ssh 사용자 이름이**: hello SSH 사용자 이름을 입력 합니다. 기본 이름은 hello **sshuser**합니다.
   * **Ssh 암호**: hello SSH 사용자 암호를 입력 합니다.
   * **설치 스크립트 작업**:이 자습서를 진행 하 고 hello 기본값을 유지 합니다.
     
     일부 속성이 hello 템플릿에 하드 코드 된: 클러스터 종류, 클러스터 작업자 노드 수, 가장자리 노드 크기 및 가장자리 노드 이름입니다.
4. 확인 **toohello 약관 위에서 설명한 동의**, 클릭 하 고 **구매** hello 가장자리 노드와 toocreate hello 클러스터입니다.

## <a name="access-an-edge-node"></a>에지 노드 액세스
hello 가장자리 노드 ssh 끝점은 &lt;EdgeNodeName >.&lt; ClusterName >-ssh.azurehdinsight.net:22 합니다.  예: new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22

hello 가장자리 노드가 hello Azure 포털에서 응용 프로그램으로 나타납니다.  hello 포털 제공 정보 tooaccess hello hello SSH를 사용 하 여 노드를 가장자리입니다.

**tooverify hello 가장자리 노드 SSH 끝점**

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. 가장자리 노드도 hello HDInsight 클러스터를 엽니다.
3. 클릭 **응용 프로그램** hello 클러스터 블레이드에서 합니다. Hello 가장자리 노드를 참조 해야 합니다.  기본 이름은 hello **새 edgenode**합니다.
4. Hello 가장자리 노드를 클릭 합니다. Hello SSH 끝점에 표시 되어야 합니다.

**hello 가장자리 노드에서 toouse 하이브**

1. SSH tooconnect toohello 가장자리 노드를 사용 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. SSH를 사용 하 여 toohello 가장자리 노드를 연결한 후 다음 명령 tooopen hello 하이브 콘솔 hello를 사용 합니다.
   
        hive
3. 다음 명령은 tooshow 하이브 표 hello 클러스터의 hello를 실행 합니다.
   
        show tables;

## <a name="delete-an-edge-node"></a>에지 노드를 삭제합니다.
Hello Azure 포털에서에서 가장자리 노드를 삭제할 수 있습니다.

**tooaccess 가장자리 노드**

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. 가장자리 노드도 hello HDInsight 클러스터를 엽니다.
3. 클릭 **응용 프로그램** hello 클러스터 블레이드에서 합니다. 에지 노드의 목록이 표시됩니다.  
4. 마우스 오른쪽 단추로 클릭 hello 가장자리 사용할 노드 toodelete, 마우스 클릭 **삭제**합니다.
5. 클릭 **예** tooconfirm 합니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 배웠습니다 어떻게 tooadd 방법을 tooaccess hello 가장자리 노드 및 가장자리 노드. 더 toolearn hello 다음 문서를 참조:

* [HDInsight 응용 프로그램을 설치](hdinsight-apps-install-applications.md): tooinstall HDInsight 응용 프로그램 tooyour 클러스터 하는 방법에 대해 알아봅니다.
* [사용자 지정 HDInsight 응용 프로그램을 설치](hdinsight-apps-install-custom-applications.md): 자세한 방법을 toodeploy 게시 되지 않은 HDInsight 응용 프로그램 tooHDInsight 합니다.
* [HDInsight는 응용 프로그램 게시](hdinsight-apps-publish-applications.md): 자세한 방법을 toopublish 사용자 사용자 지정 HDInsight 응용 프로그램 tooAzure 마켓플레이스입니다.
* [MSDN: HDInsight 응용 프로그램을 설치 하](https://msdn.microsoft.com/library/mt706515.aspx): 자세한 방법을 toodefine HDInsight 응용 프로그램입니다.
* [스크립트 동작을 사용 하 여 Linux 기반 HDInsight 클러스터를 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md): 자세한 방법을 toouse 스크립트 동작 tooinstall 추가 응용 프로그램입니다.
* [리소스 관리자 템플릿을 사용 하 여 HDInsight의 Linux 기반 Hadoop 클러스터를 만들어](hdinsight-hadoop-create-linux-clusters-arm-templates.md): 방법을 toocall 리소스 관리자 템플릿 toocreate HDInsight 클러스터에 대해 알아봅니다.

