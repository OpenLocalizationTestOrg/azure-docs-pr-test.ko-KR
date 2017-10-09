---
title: "HDInsight-Azure와 액션 개발 aaaScript | Microsoft Docs"
description: "스크립트 동작을 가진 toocustomize Hadoop 클러스터 하는 방법에 대해 알아봅니다. 스크립트 동작 사용된 tooinstall 클러스터에 설치 된 응용 프로그램의 Hadoop 클러스터 또는 toochange hello 구성에서 실행 되는 추가 소프트웨어를 수 있습니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a>HDInsight Windows 기반 클러스터용 스크립트 작업 스크립트 개발
스크립트 동작 toowrite HDInsight에 대 한 스크립트 하는 방법에 대해 알아봅니다. 스크립트 동작 스크립트 사용에 대한 자세한 내용은 [스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md)을 참조하세요. Linux 기반 HDInsight 클러스터를 용으로 작성 된 동일한 문서의 hello에 대 한 참조 [HDInsight에 대 한 스크립트 작업 개발 스크립트](hdinsight-hadoop-script-actions-linux.md)합니다.



> [!IMPORTANT]
> hello 단계에서 Windows 기반 HDInsight 클러스터에 대 한이 문서 에서만 작동 합니다. HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요. Linux 기반 클러스터로 스크립트 작업 사용에 대한 정보는 [HDInsight를 사용하여 스크립트 작업 개발(Linux)](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.
>
>



스크립트 동작 사용된 tooinstall 클러스터에 설치 된 응용 프로그램의 Hadoop 클러스터 또는 toochange hello 구성에서 실행 되는 추가 소프트웨어를 수 있습니다. 스크립트 작업은 HDInsight 클러스터를 구축할 때 hello 클러스터 노드에서 실행 되는 스크립트 및 hello 클러스터의 노드 HDInsight 구성을 완료 한 후 실행 됩니다. 스크립트 작업을 시스템 관리자 계정 권한으로 실행 되 고 읽기/쓰기 권한 toohello 클러스터 노드를 제공 합니다. 각 클러스터는 지정 된 hello 순서로 실행 하는 스크립트 작업 toobe 목록과 함께 제공 될 수 있습니다.

> [!NOTE]
> Hello 다음과 같은 오류 메시지가 발생 하면:
>
> System.Management.Automation.CommandNotFoundException; ExceptionMessage: hello 용어 ' 저장 HDIFile' 인식 되지 않습니다는 cmdlet, 함수, 스크립트 파일 또는 실행 프로그램의 hello 이름으로 합니다. Hello hello 이름이 올바른지 확인 하거나 경로 포함 한 경우 해당 hello 경로가 올바른지 확인 하 고 다시 시도 하십시오.
> Hello 도우미 메서드를 포함 하지 않은 것입니다.  [사용자 지정 스크립트에 대한 도우미 메서드](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts)를 참조하세요.
>
>

## <a name="sample-scripts"></a>샘플 스크립트
Windows 운영 체제에서 HDInsight 클러스터를 만들기 위해 hello 스크립트 작업은 Azure PowerShell 스크립트입니다. hello 다음 스크립트는 hello 사이트 구성 파일을 구성 하기 위한 예제:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

hello 스크립트는 4 개의 매개 변수, hello 구성 파일 이름, toomodify, hello 값 tooset, 및 설명을 표시할 hello 등록 합니다. 예:

    hive-site.xml hive.metastore.client.socket.timeout 90

이러한 매개 변수는 hello hive.metastore.client.socket.timeout 값 too90 hello hive-site.xml 파일에 설정 합니다.  hello 기본값은 60 초입니다.

이 샘플 스크립트는 [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1)에도 나옵니다.

HDInsight은 HDInsight 클러스터에서 여러 스크립트 tooinstall 추가 구성 요소를 제공 합니다.

| 이름 | 스크립트 |
| --- | --- |
| **Spark 설치** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. [HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]을 참조하세요. |
| **R 설치** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. [HDInsight 클러스터에서 R 설치 및 사용][hdinsight-r-scripts]을 참조하세요. |
| **Solr 설치** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. [HDInsight 클러스터에서 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)을 참조하세요. |
| - **Giraph 설치** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. [HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)을 참조하세요. |

스크립트 동작에는 hello HDInsight.NET SDK를 사용 하 여 하거나 hello Azure 포털, Azure PowerShell에서에서 배포할 수 있습니다.  자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]을 참조하세요.

