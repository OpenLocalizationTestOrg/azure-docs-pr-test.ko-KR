---
title: "VM 확장을 사용 하 여 Linux VM aaaMonitoring | Microsoft Docs"
description: "Linux 진단 확장 toomonitor hello 성능 및 진단 데이터 Azure에서 Linux VM의 toouse hello 하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a>Hello Linux 진단 확장 toomonitor hello 성능과 Linux VM의 진단 데이터를 사용 하 여

이 문서에서는 버전 2.3 hello Linux 진단 확장을 설명 합니다.

> [!IMPORTANT]
> 이 버전은 사용이 중단되었으며 2018년 6월 30일 이후에 언제든지 게시가 취소될 수 있습니다. 이 버전은 버전 3.0으로 대체되었습니다. 자세한 내용은 참조 hello [hello Linux 진단 확장의 버전 3.0 설명서](../diagnostic-extension.md)합니다.

## <a name="introduction"></a>소개

(**참고**: Linux 진단 확장에서 오픈 소스는 hello [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) hello hello 확장에서 최신 정보를 처음 게시 된 합니다. Toocheck hello 경우가 [GitHub 페이지](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) 첫 번째.)

hello Linux 진단 확장은 사용자 모니터 hello Linux Vm의 경우 Microsoft Azure에서 실행 되는 데 도움이 됩니다. 기능을 수행 하는 hello 다음과 같습니다.

* 수집 하 고 진단 및 syslog 정보를 포함 하는 hello Linux VM toohello 사용자의 저장소 테이블에서 hello 시스템 성능 정보를 업로드 합니다.
* 수집 되어 업로드 하는 사용자가 toocustomize hello 데이터 메트릭을 수 있습니다.
* 사용자가 tooupload 지정 된 로그 파일 tooa 지정 된 저장소 테이블을 수 있습니다.

Hello 현재 버전 2.3에에서 hello 데이터 포함 됩니다.

