---
title: "Azure Machine Learning 실험 실행 서비스 개요"
description: "이 문서는 Azure Machine Learning 실험 실행 서비스의 고급 개요를 제공함"
services: machine-learning
author: gokhanuluderya-msft
ms.author: gokhanu
manager: haining
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 09/17/2017
ms.openlocfilehash: bb1c7d318939c42edb9a51e28dec31593f2485f9
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="overview-of-azure-machine-learning-experiment-execution-service"></a>Azure Machine Learning 실험 실행 서비스 개요
Azure ML(Azure Machine Learning) 실험 실행 서비스를 사용하면 데이터 과학자가 Azure ML의 실행 및 실행 관리 기능을 사용하여 실험을 실행할 수 있습니다. 이는 빠른 반복과 함께 빠른 실험 프레임워크를 제공합니다. Azure ML Workbench를 사용하면 컴퓨터에서 로컬 실행으로 시작하고 GPU 또는 Spark를 실행하는 HDInsight 클러스터를 포함한 원격 Data Science VM 등의 다른 환경으로 확장할 수 있습니다.

실험 실행 서비스는 격리되고 재현 가능하고 일관성 있는 실험 실행을 제공하기 위한 기능입니다. 이는 계산 대상, 실행 환경 및 실행 구성을 관리하는 데 도움이 됩니다. Azure ML Workbench 실행 및 실행 관리 기능을 사용하면 서로 다른 환경 간에 쉽게 이동할 수 있습니다. 

Azure ML Workbench 프로젝트에서 로컬로 또는 클라우드에서 크기에 따라 Python 또는 PySpark 스크립트를 실행할 수 있습니다. 

다음 환경에서 스크립트를 실행할 수 있습니다. 

* Azure ML Workbench에 의해 로컬 컴퓨터에 설치한 Python(3.5.2) 환경.
* 로컬 컴퓨터의 Docker 컨테이너 내부에 있는 conda Python 환경
* 원격 Linux 컴퓨터의 Docker 컨테이너 내부에 있는 conda Python 환경. 예를 들어 [Azure의 Ubuntu 기반 DSVM](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.linux-data-science-vm-ubuntu)
* Azure의 [Spark용 HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/)

>[!IMPORTANT]
>Azure ML 실행 서비스는 현재 Python 및 Spark 런타임 버전으로 Python 3.5.2 및 Spark 2.1.11을 각각 지원합니다. 


## <a name="key-concepts-in-azure-ml-experiment-execution"></a>Azure ML 실험 실행의 주요 개념
Azure ML 실험 실행의 다음과 같은 개념을 이해해야 합니다. 이후 섹션에서 이러한 개념을 사용 하는 방법을 자세히 설명합니다. 
### <a name="compute-target"></a>계산 대상
계산 대상은 사용자의 데스크톱, VM의 원격 Docker 또는 클러스터 등과 같은 사용자의 프로그램을 실행하는 위치를 지정합니다. 계산 대상은 사용자가 주소 지정 및 액세스할 수 있어야 합니다. Azure ML Workbench에서는 Workbench 응용 프로그램 및 CLI를 사용하여 계산 대상을 만들고 관리할 수 있습니다. 

CLI의 _az ml computetarget attach_ 명령을 사용하면 실행에 사용할 수 있는 계산 대상을 만들 수 있습니다.

### <a name="supported-compute-targets-are"></a>지원되는 계산 대상은 다음과 같습니다.
* Azure ML Workbench가 설치한 사용자 컴퓨터의 로컬 Python(3.5.2) 환경.
* 사용자 컴퓨터의 로컬 Docker
* Linux-Ubuntu VM의 원격 Docker. 예를 들어 [Azure의 Ubuntu 기반 DSVM](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.linux-data-science-vm-ubuntu)
* Azure의 [Spark 클러스터용 HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/)

Azure ML 실행 서비스는 현재 Python 및 Spark 런타임 버전으로 Python 3.5.2 및 Spark 2.1.11을 각각 지원합니다. 