> [!NOTE]
> hello 예제 스크립트는 HDInsight 클러스터 버전이 3.1은만 이상 버전에 작동합니다. HDInsight 클러스터 버전에 대한 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.
>
>

## <a name="helper-methods-for-custom-scripts"></a>사용자 지정 스크립트에 대한 도우미 메서드
스크립트 작업 도우미 메서드는 사용자 지정 스크립트를 쓰는 동안 사용할 수 있는 유틸리티입니다. 에 정의 된 이러한 메서드가 [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), 다음 예제는 hello를 사용 하 여 스크립트에 포함 될 수 있습니다.

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

이 스크립트에 의해 제공 되는 hello 도우미 메서드는 다음과 같습니다.

| 도우미 메서드 | 설명 |
| --- | --- |
| **Save-HDIFile** |Hello Azure VM 노드 할당된 toohello 클러스터와 연결 된 hello 로컬 디스크에서 식별자 URI (Uniform Resource) tooa 위치를 지정 하는 hello에서 파일을 다운로드 합니다. |
| **Expand-HDIZippedFile** |압축된 파일의 압축을 풉니다. |
| **Invoke-HDICmdScript** |cmd.exe에서 스크립트를 실행합니다. |
| **Write-HDILog** |스크립트 작업에 사용 된 hello 사용자 지정 스크립트에서 출력을 씁니다. |
| **Get-Services** |Hello 컴퓨터에서 실행 중인 hello 스크립트를 실행 하는 서비스의 목록을 가져옵니다. |
| **Get-Service** |입력으로 hello 특정 서비스 이름으로 특정 서비스에 대 한 자세한 정보를 가져올 (서비스 이름, 프로세스 ID, 상태, 등) hello 컴퓨터 hello 스크립트를 실행 합니다. |
| **Get-HDIServices** |Hello 컴퓨터에서 실행 중인 hello 스크립트를 실행 하는 HDInsight 서비스의 목록을 가져옵니다. |
| **Get-HDIService** |Hello 특정 HDInsight 서비스 이름으로 입력으로, 특정 서비스에 대 한 자세한 정보를 가져올 (서비스 이름, 프로세스 ID, 상태, 등) hello 컴퓨터 hello 스크립트를 실행 합니다. |
| **Get-ServicesRunning** |Hello 컴퓨터에서 실행 중인 hello 스크립트를 실행 하는 서비스의 목록을 가져옵니다. |
| **Get-ServiceRunning** |특정 서비스 이름 사용 하 여 실행 중인지 확인 hello 컴퓨터에서 hello 스크립트를 실행 합니다. |
| **Get-HDIServicesRunning** |Hello 컴퓨터에서 실행 중인 hello 스크립트를 실행 하는 HDInsight 서비스의 목록을 가져옵니다. |
| **Get-HDIServiceRunning** |경우 특정 HDInsight 서비스 이름 사용 하 여 컴퓨터에서 실행 중인 hello hello 스크립트가 실행 되는 위치를 확인 합니다. |
| **Get-HDIHadoopVersion** |Hadoop hello 스크립트를 실행 하는 hello 컴퓨터에 설치 된 hello 버전을 가져옵니다. |
| **Test-IsHDIHeadNode** |헤드 노드 hello 스크립트를 실행 하는 hello 컴퓨터 인지 확인 합니다. |
| **Test-IsActiveHDIHeadNode** |Hello 스크립트를 실행 하는 hello 컴퓨터 활성 헤드 노드에 있는지 확인 하십시오. |
| **Test-IsHDIDataNode** |데이터 노드 hello 스크립트를 실행 하는 hello 컴퓨터 인지 확인 합니다. |
| **Edit-HDIConfigFile** |Hello config 파일 hive-site.xml, 코어 site.xml, hdfs-site.xml, mapred-site.xml, 또는 yarn-site.xml 편집 합니다. |