* 시스템, 보안 및 응용 프로그램 로그를 비롯한 모든 Linux Rsyslog 로그.
* 에 지정 된 모든 시스템 데이터 [hello System Center 플랫폼 크로스 솔루션 사이트](https://scx.codeplex.com/wikipage?title=xplatproviders)합니다.
* 사용자가 지정한 로그 파일.

이 확장 프로그램은 클래식 hello와 리소스 관리자 배포 모델입니다.

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a>현재 버전의 hello 확장 및 이전 버전의 사용 중단

hello hello 확장의 최신 버전은 **2.3**, 및 **(2.0, 2.1 및 2.2)에 있는 이전 버전이 더 이상 사용 되지 되 고 끝날 때 올해 (2017) 게시 되지 않은**합니다. 사용 하지 않도록 설정 하는 자동으로 부 버전 업그레이드를 hello Linux 진단 확장을 설치한 경우 hello 확장을 제거 하 고 사용 하도록 설정 하는 자동으로 부 버전 업그레이드를 다시 설치 것이 좋습니다. 클래식 (ASM) Vm에서이 Azure XPLAT CLI 또는 Powershell을 통해 hello 확장을 설치 하는 경우 '2.*' hello 버전으로 지정 하 여 수행할 수 있습니다. ARM Vm에서이 위해서는 포함 하 여 ' "autoUpgradeMinorVersion": true' hello VM 배포 템플릿에서 합니다. 또한 새 hello 확장이 설치 되어 있는 모든 hello 자동 부 버전 업그레이드 옵션 설정 되어 있어야 합니다.

## <a name="enable-hello-extension"></a>Hello 확장 사용 하도록 설정

Hello를 사용 하 여이 확장을 사용 하도록 설정할 수 있습니다 [Azure 포털](https://portal.azure.com/#), Azure PowerShell 또는 Azure CLI 스크립트입니다.

tooview hello 시스템을 구성 하 고 성능 데이터를 직접 hello Azure 포털에서에서 수행 [hello Azure 블로그에서 이러한 단계](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/)합니다.

이 문서는 방법에 중점을 둡니다 tooenable Azure CLI 명령을 사용 하 여 hello 확장을 구성 하 고 있습니다. 이렇게 하면 tooread hello 데이터 보려면 hello 저장소 테이블에서 직접 있습니다.

Note hello Azure 포털에 대 한 여기에서 설명 하는 hello 구성 메서드 작동 하지 않습니다. tooview hello Azure 포털에서 직접 hello 시스템 및 성능 데이터를 구성 하 고, hello 확장 hello 포털을 통해 사용할 수 있어야 합니다.

## <a name="prerequisites"></a>필수 조건

* **Azure Linux 에이전트 버전 2.0.6 이상**.

  대부분의 Azure VM Linux 갤러리 이미지에는 2.0.6 이후 버전이 포함되어 있습니다. 실행할 수 있습니다 **WAAgent-버전** tooconfirm hello VM에 설치 된 버전입니다. Hello VM 2.0.6 이전 버전을 실행 하는 경우 참고할 수 [GitHub에서 이러한 지침](https://github.com/Azure/WALinuxAgent "지침") tooupdate 것입니다.
* **Azure CLI**. 에 따라 [CLI를 설치 하는 데이 지침은](../../../cli-install-nodejs.md) tooset hello Azure CLI 환경 컴퓨터에 설치 합니다. Hello Azure CLI를 설치한 후 사용할 수 있습니다 **azure** 명령줄 인터페이스 (예: Bash, 터미널, 또는 명령 프롬프트) tooaccess hello Azure CLI 명령의 명령을 합니다. 예:

  * 자세한 도움말 정보는 **azure vm extension set –help** 를 실행합니다.
  * 실행 **azure 로그인** toosign tooAzure에 있습니다.
  * 실행 **azure vm 목록** toolist 모든 hello Azure에 있는 가상 컴퓨터.
* 저장소 계정 toostore hello 데이터입니다. 이전에 만든 저장소 계정 이름 및 액세스 키 tooupload hello 데이터 tooyour 저장 해야 합니다.

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a>Hello Azure CLI 명령을 tooenable hello Linux 진단 확장을 사용 하 여

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a>시나리오 1. Hello 확장 hello 기본 데이터 집합으로 사용 하도록 설정

2.3 이상 버전에서 수집 되는 hello 기본 데이터에 포함 됩니다.

* 모든 Rsyslog 정보(시스템, 보안 및 응용 프로그램 로그 포함)  
* 기본 시스템 데이터의 핵심 집합입니다. 전체 데이터 집합을 hello는 hello에 설명 되어 [System Center 플랫폼 크로스 솔루션 사이트](https://scx.codeplex.com/wikipage?title=xplatproviders)합니다.
  Tooenable 하려는 경우 추가 데이터 시나리오 2와 3 hello 단계로 계속 진행 합니다.

1단계. 콘텐츠는 다음 hello로 PrivateConfig.json 이라는 파일을 만듭니다.

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

2단계. **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**을 실행합니다.

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a>시나리오 2. Hello 성능 모니터 메트릭 사용자 지정

이 섹션에서는 성능 및 진단 데이터 테이블 toocustomize hello 하는 방법을 설명 합니다.

1단계. 시나리오 1에 설명 된 hello 콘텐츠로 PrivateConfig.json 이라는 파일을 만듭니다. 또한 PublicConfig.json이라는 파일도 만듭니다. 원하는 toocollect hello 특정 데이터를 지정 합니다.

지원 되는 모든 공급자 및 변수에 대 한 참조 hello [System Center 플랫폼 크로스 솔루션 사이트](https://scx.codeplex.com/wikipage?title=xplatproviders)합니다. 여러 개의 쿼리를 포함할 수 있으며 더 많은 쿼리 toohello 스크립트를 추가 하 여 여러 테이블에 저장 합니다.

기본적으로 hello Rsyslog 데이터가 항상 수집 됩니다.

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


2단계. **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**을 실행합니다.

### <a name="scenario-3-upload-your-own-log-files"></a>시나리오 3. 고유한 로그 파일 업로드

이 섹션에서는 toocollect 및 업로드 특정 로그 파일을 저장소 계정 tooyour 방법 설명 합니다. Toospecify 모두 hello tooyour 로그 파일과 hello의 경로 이름 hello 저장할 테이블 toostore 로그 해야 합니다. 파일/테이블에서 여러 개의 항목 toohello 스크립트를 추가 하 여 여러 개의 로그 파일을 만들 수 있습니다.

1단계. 시나리오 1에 설명 된 hello 콘텐츠로 PrivateConfig.json 이라는 파일을 만듭니다. 그런 다음 다음 hello로 PublicConfig.json 라는 다른 파일 콘텐츠 만듭니다.

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

2단계. `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`을 실행합니다.

유의 hello 확장 버전 이전 too2.3에서이 설정을 사용 하 여 모든 로그를 기록 너무`/var/log/mysql.err` 너무 중복 될 수도 있습니다`/var/log/syslog` (또는 `/var/log/messages` hello Linux 배포판에 따라)도 있습니다. 원하는 tooavoid 로깅이 복제본의 로깅을 제외할 수 있습니다 `local6` 시설 rsyslog 구성에 로그인 합니다. Hello Linux 배포판에 의존 하지만 Ubuntu 14.04 시스템에서 hello 파일 toomodify이 `/etc/rsyslog.d/50-default.conf` hello 줄을 바꿀 수 있습니다 및 `*.*;auth,authpriv.none -/var/log/syslog` 너무`*.*;auth,authpriv,local6.none -/var/log/syslog`합니다. 2.3 (2.3.9007)의 hello 최신 핫픽스 릴리스에서이 문제는 해결 되므로 hello 확장 버전 2.3 설정한 경우이 문제가 발생 하지 않아야 합니다. 이 VM을 다시 시작 후에 여전히 용어가 들어 문의 hello 최신 핫픽스 버전을 자동으로 설치 되지 않는 문제 해결 하는 데 도움이 하십시오.

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a>시나리오 4. Hello 확장에서 로그 수집을 중지 합니다.

이 섹션에서 수집 toostop hello 확장 기록 하는 방법을 설명 합니다. Hello 모니터링 에이전트 프로세스는 이러한 재구성 된 경우에 계속 작동 하 고 실행 됩니다. 모니터링 에이전트 프로세스를 완전히 toostop hello를 원하는 경우 hello 확장을 사용 하지 않도록 설정 하 여 그렇게 할 수 있습니다. hello 명령 toodisable hello 확장은 `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`합니다.

1단계. 시나리오 1에 설명 된 hello 콘텐츠로 PrivateConfig.json 이라는 파일을 만듭니다. 콘텐츠를 수행 하는 hello로 PublicConfig.json 라는 다른 파일을 만듭니다.

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


2단계. **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**을 실행합니다.

## <a name="review-your-data"></a>데이터 검토

hello 성능 및 진단 데이터는 Azure 저장소 테이블에 저장 됩니다. 검토 [어떻게 toouse Ruby에서 Azure 테이블 저장소](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn tooaccess hello 저장소의에서 데이터를 hello Azure CLI 스크립트를 사용 하 여 테이블 방법입니다.

또한 다음 UI 도구 tooaccess hello 데이터를 사용할 수 있습니다.

1. Visual Studio 서버 탐색기. 저장소 계정 tooyour 이동 합니다. Hello VM 약 5 분 동안 실행 된 후 4 hello 기본 테이블 표시 됩니다: "LinuxCpu", "LinuxDisk", "LinuxMemory" 및 "Linuxsyslog"입니다. Hello 테이블 이름 tooview hello 데이터를 두 번 클릭 합니다.
1. [Azure 저장소 탐색기](https://azurestorageexplorer.codeplex.com/ "Azure 저장소 탐색기")에 지정된 모든 시스템 데이터.

![이미지](./media/diagnostic-extension/no1.png)

FileCfg 또는 perfCfg (시나리오 2와 3 단계에서 설명)으로 설정한 경우에 Visual Studio 서버 탐색기 및 Azure 저장소 탐색기 tooview 기본이 아닌 데이터를 사용할 수 있습니다.

## <a name="known-issues"></a>알려진 문제

* hello Rsyslog 정보 및 사용자 지정 로그 파일 스크립팅을 통해 액세스할 수 있습니다.
