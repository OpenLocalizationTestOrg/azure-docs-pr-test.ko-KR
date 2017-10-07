---
title: "Azure CLI-Azure HDInsight를 사용 하 여 aaaManage Hadoop 클러스터 | Microsoft Docs"
description: "Azure HDInsight에서 toouse hello Azure 명령줄 인터페이스 toomanage Hadoop 클러스터 하는 방법에 대해 알아봅니다. hello Azure CLI는 Windows, Mac 및 Linux에서 작동합니다."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 HDInsight의 Hadoop 클러스터를 관리 합니다.
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

자세한 내용은 방법 toouse hello [Azure 명령줄 인터페이스](../cli-install-nodejs.md) toomanage Hadoop Azure HDInsight 클러스터를 합니다. hello Azure CLI Node.js에서 구현 됩니다. Windows, Mac, Linux를 포함하여 Node.js를 지원하는 플랫폼에서 사용할 수 있습니다.

이 문서에서는 hello Azure CLI를 사용 하 여 HDInsight와에 대해 설명 합니다. 방법에 대 한 일반 지침에 대 한 Azure CLI toouse 참조 [설치 하 고 Azure CLI 구성][azure-command-line-tools]합니다.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>필수 조건
이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* **Azure CLI** -참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) 설치 및 구성 정보에 대 한 합니다.
* **TooAzure 연결**를 사용 하 여 다음 명령을 hello:
  
        azure login
  
    회사 또는 학교 계정을 사용 하 여 인증에 대 한 자세한 내용은 참조 하십시오. [hello Azure CLI에서에서 tooan Azure 구독 연결](../xplat-cli-connect.md)합니다.
* **Toohello Azure Resource Manager 모드로 전환**를 사용 하 여 다음 명령을 hello:
  
        azure config mode arm

tooget 도움말을 사용 하 여 hello **-h** 전환 합니다.  예:

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a>CLI hello로 클러스터를 만들려면
참조 [사용 하 여 HDInsight 클러스터 만들기 hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md)합니다.

## <a name="list-and-show-cluster-details"></a>클러스터 세부 정보 나열 및 표시
다음 명령을 toolist hello를 사용 하 고 클러스터 세부 정보 표시 됩니다.

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![클러스터 목록의 명령줄 보기][image-cli-clusterlisting]

## <a name="delete-clusters"></a>클러스터 삭제
다음 명령은 toodelete 클러스터 hello를 사용 합니다.

    azure hdinsight cluster delete <Cluster Name>

또한 hello 클러스터를 포함 하는 hello 리소스 그룹을 삭제 하 여 클러스터를 삭제할 수 있습니다. 하십시오 note, hello 그룹의에서 모든 리소스 hello hello 기본 저장소 계정을 포함 하 여 삭제 합니다.

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>클러스터 크기 조정
toochange hello Hadoop 클러스터 크기:

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>클러스터에 대한 HTTP 액세스 사용/사용 안 함
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>클러스터에 대한 RDP 액세스 사용/사용 안 함
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>다음 단계
이 문서에서는 배웠습니다 어떻게 tooperform 다른 HDInsight 클러스터 관리 작업입니다. 더 toolearn hello 다음 문서를 참조:

* [HDInsight hello Azure 포털을 사용 하 여 관리][hdinsight-admin-portal]
* [Azure PowerShell을 사용하여 HDInsight 클러스터 관리][hdinsight-admin-powershell]
* [Azure HDInsight 시작][hdinsight-get-started]
* [Toouse는 Azure CLI hello 하는 방법][azure-command-line-tools]

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "클러스터 나열 및 표시"