## <a name="best-practices-for-script-development"></a>스크립트 개발을 위한 모범 사례
HDInsight 클러스터에 대 한 사용자 지정 스크립트를 개발할 때 염두에 몇 가지 모범 사례 tookeep 가지 있습니다.

* Hello Hadoop 버전을 확인

    HDInsight 버전 3.1 (Hadoop 2.4) 이상과 tooinstall 사용자 지정 스크립트 동작 구성 요소를 사용 하 여 클러스터에서 지원 합니다. 사용자 지정 스크립트에서 hello를 사용 해야 **Get HDIHadoopVersion** hello 스크립트에서 다른 작업을 수행 합니다. 계속 하기 전에 도우미 메서드 toocheck hello Hadoop 버전입니다.
* 안정적인 tooscript 리소스 링크를 제공 합니다.

    사용자가 확인 해야 모든 hello 스크립트와 클러스터의 hello 사용자 지정에 사용 되는 다른 아티팩트 계속 hello 클러스터의 hello 수명 주기 동안 사용할 수 및 이러한 파일의 hello 버전 hello 기간에 대 한 변경 되지 않습니다. 이러한 리소스는 hello hello 클러스터 노드를 이미지로 다시 설치 해야 하는 경우에 필요 합니다. hello 가장 좋은 방법은 toodownload 이며 사용자 정의 컨트롤 hello 저장소 계정에 모든 항목을 보관 합니다. 이 hello 기본 저장소 계정 또는 사용자 지정 된 클러스터에 대 한 배포의 hello 타임에 지정한 hello 추가 되는 저장소 계정 수 있습니다.
    Hello에서 Spark와 R 사용자 지정 클러스터 샘플 hello 설명서의 예를 들어 기능이 되었습니다 hello 리소스의 로컬 복사본을이 저장소 계정을 제공: https://hdiconfigactions.blob.core.windows.net/ 합니다.
* Hello 클러스터 사용자 지정 스크립트가 idempotent 인지 확인

    Hello 클러스터 수명 동안 HDInsight 클러스터의 노드 hello를 이미지로 다시 설치를 예상 해야 합니다. 클러스터를 이미지로 다시 설치할 때마다 hello 클러스터 사용자 지정 스크립트가 실행 됩니다. 이 스크립트를 이미지로 다시 설치 시 hello 스크립트 해당 hello 클러스터 상태에 있었던 경우 hello 클러스터 처음부터 처음으로 hello에 대 한 hello 스크립트 실행 한 후에 사용자 지정 된 동일한 toohello 반환 확인 해야 하는 hello 의미에서 설계 된 toobe idempotent 있어야 합니다. 만들어집니다. 예를 들어 사용자 지정 스크립트에 D:\AppLocation에서 응용 프로그램을 설치 하는 경우 첫 번째 실행 한 다음, 이미지로 다시 설치 시 각 후속 실행 시 hello 스크립트 hello 응용 프로그램 hello 다른를 계속 하기 전에 D:\AppLocation 위치에 있는지 여부를 확인 해야 hello 스크립트의 단계입니다.