>[!IMPORTANT]
> Docker를 실행하는 Windows VM은 원격 계산 대상으로 지원되지 **않습니다**.

### <a name="execution-environment"></a>실행 환경
실행 환경은 Azure ML Workbench에서 프로그램을 실행하는 데 필요한 런타임 구성 및 종속성을 정의합니다.

사용자는 Azure ML Workbench 기본 런타임에서 실행하는 경우 자신이 즐겨 쓰는 도구 및 패키지 관리자를 사용하여 로컬 실행 환경을 관리합니다. 

Conda는 로컬 Docker와 원격 Docker 실행 및 HDInsigh 기반 실행을 관리하는 데 사용됩니다. 이러한 계산 대상의 경우 실행 환경 구성은 **Conda_dependencies.yml** 및 **Spark_dependencies.yml 파일**을 통해 관리됩니다. 이 파일들은 프로젝트 내의 **aml_config** 폴더에 있습니다.

**실행 환경을 위해 지원되는 런타임:**
* Python 3.5.2
* Spark 2.1.11

### <a name="run-configuration"></a>실행 구성
계산 대상과 실행 환경 외에도 Azure ML은 실행 구성을 정의 및 변경하기 위한 프레임워크를 제공합니다. 실험의 서로 다른 실행을 위해 반복 실험의 일부로 서로 다른 구성이 필요할 수 있습니다. 서로 다른 데이터 소스를 사용하여 서로 다른 매개 변수 범위를 비우고 Spark 매개 변수를 튜닝할 수 있습니다. Azure ML 실행 서비스는 실행 구성을 관리하기 위한 프레임워크를 제공합니다.

_az ml computetarget attach_ 명령을 실행하면 프로젝트의 **aml_config** 폴더에 다음 규칙에 따라 .compute 및 .runconfig가 생성됩니다. _<your_computetarget_name>.compute_ 및 _<your_computetarget_name>.runconfig_. .runconfig 파일은 계산 대상을 만들 때 사용자의 편의를 위해 자동으로 생성됩니다. CLI에서 _az ml runconfigurations_ 명령을 사용하여 다른 실행 구성을 만들고 관리할 수 있습니다. 또한 사용자의 파일 시스템에서 이들을 만들고 편집할 수도 있습니다.

그리고 Azure ML Workbench의 실행 구성을 사용하여 환경 변수를 지정할 수 있습니다. .runconfig 파일에 다음 섹션을 추가하여 환경 변수를 지정하고 해당 환경 변수를 코드에 사용할 수 있습니다. 

```
EnvironmentVariables:
"EXAMPLE_ENV_VAR1": "Example Value1"
"EXAMPLE_ENV_VAR2": "Example Value2"
```

이러한 환경 변수는 사용자의 코드에서 액세스할 수 있습니다. 예를 들어 이 Phyton 코드 조각은 "EXAMPLE_ENV_VAR1"이라는 환경 변수를 인쇄함
```
print(os.environ.get("EXAMPLE_ENV_VAR1"))
```

_**다음 그림은 초기 실험 실행에 대한 고급 흐름을 보여 줍니다.**_
![](media/experiment-execution-configuration/experiment-execution-flow.png)

## <a name="azure-ml-experiment-execution-scenarios"></a>Azure ML 실험 실행 시나리오
이 시나리오에서는 실행 시나리오를 자세히 살펴보고 Azure ML이 실험을 실행하는 방법, 구체적으로 원격 VM 및 HDInsight 클러스터에서 실험을 로컬로 실행하는 방법을 알아봅니다. 이 섹션에서는 계산 대상 만들기에서 시작하여 실험 실행까지 훑어봅니다.

>[!NOTE]
>이 문서의 나머지 부분에서는 CLI(명령줄 인터페이스) 명령을 사용하여 개념 및 기능을 보여 줍니다. 여기서 설명하는 기능은 Workbench 데스크톱 응용 프로그램에서도 사용할 수 있습니다.

