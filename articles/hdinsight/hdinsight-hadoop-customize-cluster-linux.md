---
title: "스크립트 동작-Azure를 사용 하 여 aaaCustomize HDInsight 클러스터 | Microsoft Docs"
description: "사용자 지정 구성 요소 스크립트 동작을 사용 하 여 tooLinux 기반 HDInsight 클러스터를 추가 합니다. 스크립트 작업을 사용 하는 toocustomize hello 클러스터 구성 하거나 추가 서비스 및 색상, Solr, 또는 지역와 같은 유틸리티를 추가할 수 있는 Bash 스크립트"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정

호출 하는 구성 옵션을 제공 하는 HDInsight **스크립트 동작** hello 클러스터를 사용자 지정 하는 사용자 지정 스크립트를 호출 하 합니다. 이러한 스크립트는 사용 되는 tooinstall 추가 구성 요소 및 구성 설정을 변경 합니다. 스크립트 작업은 클러스터를 만드는 중이거나 만든 후에 사용할 수 있습니다.

> [!IMPORTANT]
> 이미 실행 중인 클러스터에 hello 기능 toouse 스크립트 작업은 Linux 기반 HDInsight 클러스터에 사용할 수만 있습니다.
>
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

스크립트 동작 HDInsight 응용 프로그램으로 게시 된 toohello Azure 마켓플레이스를 수도 있습니다. 이 문서에 hello 예 중 일부는 HDInsight 응용 프로그램에서 PowerShell 및.NET SDK hello 액션 명령 스크립트를 사용 하 여 설치 하는 방법을 표시 합니다. HDInsight 응용 프로그램에 대 한 자세한 내용은 참조 하십시오. [HDInsight 게시 응용 프로그램을 Azure Marketplace hello로](hdinsight-apps-publish-applications.md)합니다.

## <a name="permissions"></a>권한

도메인에 가입 된 HDInsight 클러스터를 사용 하는 경우 두 Ambari는 권한은 hello 클러스터와 스크립트 동작을 사용 하는 경우 필수입니다.

* **AMBARI 합니다. 실행\_사용자 지정\_명령**: hello Ambari 관리자 역할에는 기본적으로이 권한이 있습니다.
* **클러스터입니다. 실행\_사용자 지정\_명령**: HDInsight 클러스터 관리자 모두 hello 및 Ambari 관리자는 기본적으로이 권한이 있어야 합니다.

도메인 가입 HDInsight에서 권한으로 작업하는 방법에 대한 자세한 내용은 [도메인 가입 HDInsight 클러스터 관리](hdinsight-domain-joined-manage.md)를 참조하세요.

## <a name="access-control"></a>Access Control

계정 적어도 있어야 Azure 구독의 관리자/소유자 hello 아니라면 **참가자** hello HDInsight 클러스터를 포함 하는 액세스 toohello 리소스 그룹입니다.