* Hello 최적의 위치에 사용자 지정 구성 요소를 설치 합니다.

    클러스터 노드를 이미지로 다시 설치 되 면 hello C:\ 리소스 드라이브 및 D:\ 드라이브 수를 다시 포맷, 데이터 및 해당 드라이브에 설치 하는 응용 프로그램의 hello 손실. 또한 hello 클러스터의 일부인 Azure 가상 컴퓨터 (VM) 노드는 작동이 중단 되며 새 노드도 대체 됩니다 하는 경우 발생할 수 있습니다. Hello 클러스터에서 hello C:\apps 위치 또는 hello D:\ 드라이브에 구성 요소를 설치할 수 있습니다. Hello C:\ 드라이브에서 다른 위치에 모두 예약 됩니다. Hello 응용 프로그램 또는 라이브러리 놓이는 위치 toobe hello 클러스터 사용자 지정 스크립트에 설치를 지정 합니다.
* Hello 클러스터 아키텍처의 고가용성을 보장

    HDInsight는 액티브-패시브 아키텍처 고가용성을 위해, 헤드 노드는 어느 한 헤드 노드는 활성 모드 (hello HDInsight 서비스 실행)이 고 다른 hello에서 (어떤 HDInsight에서 서비스가 실행 되지 않는) 대기 모드에 됩니다. HDInsight 서비스는 중단 되는 경우 활성 노드와 수동 모드를 전환 하는 hello 노드. 고가용성을 위해 두 헤드 노드에 사용 되는 tooinstall 서비스 스크립트 동작을 사용 하는 경우 해당 hello HDInsight 장애 조치 메커니즘 않습니다 수 tooautomatically 장애가 사용자 설치 서비스를 대신 note 합니다. 따라서 사용자 설치 서비스를 HDInsight 헤드 노드에 항상 사용 가능한 예상된 toobe 액티브-패시브 모드에 있는 경우 장애 조치 메커니즘이 자신의 하거나 액티브-액티브 모드로 설정 해야 해야 합니다.

    Hello 헤드 노드 역할 hello에 값으로 지정 하는 경우 헤드 노드 모두에서 실행 되는 HDInsight 스크립트 동작 명령 *ClusterRoleCollection* 매개 변수입니다. 따라서 사용자 지정 스크립트를 설계할 때는 스크립트에서 이 설정을 인식하는지 확인해야 합니다. 여기서 hello 동일한 서비스 설치 되 고 hello 헤드 노드 모두에서 시작 하 고 서로 경쟁 결국 문제를 실행 하지 마십시오. 또한, 주의 이미지로 다시 설치 하는 동안 데이터는 손실 되므로 스크립트 동작을 통해 설치 된 소프트웨어는 toobe 탄력적인 toosuch 이벤트입니다. 응용 프로그램 디자인 된 toowork 여러 노드 간에 분산 되는 항상 사용 가능한 데이터를 사용 해야 합니다. 클러스터의 노드 hello의 1/5로 수 이미지로 다시 설치할 수 hello에 참고 동시 합니다.
* Hello 사용자 지정 구성 요소 toouse Azure Blob 저장소 구성

    hello 클러스터 노드에 설치 하는 hello 사용자 지정 구성 요소는 기본 구성 toouse Hadoop 분산 파일 시스템 (HDFS) 저장소에 있을 수 있습니다. Hello 구성 toouse Azure Blob 저장소를 대신 변경 해야 합니다. 클러스터에 이미지로 다시 설치 hello HDFS 파일 시스템 포맷 가져옵니다 하 고 저장 된 모든 데이터는 손실 됩니다. 대신 Azure Blob Storage를 사용하면 데이터가 유지됩니다.

## <a name="common-usage-patterns"></a>일반적인 사용 패턴
이 섹션에서 사용자 고유의 사용자 지정 스크립트를 작성 하는 동안에 실행 될 수 있는 hello 일반적인 사용 패턴을 구현 지침을 제공 합니다.

### <a name="configure-environment-variables"></a>환경 변수 구성
종종 스크립트 작업 개발 중 이며 보이면 hello tooset 환경 변수를 필요 합니다. 예를 들어 가장 가능성이 높은 시나리오는 이진 외부 사이트에서 다운로드 하 고 hello 클러스터에 설치 위치는 설치 된 tooyour 'PATH' 환경 변수의 hello 위치를 추가 합니다. 다음 코드 조각 hello tooset 환경 변수에서 사용자 지정 스크립트를 hello 하는 방법을 보여 줍니다.

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