## <a name="launching-the-cli"></a>CLI 시작
CLI를 시작하는 쉬운 방법은 Azure ML Workbench 데스크톱 응용 프로그램에서 프로젝트를 열고 **파일-->명령 프롬프트 열기**로 이동하는 것입니다.

![](media/experiment-execution-configuration/opening-cli.png)

이 명령은 현재 프로젝트 폴더의 스크립트를 실행하는 명령을 입력할 수 있는 터미널 창을 시작합니다. 이 터미널 창은 Workbench가 설치하는 Python 3.5.2 환경을 사용하여 구성됩니다.

>[!NOTE]
> 명령 창에서 임의의 _az ml_ 명령을 실행하는 경우 Azure에 대해 인증해야 합니다. CLI는 독립적인 인증 캐시에 이어서 데스크톱 앱을 사용하므로 Workbench 데스크톱 앱에 로그인한다고 해서 CLI 환경에서 인증되는 것은 아닙니다. 인증하려면 아래 단계를 수행합니다. 인증 토큰은 일정 시간 동안 로컬 컴퓨터에 캐시되므로 토큰이 만료할 때에만 이 단계를 반복하면 됩니다. 토큰이 만료되거나 인증 오류가 발견된 경우 다음 명령을 실행합니다.

```
# to authenticate 
$ az login

# to list subscriptions
$ az account list -o table

# to set current subscription to a particular subscription ID 
$ az account set -s <subscription_id>

# to verify your current Azure subscription
$ az account show
```

>[!NOTE] 
>프로젝트 폴더 내에서 _az ml_ 명령을 실행하는 경우 프로젝트가 _현재_ Azure 구독의 Azure ML 실험 계정에 속하는지 확인해야 합니다. 그렇지 않으면 실행 오류가 발생할 수 있습니다.


## <a name="running-scripts-and-experiments"></a>스크립트 및 실험 실행
Azure ML Workbench를 사용하면 _az ml experiment submit_ 명령을 사용하여 다양한 컴퓨터 대상에서 Python 및 PySpark 스크립트를 실행할 수 있습니다. 이 명령을 사용하려면 실행 구성 정의가 필요합니다. 

Azure ML Workbench는 계산 대상을 만들 때 해당 .runconfig 파일을 만들지만, _az ml runconfiguration  create_ 명령을 사용하여 추가 실행 구성을 만들 수 있습니다. 실행 구성 파일을 수동으로 편집할 수도 있습니다.

실행 구성은 Workbench 응용 프로그램에서 실험 실행 경험의 일부로 표시됩니다. 

>[!NOTE]
>[실험 실행 구성 참조](experiment-execution-configuration-reference.md) 섹션에서 실행 구성 파일에 대해 더 자세히 알아볼 수 있습니다.

## <a name="running-a-script-locally-on-azure-ml-workbench-installed-runtime"></a>Azure ML Workbench가 설치된 런타임에 대해 로컬로 스크립트 실행
Azure ML Workbench를 사용하면 Azure ML Workbench가 설치된 Python 3.5.2 런타임에 대해 직접 스크립트를 실행할 수 있습니다. 이 기본 런타임은 Azure ML Workbench 설치 시에 설치되며 Azure ML 라이브러리 및 종속성을 포함합니다. 로컬 실행에 대한 실행 결과 및 아티팩트는 여전히 클라우드의 실행 기록 서비스에 저장됩니다.

Docker 기반 실행과 달리 이 구성은 Conda에서 관리되지 _않습니다_. 로컬 Azure ML Workbench Python 환경에 대한 패키지 종속성은 수동으로 프로비전해야 합니다.

다음 명령을 실행하여 Workbench가 설치된 Python 환경에서 로컬로 스크립트를 실행할 수 있습니다. 

```
$az ml experiment submit -c local myscript.py
```

Azure ML Workbench CLI 창에 다음 명령을 입력하여 기본 Python 환경에 대한 경로를 찾을 수 있습니다.
```
$ conda env list
```