또한 이상 있는 사용자는 HDInsight 클러스터를 만드는 경우 **참가자** 액세스 toohello Azure 구독 이전에 등록 해야 HDInsight에 대 한 hello 공급자입니다. 공급자 등록 사용자 만들면 참가자 액세스 toohello 구독과 hello에 대 한 리소스 처음으로 hello 구독에 대해 발생 합니다. [REST를 사용하여 공급자를 등록](https://msdn.microsoft.com/library/azure/dn790548.aspx)하면 리소스를 만들지 않고도 수행될 수 있습니다.

작업 액세스 관리에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.

* [Hello Azure 포털에에서 대 한 액세스 관리 시작](../active-directory/role-based-access-control-what-is.md)
* [역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>스크립트 작업 이해

스크립트 동작은 단순히 URI 및 해당 매개 변수를 제공하는 Bash 스크립트입니다. hello 스크립트 hello HDInsight 클러스터의 노드에서 실행 됩니다. hello 다음은 특성 및 스크립트 동작의 기능입니다.

* Hello HDInsight 클러스터에서 액세스할 수 있는 URI에 저장 되어야 합니다. hello 다음 저장소 위치 같습니다.

    * **Azure 데이터 레이크 저장소** hello HDInsight 클러스터에서 액세스할 수 있는 계정입니다. HDInsight에서 Azure Data Lake Store를 사용하는 방법에 대한 자세한 내용은 [Azure Data Lake Store에서 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.

        데이터 레이크 저장소에 저장 하는 스크립트를 사용할 경우 hello URI 형식은 `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`합니다.

        > [!NOTE]
        > hello 서비스 보안 주체 HDInsight 사용 하 여 tooaccess Data Lake 저장소에 대 한 읽기 액세스 toohello 스크립트가 있어야 합니다.

    * Blob에는 **Azure 저장소 계정** hello HDInsight 클러스터에 대 한 hello 기본 또는 추가 저장소 계정 중 하나입니다. HDInsight은 클러스터를 만드는 동안 저장소 계정에 이러한 유형의 tooboth 액세스 권한이 부여 됩니다.

    * Azure Blob, GitHub, OneDrive, Dropbox 등과 같은 공용 파일 공유 서비스

        예를 들어 Uri 참조 hello [예제 스크립트 작업 스크립트](#example-script-action-scripts) 섹션.

        > [!WARNING]
        > HDInsight는 __범용__ Azure Storage 계정만 지원합니다. Hello 현재 지원 하지 않는 __Blob 저장소__ 계정 유형입니다.

* 너무 제한 될 수 있습니다**특정 노드 유형에 대해**, 예에서는 헤드 노드 또는 작업자 노드에 대 한 합니다.

  > [!NOTE]
  > 프리미엄 HDInsight를 사용할 때는 hello 가장자리 노드에서 hello 스크립트를 사용 해야 함을 지정할 수 있습니다.

* **지속형** 또는 **임시** 스크립트일 수 있습니다.

    **지속** hello 스크립트를 실행 한 후 스크립트는 적용 된 tooworker 노드 추가 toohello 클러스터입니다. 예를 들어 hello 클러스터를 확장 하는 경우.

    지속형된 스크립트 변경 내용을 tooanother와 같은 노드 유형이 헤드 노드도 적용할 수 있습니다.

  > [!IMPORTANT]
  > 지속형 스크립트 작업은 고유한 이름이 있어야 합니다.

    **임시** 스크립트는 지속되지 않습니다. 가 hello 스크립트를 실행 한 후 노드 추가 toohello 클러스터 tooworker 적용된 하지 않습니다. 승격할 수 있고 이후에 임시 스크립트 tooa 스크립트를 지 속하거나 지속형된 스크립트 tooan 임시 스크립트 수준을 내립니다.

  > [!IMPORTANT]
  > 클러스터를 만들 때 사용되는 스크립트 작업은 자동으로 보존됩니다.
  >
  > 사용자가 지속형 스크립트로 지정하더라도 실패하는 스크립트는 보존되지 않습니다.

* 수락할 수 있는 **매개 변수** 에서 사용 하는 hello 스크립트 실행 중입니다.
* 사용 하 여 실행 **루트 수준 권한을** hello 클러스터 노드에서 합니다.
* Hello를 통해 사용할 수 있습니다 **Azure 포털**, **Azure PowerShell**, **Azure CLI**, 또는 **HDInsight.NET SDK**

hello 클러스터는 실행 된 모든 스크립트의 기록을 유지 합니다. hello 기록 올리기 또는 수준 내리기 작업에 대 한 스크립트의 toofind hello ID가 필요 하면 경우에 유용 합니다.

> [!IMPORTANT]
> 자동으로 방법 tooundo 없습니다는 hello 스크립트 작업으로 변경 합니다. Hello 변경 내용이 되돌리는 것 수동으로 하거나 되돌린 해당 하는 스크립트를 제공 합니다.


### <a name="script-action-in-hello-cluster-creation-process"></a>Hello 클러스터 만들기 프로세스에 스크립트 동작

클러스터를 만들 때 사용되는 스크립트 작업은 기존 클러스터에서 실행되는 스크립트 작업과 약간 다릅니다.

* hello 스크립트는 **자동으로 지속형**합니다.
* A **오류** hello 스크립트에 hello 클러스터 만들기 프로세스 toofail 인해 발생할 수 있습니다.

hello 다음 다이어그램에서는 hello 만드는 프로세스 동안 스크립트 작업을 실행할 때 수행 합니다.

![HDInsight 클러스터 사용자 지정 및 클러스터 만드는 동안의 단계][img-hdi-cluster-states]

hello 스크립트 HDInsight를 구성 하는 동안 실행 됩니다. 이 단계에서 모두에서 동시에 hello 스크립트가 실행 hello 클러스터 hello 노드에서 루트 권한으로 실행 하 고 지정 된 노드에 hello 합니다.

> [!NOTE]
> Hello 스크립트 hello 클러스터 노드에서 루트 수준 권한으로 실행, 되므로 Hadoop 관련 서비스를 포함 한 서비스를 시작 및 중지와 같은 작업을 수행할 수 있습니다. 서비스를 중지 하면 hello Ambari 서비스 및 기타 Hadoop 관련 서비스 되는지 실행 되 고 hello 스크립트 실행이 완료 되기 전에 확인 해야 합니다. 이러한 서비스는 필요한 생성 되는 동안 toosuccessfully hello 상태 및 hello 클러스터의 상태 확인 합니다.


클러스터를 만드는 동안 한 번에 여러 스크립트 작업을 사용할 수 있습니다. 이러한 스크립트는 지정 된 hello 순서로 호출 됩니다.

> [!IMPORTANT]
> 스크립트 작업은 60분 이내에 완료하지 않으면 시간이 초과됩니다. 클러스터 프로 비전 하는 동안 hello 스크립트는 다른 설치 및 구성 프로세스와 동시에 실행 됩니다. CPU 시간 또는 네트워크 대역폭 등의 리소스에 대 한 경합은 hello 스크립트 tootake 긴 toofinish 개발 환경에서 사용 하지 않고 발생할 수 있습니다.
>
> toominimize hello 하나 toorun hello 스크립트 시간, 다운로드 및 소스에서 응용 프로그램을 컴파일 등의 작업을 방지 합니다. 응용 프로그램을 미리 컴파일 하 고 Azure 저장소의 hello 이진 파일을 저장 합니다.


### <a name="script-action-on-a-running-cluster"></a>실행 중인 클러스터의 스크립트 작업

이미 실행 중인 클러스터에서 클러스터를 만드는 스크립트에 실패 하는 동안 사용 되는 작업을 실행 하는 스크립트와는 달리 hello 클러스터 toochange tooa 실패 상태가 자동으로 발생 하지 않습니다. 스크립트가 완료 되 면 hello 클러스터 tooa "실행 중" 상태를 반환 해야 합니다.

> [!IMPORTANT]
> Hello 클러스터 상태가 '실행 중', 경우에 hello 실패 한 스크립트 수을 위반한 것 작업 합니다. 예를 들어 스크립트는 hello 클러스터에 필요한 파일을 삭제 수 없습니다.
>
> 스크립트 동작 tooyour 클러스터를 적용 하기 전에 스크립트를 수행 하는 작업을 이해 해야 확인 해야 하므로 루트 권한으로 실행 합니다.

Hello 클러스터 상태가 toofrom 변경 스크립트 tooa 클러스터를 적용할 때 **실행** 너무**"승인 됨"**, 다음 **HDInsight 구성**, 한 마지막 너무 다시**실행** 성공적인 스크립트에 대 한 합니다. hello 스크립트 상태 hello 스크립트 동작 기록을 로그인 하 고 hello 스크립트의 성공 또는 실패 여부 정보 toodetermine이를 사용할 수 있습니다. 예를 들어 hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet에 사용 되는 tooview hello 상태의 스크립트 일 수 있습니다. 정보 비슷한 toohello를 다음 텍스트를 반환 합니다.

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> Hello 클러스터를 만든 후 hello 클러스터 사용자 (관리자) 암호 변경 하면,이 클러스터에 대 한 작업을 실행 하는 스크립트 실패할 수 있습니다. 모든 지속형된 스크립트 동작을 해당 대상 작업자 노드가 있는 경우 이러한 스크립트는 hello 클러스터 크기를 조정할 때 실패할 수 있습니다.

## <a name="example-script-action-scripts"></a>예제 스크립트 작업 스크립트

스크립트 작업 스크립트는 hello 다음 유틸리티를 통해 사용할 수 있습니다.

* Azure portal
* Azure PowerShell
* Azure CLI
* HDInsight .NET SDK

HDInsight는 HDInsight 클러스터에서 다음과 같은 구성 요소가 스크립트 tooinstall hello를 제공 합니다.

| 이름 | 스크립트 |
| --- | --- |
| **Azure Storage 계정 추가** |https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. 참조 [추가 저장소 추가 tooan HDInsight 클러스터](hdinsight-hadoop-add-storage.md)합니다. |
| **Hue 설치** |https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. [HDInsight 클러스터에서 Hue 설치 및 사용](hdinsight-hadoop-hue-linux.md)을 참조하세요. |
| **Presto 설치** |https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. [HDInsight 클러스터에 Presto 설치 및 사용](hdinsight-hadoop-install-presto.md)을 참조하세요. |
| **Solr 설치** |https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. [HDInsight 클러스터에서 Solr 설치 및 사용](hdinsight-hadoop-solr-install-linux.md)을 참조하세요. |
| **Giraph 설치** |https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. [HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install-linux.md)을 참조하세요. |
| **Hive 라이브러리 사전 로드** |https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. [HDInsight 클러스터에서 Hive 라이브러리 추가](hdinsight-hadoop-add-hive-libraries.md)를 참조하세요. |
| **Mono 설치 또는 업데이트** | https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash. [HDInsight에서 Mono 설치 또는 업데이트](hdinsight-hadoop-install-mono.md)를 참조하세요. |

## <a name="use-a-script-action-during-cluster-creation"></a>클러스터를 만드는 동안 스크립트 작업 사용

이 섹션에는 HDInsight 클러스터를 만들 때 작업 스크립트를 사용 하 여 hello 다른 방법을 예제를 제공 합니다.

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a>스크립트 작업을 사용 하 여 hello Azure 포털에서에서 클러스터를 만드는 동안

1. [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)에서 설명한 대로 클러스터를 만들기 시작합니다. Hello에 도달 하면 중지 __클러스터 요약__ 섹션.

2. Hello에서 __클러스터 요약__ 섹션을 선택 하는 hello __편집__ 에 대 한 링크 __고급 설정__합니다.

    ![고급 설정 링크](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. Hello에서 __고급 설정__ 섹션에서 __스크립트 작업을__합니다. Hello에서 __스크립트 작업을__ 섹션에서 __+ new 전송__

    ![새 스크립트 작업 제출](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. 사용 하 여 hello __스크립트를 선택__ 항목 tooselect 미리 만들어 놓은 스크립트입니다. toouse 사용자 지정 스크립트를 선택 __사용자 지정__ hello 다음 설명과 __이름__ 및 __URI 스크립트를 이용한 적__ 스크립트에 대 한 합니다.

    ![Hello 선택 스크립트 형식으로 스크립트 추가](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    다음 표에서 hello hello 양식에 hello 요소에 설명 합니다.

    | 속성 | 값 |
    | --- | --- |
    | 스크립트 선택 | toouse 선택 사용자 지정 스크립트 __사용자 지정__합니다. 그렇지 않은 경우 제공 된 hello 스크립트 중 하나를 선택 합니다. |
    | 이름 |Hello 스크립트 동작에 대 한 이름을 지정 합니다. |
    | Bash 스크립트 URI |가 호출 된 toocustomize hello 클러스터 hello URI toohello 스크립트를 지정 합니다. |
    | Head/Worker/Zookeeper |Hello 노드를 지정 (**h e a d**, **작업자**, 또는 **사육**) hello 사용자 정의 스크립트 실행 됩니다. |
    | 매개 변수 |Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다. |

    사용 하 여 hello __이 스크립트 동작이 계속__ 스크립트 hello 항목 tooensure 작업 크기 조정 하는 동안 적용 됩니다.

5. 선택 __만들기__ toosave hello 스크립트입니다. 사용할 수 있습니다 __+ 새 전송__ tooadd 또 다른 스크립트입니다.

    ![여러 스크립트 작업](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Hello를 사용 하 여 스크립트를 추가 마쳤으면 __선택__ 단추를 클릭 한 다음 hello __다음__ 단추 tooreturn toohello __클러스터 요약__ 섹션.

3. 선택 toocreate hello 클러스터 __만들기__ hello에서 __클러스터 요약__ 선택 합니다.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Azure 리소스 관리자 템플릿에서 스크립트 작업 사용

이 섹션의 예제 hello toouse Azure 리소스 관리자 템플릿 사용 하 여 작업을 스크립팅 하는 방법을 보여 줍니다.

#### <a name="before-you-begin"></a>시작하기 전에

* 워크스테이션 toorun HDInsight Powershell cmdlet을 구성 하는 방법에 대 한 정보를 참조 하십시오. [설치 Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
* 방법에 대 한 지침은 toocreate 템플릿 참조 [제작 Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md)합니다.
* 이전에 리소스 관리자에서 Azure PowerShell을 사용하지 않은 경우 [Azure 리소스 관리자와 함께 Azure PowerShell 사용](../azure-resource-manager/powershell-azure-resource-manager.md)을 참조하세요.

#### <a name="create-clusters-using-script-action"></a>스크립트 작업을 사용하여 클러스터 만들기

1. 컴퓨터에서 수정할 수 있는 템플릿 tooa 위치 hello를 복사 합니다. 이 서식 파일 hello headnodes 및 작업자 클러스터의 노드에서 hello Giraph를 설치합니다. Hello JSON 템플릿을 유효한 것을 확인할 수 있습니다. 템플릿 콘텐츠를 [JSONLint](http://jsonlint.com/), 즉, 온라인 JSON 유효성 검사기 도구에 붙여 넣습니다.

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. Azure PowerShell을 시작 하 고 Azure 계정을 tooyour 로그인 합니다. Hello 명령은 자격 증명을 입력 한 후 계정에 대 한 정보를 반환 합니다.

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. Hello 구독 ID를 제공 하는 여러 구독이 있는 경우 배포에 대 한 toouse를 백업본 있습니다.

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > 사용할 수 있습니다 `Get-AzureRmSubscription` tooget 각각에 대 한 hello 구독 ID를 포함 하는 사용자 계정과 연결 된 모든 구독의 목록입니다.

4. 기본 리소스 그룹이 없는 경우 리소스 그룹을 만듭니다. Hello 이름 hello 리소스 그룹 및 솔루션에 필요한 위치를 제공 합니다. Hello 새 리소스 그룹의 요약이 반환 됩니다.

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. toocreate hello를 실행 하 여 리소스 그룹에 대 한 배포 **새로 AzureRmResourceGroupDeployment** 명령 및 hello 필요한 매개 변수를 제공 합니다. hello 매개 변수는 같은 데이터가 hello를 같습니다.

    * 배포에 사용할 이름
    * 리소스 그룹의 hello 이름
    * hello 경로 또는 URL toohello 만든 서식 파일입니다.

  템플릿에 매개 변수가 필요한 경우 해당 매개 변수를 전달해야 합니다. 이 경우 hello 클러스터에서 hello 스크립트 동작 tooinstall R 매개 변수가 필요 하지 않습니다.

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    사용자는 hello 서식 파일에 정의 된 hello 매개 변수에 대 한 증명된 tooprovide 값입니다.

1. Hello 리소스 그룹 배포 된 hello 배포의 요약이 표시 됩니다.

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. 배포에 실패할 경우에 다음 cmdlet tooget 정보 hello 실패에 대 한 hello를 사용할 수 있습니다.

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>클러스터를 만드는 동안 Azure PowerShell에서 스크립트 작업 사용

이 섹션을 사용 하 여 hello [추가 AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) 스크립트 동작 toocustomize 클러스터를 사용 하 여 cmdlet tooinvoke 스크립트입니다. 계속하기 전에 Azure PowerShell을 설치 및 구성했는지 확인하세요. 워크스테이션 toorun HDInsight PowerShell cmdlet을 구성 하는 방법에 대 한 정보를 참조 하십시오. [설치 Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

hello 다음 스크립트에서는 방법을 tooapply PowerShell을 사용 하는 클러스터를 만들 때 스크립트 동작:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Hello 클러스터를 만들기 전에 몇 분 정도 걸릴 수 있습니다.

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a>스크립트 작업을 사용 하 여 hello HDInsight.NET SDK에서에서 클러스터를 만드는 동안

HDInsight.NET SDK hello HDInsight와 보다 쉽게 toowork.NET 응용 프로그램에서 사용 하면 클라이언트 라이브러리를 제공 합니다. 코드 샘플을 보려면 [사용 하 여 HDInsight 클러스터 만들기 Linux 기반 hello.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)합니다.

## <a name="apply-a-script-action-tooa-running-cluster"></a>클러스터 실행 스크립트 동작 tooa 적용

이 섹션에서는 tooapply 클러스터를 실행 하는 작업 tooa를 스크립팅 하는 방법에 대해 알아봅니다.

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a>Hello Azure 포털에서에서 클러스터를 실행 하는 스크립트 작업 tooa 적용

1. Hello에서 [Azure 포털](https://portal.azure.com)를 HDInsight 클러스터를 선택 합니다.

2. Hello HDInsight 클러스터 개요에서 선택 hello **스크립트 동작** 바둑판식으로 배열입니다.

    ![스크립트 작업 타일](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > 선택할 수도 있습니다 **모든 설정을** 선택한 후 **스크립트 동작** hello 설정 섹션에서에서.

3. 스크립트 동작 섹션 hello의 hello 위에서 선택 **새 전송**합니다.

    ![클러스터를 실행 하는 스크립트 tooa 추가](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. 사용 하 여 hello __스크립트를 선택__ 항목 tooselect 미리 만들어 놓은 스크립트입니다. toouse 사용자 지정 스크립트를 선택 __사용자 지정__ hello 다음 설명과 __이름__ 및 __URI 스크립트를 이용한 적__ 스크립트에 대 한 합니다.

    ![Hello 선택 스크립트 형식으로 스크립트 추가](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    다음 표에서 hello hello 양식에 hello 요소에 설명 합니다.

    | 속성 | 값 |
    | --- | --- |
    | 스크립트 선택 | toouse 선택 사용자 지정 스크립트 __사용자 지정__합니다. 그렇지 않은 경우 제공된 스크립트를 선택합니다. |
    | 이름 |Hello 스크립트 동작에 대 한 이름을 지정 합니다. |
    | Bash 스크립트 URI |가 호출 된 toocustomize hello 클러스터 hello URI toohello 스크립트를 지정 합니다. |
    | Head/Worker/Zookeeper |Hello 노드를 지정 (**h e a d**, **작업자**, 또는 **사육**) hello 사용자 정의 스크립트 실행 됩니다. |
    | 매개 변수 |Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다. |

    사용 하 여 hello __이 스크립트 동작이 계속__ 항목 toomake 있는지 hello 스크립트 작업을 확장 하는 동안 적용 됩니다.

5. 마지막으로 hello를 사용 하 여 **만들기** 단추 tooapply hello 스크립트 toohello 클러스터입니다.

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a>Azure PowerShell에서 클러스터를 실행 하는 스크립트 작업 tooa 적용

계속하기 전에 Azure PowerShell을 설치 및 구성했는지 확인하세요. 워크스테이션 toorun HDInsight PowerShell cmdlet을 구성 하는 방법에 대 한 정보를 참조 하십시오. [설치 Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

hello 다음 예제에서는 어떻게 tooapply 스크립트 동작 tooa 실행 중인 클러스터:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

Hello 작업이 완료 되 면 정보 비슷한 toohello를 텍스트 다음 나타납니다.

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a>Hello Azure CLI에서에서 클러스터를 실행 하는 스크립트 작업 tooa 적용

계속 하기 전에 설치 하 고 hello Azure CLI를 구성 했는지 확인 합니다. 자세한 내용은 참조 [설치 hello Azure CLI](../cli-install-nodejs.md)합니다.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. tooswitch tooAzure Resource Manager 모드로, 다음 hello 명령줄에서 명령을 사용 하 여 hello:

        azure config mode arm

2. Hello 다음 tooauthenticate tooyour Azure 구독을 사용 합니다.

        azure login

3. 다음 명령은 tooapply 클러스터를 실행 하는 스크립트 작업 tooa hello를 사용 하 여

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    이 명령에 대한 매개 변수를 생략한 경우 해당 매개 변수를 묻는 메시지가 나타납니다. 하는 경우 스크립트를 사용 하 여 지정한 hello `-u` 에서는 매개 변수를 지정할 수 있습니다 hello를 통해 `-p` 매개 변수입니다.

    유효한 노드 형식은 `headnode`, `workernode` 및 `zookeeper`입니다. Hello 스크립트는 노드 유형에 적용된 toomultiple 이어야 하 고, 경우에 hello 형식을 구분 하 여 지정 된 ';'. 예: `-n headnode;workernode`.

    toopersist hello 스크립트, 추가 hello `--persistOnSuccess`합니다. 사용 하 여 hello 스크립트를 나중에 유지할 수도 있습니다 `azure hdinsight script-action persisted set`합니다.

    Hello 작업이 완료 되 면 출력 유사한 toohello를 텍스트 다음 나타납니다.

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a>REST API를 사용 하 여 클러스터를 실행 하는 스크립트 작업 tooa 적용

[실행 중인 클러스터의 스크립트 작업](https://msdn.microsoft.com/library/azure/mt668441.aspx)을 참조하세요.

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a>Hello HDInsight.NET SDK에서에서 클러스터를 실행 하는 스크립트 작업 tooa 적용

Hello.NET SDK tooapply 스크립트 tooa 클러스터를 사용 하 여 예제를 보려면 [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action)합니다.

## <a name="view-history-promote-and-demote-script-actions"></a>기록 보기, 스크립트 작업 승격 및 강등

### <a name="using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여

1. Hello에서 [Azure 포털](https://portal.azure.com)를 HDInsight 클러스터를 선택 합니다.

2. Hello HDInsight 클러스터 개요에서 선택 hello **스크립트 동작** 바둑판식으로 배열입니다.

    ![스크립트 작업 타일](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > 선택할 수도 있습니다 **모든 설정을** 선택한 후 **스크립트 동작** hello 설정 섹션에서에서.

4. 이 클러스터에 대 한 스크립트의 기록은 hello 스크립트 동작 섹션에 표시 됩니다. 이 정보에는 지속된 스크립트 목록이 포함되어 있습니다. 아래 hello 스크린샷에서 Solr 스크립트 되었습니다.이 클러스터에서 실행 하는 hello를 볼 수 있습니다. hello 스크린 샷 지속형된 스크립트를 표시 하지 않습니다.

    ![스크립트 작업 섹션](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. Hello 기록에서 스크립트를 선택 하면이 스크립트에 대 한 hello 속성 섹션을 표시 됩니다. Hello 화면 hello 위에서 hello 스크립트를 다시 실행할 수도 있고 수준을 올릴 수 있습니다.

    ![스크립트 작업 속성](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. Hello를 사용할 수도 있습니다 **...**  toohello hello 스크립트 동작 섹션 tooperform 동작에 대 한 항목의 오른쪽입니다.

    ![스크립트 작업 ... 사용량](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Azure PowerShell 사용

| Hello 다음을 사용 하는 중... | 너무... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |지속형 스크립트 작업에 대한 정보 검색 |
| Get-AzureRmHDInsightScriptActionHistory |기록을 스크립트 적용 되는 동작 toohello 클러스터 또는 특정 스크립트에 대 한 세부 정보를 검색 합니다. |
| Set-AzureRmHDInsightPersistedScriptAction |임시 승격 스크립트 동작 tooa 지속형 스크립트 동작 |
| Remove-AzureRmHDInsightPersistedScriptAction |지속형된 스크립트 동작 tooan 임시 작업을 강등합니다. |

> [!IMPORTANT]
> 사용 하 여 `Remove-AzureRmHDInsightPersistedScriptAction` 스크립트에서 수행 하는 hello 동작 실행 취소 하지 않습니다. 이 cmdlet만 hello 지속형된 플래그를 제거합니다.

다음 예제 스크립트는 hello hello cmdlet toopromote를 사용 하 여 다음 스크립트의 수준을 내리려면 합니다.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여

| Hello 다음을 사용 하는 중... | 너무... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |지속형 스크립트 작업의 목록을 검색합니다. |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |특정 지속형 스크립트 작업에 대한 정보를 검색합니다. |
| `azure hdinsight script-action history list <clustername>` |스크립트 적용 되는 동작 toohello 클러스터의 기록을 검색합니다 |
| `azure hdinsight script-action history show <clustername> <scriptname>` |특정 스크립트 작업에 대한 정보 검색 |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |임시 승격 스크립트 동작 tooa 지속형 스크립트 동작 |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |지속형된 스크립트 동작 tooan 임시 작업을 강등합니다. |

> [!IMPORTANT]
> 사용 하 여 `azure hdinsight script-action persisted delete` 스크립트에서 수행 하는 hello 동작 실행 취소 하지 않습니다. 이 cmdlet만 hello 지속형된 플래그를 제거합니다.

### <a name="using-hello-hdinsight-net-sdk"></a>Hello HDInsight.NET SDK를 사용 하 여

Hello.NET SDK tooretrieve 스크립트 기록 하는 클러스터에서 사용 하는 예로, 승격 또는 스크립트의 수준을 내리려면, 참조 [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action)합니다.

> [!NOTE]
> 이 예제에서는 또한 tooinstall HDInsight를 통해 응용 프로그램에서.NET SDK를 hello 하는 방법을 보여 줍니다.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>HDInsight 클러스터에서 사용하는 오픈 소스 소프트웨어 지원

Microsoft Azure HDInsight 서비스 hello Hadoop 주위 형성 하는 오픈 소스 기술 프로그램 에코 시스템을 사용 합니다. Microsoft Azure는 오픈 소스 기술에 대한 일반 수준의 지원을 제공합니다. 자세한 내용은 참조 hello **지원 범위** hello 섹션 [Azure 지원 FAQ 웹 사이트](https://azure.microsoft.com/support/faq/)합니다. 기본 제공 구성 요소에 대 한 지원의 수준을 추가로 제공 하는 hello HDInsight 서비스입니다.

Hello HDInsight 서비스에서에서 사용할 수 있는 오픈 소스 구성 요소는 다음과 같은 두 종류가 있습니다.

* **기본 제공 구성 요소** -이 구성 요소는 HDInsight 클러스터에 미리 설치 되어 하며 hello 클러스터의 핵심 기능을 제공 합니다. 예를 들어 YARN ResourceManager, hello 하이브 쿼리 언어 (HiveQL) 및 hello Mahout 라이브러리 toothis 범주에 속합니다. 클러스터 구성 요소 전체 목록은 영어로 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능](hdinsight-component-versioning.md)합니다.
* **사용자 지정 구성 요소** -, hello 클러스터의 사용자로 설치 또는 hello 커뮤니티에서 사용할 수 있거나 사용자가 만든 모든 구성 요소를 작업에 사용 합니다.

> [!WARNING]
> Hello HDInsight 클러스터와 함께 제공 되는 구성 요소를 완전히 지원 됩니다. Microsoft 지원 tooisolate 주며 toothese 관련된 구성 요소 문제를 해결 합니다.
>
> 사용자 지정 구성 요소 상업적으로 적절 한 지원 toohelp 수신 하면 toofurther hello 문제를 해결 합니다. Microsoft 지원 수 tooresolve hello 문제 이거나 해당 기술에 대 한 심층 전문 지식이 있는 hello 오픈 소스 기술에 대 한 사용 가능한 채널 tooengage 요청할 수 있습니다. 예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다. Apache 프로젝트는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/)).

HDInsight 서비스 hello toouse 사용자 지정 구성 요소를 여러 가지 방법으로 제공합니다. hello 구성 요소는 사용 되거나 hello 클러스터에 설치 하는 것에 관계 없이 동일한 지원 수준으로 적용 됩니다. hello 다음 목록에서는 설명 hello 가장 일반적인 방법은 사용자 지정 구성 요소를 사용할 수 있도록 하는 HDInsight 클러스터에서:

1. 작업 제출-Hadoop 또는 기타 유형의 작업을 실행 하거나 사용자 지정 구성 요소를 사용 하 여 제출 된 toohello 클러스터가 될 수 있습니다.

2. 클러스터를 만드는 동안 클러스터 사용자 지정-추가 설정과 hello 클러스터 노드에 설치 된 사용자 지정 구성 요소를 지정할 수 있습니다.

3. 샘플-인기 있는 사용자 지정 구성 요소, Microsoft 등에 대 한 예제는 hello HDInsight 클러스터에서 이러한 구성 요소를 사용할 수 있는 방법을 제공할 수 있습니다. 이러한 샘플은 지원 없이 제공됩니다.

## <a name="troubleshooting"></a>문제 해결

스크립트 동작에 의해 기록 된 Ambari 웹 UI tooview 정보를 사용할 수 있습니다. 클러스터를 만드는 동안 실패 하면 hello 스크립트 hello 로그 hello 클러스터와 연결 된 hello 기본 저장소 계정에서 사용할 수 있습니다. 이 섹션에서는 이러한 두 옵션을 사용 하 여 tooretrieve hello을 기록 하는 방법을 설명 합니다.

### <a name="using-hello-ambari-web-ui"></a>Hello Ambari 웹 UI를 사용 하 여

1. 브라우저에서 toohttps://CLUSTERNAME.azurehdinsight.net 이동 합니다. CLUSTERNAME를 HDInsight 클러스터의 hello 이름을 바꿉니다.

    메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 계정 이름 (admin) 및 암호를 입력 합니다. Web form의 tooreenter hello에 대 한 관리자 자격 증명을 할 수 있습니다.

2. Hello hello 페이지 위쪽에 hello 모음에서 선택 hello **ops** 항목입니다. Ambari 통해 hello 클러스터에 대해 현재 및 이전 작업의 목록이 표시 됩니다.

    ![선택한 작업으로 Ambari 웹 UI 모음](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. 포함 된 찾기 hello 항목 **실행\_customscriptaction** hello에 **작업** 열입니다. 이러한 항목은 hello 스크립트 동작 실행 될 때 만들어집니다.

    ![작업의 스크린샷](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    tooview hello STDOUT 및 STDERR 출력 hello run\customscriptaction 항목을 선택 하 고 hello 링크를 통해 드릴 다운 합니다. Hello 스크립트를 실행 하는 경우이 출력이 생성 되 고 유용한 정보를 포함할 수 있습니다.

### <a name="access-logs-from-hello-default-storage-account"></a>Hello 기본 저장소 계정에서 액세스 로그

Hello 클러스터 만들기 tooa 스크립트 작업 오류 때문에 실패 하면 hello 로그 hello 클러스터 저장소 계정에서 액세스할 수 있습니다.

* hello 저장소 로그에서 제공 됩니다 `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`합니다.

    ![작업의 스크린샷](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    이 디렉터리 아래의 hello 로그 헤드 노드에, workernode, 및 사육 노드를 개별적으로 구성 됩니다. 일부 사례:

    * **헤드 노드** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **작업자 노드** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Zookeeper 노드** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* 모든 stdout 및 stderr hello 해당 호스트의 toohello 저장소 계정에 업로드 합니다. 각 스크립트 동작마다 하나의 **output-\*.txt** 및 **errors-\*.txt**가 있습니다. hello 출력 *.txt 파일 내용이 hello 호스트에서 실행 하는 hello 스크립트의 hello URI에 대 한 정보를 포함 합니다. 예를 들면 다음과 같습니다.

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* Hello로 스크립트 작업 클러스터를 만드는 반복 해 서 수 같은 이름입니다. 이러한 경우 hello 날짜 폴더 이름에 따라 hello 관련 로그를 구별할 수 있습니다. 예를 들어 서로 다른 날짜에 만든 클러스터 (mycluster)에 대 한 폴더 구조 hello 로그 항목을 다음 유사한 toohello 나타납니다.

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* Hello로 스크립트 작업 클러스터를 만드는 경우 이름과 같은 이름을 hello에 동일 날짜, hello 고유한 접두사 tooidentify hello 관련 로그 파일을 사용할 수 있습니다.

* 클러스터 근처 오전 12시 (자정)를 만들 경우 2 일 걸쳐 hello 로그 파일 수입니다. 이러한 경우에 hello에 대 한 두 개의 서로 다른 날짜 폴더 표시 동일한 클러스터입니다.

* 업로드 로그 파일 toohello 기본 컨테이너 큰 클러스터를 위해 특별히 too5 분 정도 걸릴 수 있습니다. 따라서 tooaccess hello 로그 하려면 삭제 하면 안 즉시 hello 클러스터 경우 스크립트 작업이 실패 합니다.

### <a name="ambari-watchdog"></a>Ambari 감시

> [!WARNING]
> Linux 기반 HDInsight 클러스터에 Ambari 감시 (hdinsightwatchdog) hello에 대 한 hello 암호를 변경 하지 마십시오. 이 계정에 대 한 hello 암호를 변경할 hello HDInsight 클러스터에서 hello 기능 toorun 새 스크립트 동작을 중단합니다.

### <a name="cant-import-name-blobservice"></a>이름 BlobService를 가져올 수 없음

__증상__: hello 스크립트 동작이 실패 합니다. Ambari에서 hello 작업을 볼 때 텍스트 비슷한 toohello 다음 오류가 표시 됩니다.

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__원인__: hello HDInsight 클러스터에 포함 되어 있는 hello Python Azure 저장소 클라이언트를 업그레이드 하는 경우이 오류가 발생 합니다. HDInsight는 Azure Storage 클라이언트 0.20.0을 예상합니다.

__해상도__: tooresolve이이 오류를 수동으로 사용 하 여 tooeach 클러스터 노드를 연결 `ssh` 명령 tooreinstall hello 올바른 저장소 클라이언트 버전에 따라 사용 하 여 hello:

```
sudo pip install azure-storage==0.20.0
```

SSH 사용 하는 연결 toohello 클러스터에 대 한 자세한 내용은 참조 [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md)합니다.

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>클러스터를 만드는 동안 기록에 스크립트가 표시되지 않음

2016년 3월 15일 전에 클러스터를 만든 경우에는 스크립트 작업 기록에 항목이 나타나지 않을 수 있습니다. 2016 년 3 월 15 일 후 hello 클러스터 크기를 조정 하면 클러스터를 만드는 동안 사용 하 여 hello 스크립트 기록에 표시 적용 되는 크기 조정 작업 hello의 일환으로 hello 클러스터의 toonew 노드.

두 가지 예외 사항이 있습니다.

* 클러스터가 2015년 9월 1일 전에 생성되었습니다. 스크립트 작업이 이 날에 도입되었습니다. 따라서 이 날짜 이전에 생성된 클러스터는 클러스터 생성에 스크립트 작업이 사용되지 않았습니다.

* 클러스터를 만드는 동안 여러 스크립트 작업을 사용 하 고 동일한 여러 스크립트에 대 한 이름을 지정 하거나 hello hello를 사용 하는 경우 동일한 이름, 여러 스크립트에 대 한 서로 다른 매개 변수 이지만 동일한 URI입니다. 이러한 경우 hello 다음 오류가 나타날 수 있습니다.

    기존 스크립트의 스크립트 이름 tooconflicting 인해이 클러스터에서 동작은 수 없는 새 스크립트를 실행 했습니다. 클러스터 만들기에 제공되는 스크립트 이름이 모두 고유해야 합니다. 크기 조정에 기존 스크립트가 실행됩니다.

## <a name="next-steps"></a>다음 단계

* [HDInsight용 스크립트 작업 스크립트 개발](hdinsight-hadoop-script-actions-linux.md)
* [HDInsight 클러스터에 Solr 설치 및 사용](hdinsight-hadoop-solr-install-linux.md)
* [HDInsight 클러스터에 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install-linux.md)
* [추가 저장소 tooan HDInsight 클러스터를 추가 합니다.](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "클러스터를 만드는 동안의 단계"