Hello 환경 변수를 설정 하는이 문을 **MDS_RUNNER_CUSTOM_CLUSTER** toohello 값 'true' 및 집합 hello이 변수 toobe 전체 컴퓨터의 범위. 시간에 반드시 환경 변수 hello 적절 한 범위-컴퓨터 또는 사용자에서 설정 됩니다. 환경 변수 설정에 대한 자세한 내용은 [여기][1]를 참조하세요.

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Hello 사용자 지정 스크립트를 저장할 toolocations 액세스
사용 되는 스크립트 toocustomize 클러스터 요구 tooeither hello 클러스터에 대 한 hello 기본 저장소 계정 또는 다른 저장소 계정에 읽기 전용 컨테이너를 공용 이어야 합니다. 공개적으로 액세스할 수 있는 toobe 작업이 필요한 스크립트 리소스의 다른 위치 액세스 하는 경우 (적어도 공개 읽기 전용). 예를 들어 tooaccess 파일을 원하는 하 고 hello SaveFile HDI 명령을 사용 하 여 저장할 수 있습니다.

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

이 예제에서는 해당 hello 컨테이너 'somecontainer' 저장소 계정 'somestorageaccount'에 공개적으로 액세스할 수 있어야 합니다. 그렇지 않으면 hello 스크립트 ' 찾을 수 없음 ' 예외를 throw 하 고 실패 합니다.

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a>추가 AzureRmHDInsightScriptAction toohello cmdlet 매개 변수 전달
toopass 여러 매개 변수 추가 AzureRmHDInsightScriptAction toohello cmdlet hello 스크립트에 대 한 tooformat hello 문자열 값 toocontain 모든 매개 변수가 필요 합니다. 예:

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

또는

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a>실패한 클러스터 배포에 대한 예외 발생
Tooget hello 팩트의 정확 하 게 알림이 표시 하려는 경우 클러스터 사용자 지정 예상 대로 실패을 중요 한 toothrow 예외로 hello 클러스터 만들기 실패 합니다. 예를 들어,이 특성이 있으면 tooprocess 파일을 사용할 수도 있으며 hello 파일이 존재 하지 않습니다 hello 오류 사례를 처리할 수 있습니다. 이렇게 하면 hello 스크립트 정상적으로 종료 하 고 hello hello 클러스터 상태가 올바르게 알려져 있습니다. hello 다음 조각은 방법의 예로 tooachieve이:

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

이 코드 조각에서 hello 파일 존재 하지 않는 경우 hello 스크립트 hello 오류 메시지를 인쇄 후 정상적으로 실제로 종료 하 고 hello 클러스터에 클러스터 사용자 지정 프로세스를 완료 "했습니다" 것으로 가정 하는 실행 중인 상태에 도달 하면 있는 tooa 상태를 저하 합니다. Toobe hello 팩트의 정확 하 게 알림이 표시 하려는 경우 해당 클러스터 사용자 지정 항목 기본적으로 완료 하지 못했습니다 된 누락 된 파일로 인해 예상 대로 더 적절 한 toothrow 예외는 hello 클러스터 사용자 지정 단계에 실패 합니다. tooachieve이 샘플 코드 조각은 대신 다음 hello를 사용 해야 합니다.

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a>스크립트 작업 배포를 위한 검사 목록
이러한 스크립트 toodeploy를 준비할 때 했습니다 hello 단계는 다음과 같습니다.