>[!NOTE]
>로컬 Spark 환경에 대해 PySpark를 로컬로 직접 실행하는 것은 현재 지원되지 **않습니다**. Azure ML Workbench는 로컬 Docker에서 PySpark 스크립트 실행을 지원합니다. Azure ML 기본 Docker 이미지는 Spark 2.1.11이 미리 설치된 상태에서 제공됩니다. 

_**Python 스크립트에 대한 로컬 실행 개요:**_
![](media/experiment-execution-configuration/local-native-run.png)

## <a name="running-a-script-on-local-docker"></a>로컬 Docker에서 스크립트 실행
또한 Azure ML 실행 서비스를 통해 로컬 컴퓨터의 Docker 컨테이너에서 프로젝트를 실행할 수도 있습니다. Azure ML Workbench는 로컬 Spark 실행을 쉽게 해주기 위해 Azure ML 및 Spark 2.1.11 런타임이 포함된 기본 Docker 이미지를 제공합니다. Docker는 이미 로컬 컴퓨터에서 실행하고 있어야 합니다.

로컬 Docker에서 Python 또는 PySpark 스크립트를 실행하려는 경우 CLI에서 다음 명령을 실행할 수 있습니다.

```
$az ml experiment submit -c docker myscript.py
```
또는
```
az ml experiment submit --run-configuration docker myscript.py
```

로컬 Docker의 실행 환경은 Azure ML 기본 Docker 이미지를 사용하여 준비됩니다. Azure ML Workbench는 처음 실행할 때 이 이미지를 다운로드하고 사용자의 conda_dependencies.yml 파일에 지정된 패키지로 덮어씁니다. 이 작업은 초기 실행을 느리게 만들지만 이후 실행은 Workbench가 캐시된 레이어를 다시 사용하는 덕분에 훨씬 더 빨라집니다. 

>[!IMPORTANT]
>첫 번째 실행에 대해 Docker 이미지를 준비하려면 _az ml experiment prepare -c docker_ 명령을 먼저 실행해야 합니다. 또한 docker.runconfig 파일에서 **PrepareEnvironment** 매개 변수를 True로 설정할 수도 있습니다. 이 작업은 실행 수행의 일부로 환경을 자동으로 준비합니다.  

>[!NOTE]
>Spark에서 PySpark 스크립트를 실행하는 경우, conda_dependencies.yml에 더하여 spark_dependencies.yml도 사용됩니다.

Docker 이미지에서 스크립트를 실행하면 다음과 같은 이점이 있습니다.

1. 다른 실행 환경에서 스크립트를 안정적으로 실행될 수 있도록 보장합니다. Docker 컨테이너에서 실행하면 이식성에 영향을 미칠 수 있는 로컬 참조를 검색하여 방지하는 데 도움이 됩니다. 

2. 이렇게 하면 Apache Spark처럼 설치와 구성이 복잡한 런타임 및 프레임워크에서 코드를 직접 설치할 필요 없이 빨리 테스트할 수 있습니다.


_**Python 스크립트를 위한 로컬 Docker 실행 개요:**_
![](media/experiment-execution-configuration/local-docker-run.png)

## <a name="running-a-script-on-a-remote-docker"></a>원격 Docker에서 스크립트 실행
경우에 따라 사용자의 로컬 컴퓨터에서 사용할 수 있는 리소스가 원하는 모델을 학습하기에 부족할 수 있습니다. 이 경우 Azure ML 실행 서비스를 사용하면 원격 Docker 실행을 사용하여 더 강력한 VM에서 Python 또는 PySpark 스크립트를 실행하는 손쉬운 방법을 선택할 수 있습니다. 

원격 VM은 다음 요구 사항을 충족 해야 합니다.
* 원격 VM이 Linux-Ubuntu를 실행해야 하며 SSH를 통해 액세스할 수 있어야 합니다. 
* 원격 VM이 Docker를 실행하고 있어야 합니다.

>[!IMPORTANT]
> Docker를 실행하는 Windows VM은 원격 계산 대상으로 지원되지 **않습니다**.


다음 명령을 사용하여 원격 Docker 기반 실행을 위한 계산 대상 정의와 실행 구성을 모두 만들 수 있습니다.

```
az ml computetarget attach --name "remotevm" --address "remotevm_IP_address" --username "sshuser" --password "sshpassword" --type remotedocker
```

계산 대상을 구성한 후 다음 명령을 사용하여 스크립트를 실행할 수 있습니다.
```
$ az ml experiment submit -c remotevm myscript.py
```
>[!NOTE]
>실행 환경이 conda_dependencies.yml의 사양을 사용하여 구성된다는 것을 명심하세요. spark_dependencies.yml은 .runconfig 파일에 PySpark 프레임워크를 지정한 경우에도 사용됩니다. 

원격 VM을 위한 Docker 구성 프로세스는 로컬 Docker 실행 프로세스와 정확히 같으므로 유사한 실행 경험을 예상해야 합니다.

>[!TIP]
>처음에 Docker 이미지를 만들어서 발생하는 대기 시간을 피하고 싶으면 스크립트를 실행하기 전에 다음 명령을 사용하여 계산 대상을 준비할 수 있습니다. az ml experiment prepare -c <remotedocker>


_**Python 스크립트를 위한 원격 VM 실행 개요:**_
![](media/experiment-execution-configuration/remote-vm-run.png)


## <a name="running-a-script-on-hdinsight-cluster"></a>HDInsight 클러스터에서 스크립트 실행
HDInsight는 Apache Spark를 지원하는 인기 있는 빅 데이터 분석용 플랫폼입니다. Azure ML Workbench를 사용하면 HDInsight Spark 클러스터를 사용하여 빅 데이터에 대해 실험할 수 있습니다. 

다음 명령을 사용하여 HDInsight Spark 클러스터에 대한 계산 대상 및 실행 구성을 만들 수 있습니다.

```
$ az ml computetarget attach --name "myhdi" --address "<FQDN or IP address>" --username "sshuser" --password "sshpassword" --type cluster 
```

>[!NOTE]
>IP 주소 대신에 FQDN을 사용하고 HDI Spark 클러스터 이름이 _foo_인 경우, SSH 끝점은 _foo-ssh.azurehdinsight.net_이라는 드라이버 노드에 있습니다. _--address_ 매개 변수에 FQDN을 사용하는 경우 서버 이름의 접미사 **-ssh**를 잊지 마십시오.


계산 컨텍스트를 가지고 있는 경우 다음 명령을 실행하여 PySpark 스크립트를 실행할 수 있습니다.

```
$ az ml experiment submit -c myhdi myscript.py
```

Azure ML Workbench는 Conda를 사용하여 HDInsight 클러스터의 실행 환경을 준비 및 관리합니다. 구성은 _conda_dependencies.yml_ 및 _spark_dependencies.yml_ 구성 파일을 통해 관리됩니다. 

사용자는 이 모드에서 실험을 실행하려면 HDInsight 클러스터에 대한 SSH 액세스 권한이 필요합니다. 

>[!NOTE]
>지원되는 구성은 Linux(Python/PySpark 3.5.2 및 Spark 2.1.11 포함 Ubuntu)를 실행하는 HDInsight Spark 클러스터입니다.

_**PySpark 스크립트를 위한 HDInsight 기반 실행 개요**_
![](media/experiment-execution-configuration/hdinsight-run.png)


## <a name="running-a-script-on-gpu"></a>GPU에서 스크립트 실행
GPU에서 스크립트를 실행하려면 이 문서의 가이드: ["Azure Machine Learning에서 GPU를 사용하는 방법"](how-to-use-gpu.md)의 지침을 수행할 수 있음


## <a name="next-steps"></a>다음 단계
* [Azure Machine Learning 만들기 및 설치](quickstart-installation.md)
* [모델 관리](model-management-overview.md)