1. Hello 배포 하는 동안 hello 클러스터 노드에서 액세스할 수 있는 위치에서 사용자 지정 스크립트를 포함 하는 hello 파일을 넣습니다. 이 hello 기본 또는 클러스터 배포 또는 다른 공개적으로 액세스할 수 있는 저장소 컨테이너의 hello 시 지정 하는 추가 저장소 계정 수 있습니다.
2. 스크립트 toomake 보내지게를 실행 하 고 있는지에 대 한 검사를 추가 하 여 hello 스크립트 hello에 여러 번 실행 될 수 있도록 동일한 노드.
3. 사용 하 여 hello **Write-output** STDERR 뿐만 아니라 Azure PowerShell cmdlet tooprint tooSTDOUT 합니다. **Write-Host**를 사용하지 마세요.
4. $Env 같은 임시 파일 폴더를 사용 하 여: 임시 tookeep hello 스크립트에서 사용 하는 다운로드 한 파일 hello 및 다음 스크립트를 실행 한 후를 정리 합니다.
5. D:\ 또는 C:\apps에만 사용자 지정 소프트웨어를 설치합니다. Hello c: 드라이브에서 다른 위치에는 예약 되어으로 사용할 수 없습니다. Note hello C:\apps 폴더 외부 hello c: 드라이브에 파일을 설치 hello 노드의 reimages 하는 동안 설치 오류가 발생할 수 있습니다.
6. Hello 이벤트의 운영 체제 수준을 설정 또는 Hadoop 서비스 구성 파일 변경 된 경우에 hello 스크립트에서 설정 하는 hello 환경 변수와 같은 모든 운영 체제 수준 설정을 선택할 수 없도록 toorestart HDInsight 서비스를 지정할 수 있습니다.

## <a name="debug-custom-scripts"></a>사용자 지정 스크립트 디버그
hello 스크립트 오류 로그는 생성 시 hello 클러스터에 대해 지정한 hello 기본 저장소 계정에서 다른 출력과 함께 저장 됩니다. hello 로그 테이블에 저장 됩니다는 hello 이름의 *u < \cluster-name-fragment >< \time-stamp > setuplog*합니다. 이들은 hello 노드 (작업자 노드 및 헤드 노드)는 hello에 스크립트 hello 클러스터에서 실행 된 모든 레코드가 있는 집계 로그입니다.
Visual Studio 용 HDInsight 도구는 쉽게 toocheck hello 로그는 toouse 합니다. Hello 도구를 설치 하기 위한 참조 [HDInsight에 대 한 Visual Studio Hadoop 도구 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)

**Visual Studio를 사용 하 여 toocheck hello 로그**

1. Visual Studio를 엽니다.
2. **보기**를 클릭하고 **서버 탐색기**를 클릭합니다.
3. "Azure" 단추로 클릭 하 고, 연결을 너무 클릭**Microsoft Azure 구독**, 한 다음 자격 증명을 입력 합니다.
4. 확장 **저장소**, hello 기본 파일 시스템으로 사용 하는 hello Azure 저장소 계정, **테이블**, hello 테이블 이름을 두 번 클릭 합니다.

클러스터 노드 toosee hello에도 원격 수 STDOUT 및 STDERR에 대 한 사용자 지정 스크립트를 모두 합니다. hello 각 노드의 로그만 특정 toothat 노드 되며 로그인 **C:\HDInsightLogs\DeploymentAgent.log**합니다. 이러한 로그 파일 hello 사용자 지정 스크립트의 모든 출력을 기록합니다. Spark 스크립트 작업에 대한 예제 로그 조각은 다음과 같습니다.

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


이 로그에이 명확한 경우 hello Spark 스크립트 동작이 hello HEADNODE0 이라는 VM에서 실행 되 고 예외가 hello 실행 하는 동안 throw 되었습니다.

실행 오류가 발생 하는 hello 이벤트에서 것을 설명 하는 hello 출력이 로그 파일에도 포함 됩니다. 이러한 로그에 제공 된 hello 정보 발생할 수 있는 스크립트 문제 디버깅에 유용 합니다.

## <a name="see-also"></a>참고 항목
* [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]
* [HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]
* [HDInsight 클러스터에서 R 설치 및 사용][hdinsight-r-scripts]
* [HDInsight 클러스터에 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)
* [HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
