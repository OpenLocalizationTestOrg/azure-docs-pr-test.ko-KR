---
title: "로그 분석 aaaConnect Windows 컴퓨터 tooAzure | Microsoft Docs"
description: "이 문서는 hello Microsoft Monitoring Agent (MMA)의 사용자 지정된 된 버전을 사용 하 여 온-프레미스 인프라 toohello 로그 분석 서비스의에서 hello 단계 tooconnect hello Windows 컴퓨터를 표시 합니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a>Azure에서 Windows 컴퓨터 toohello 로그 분석 서비스 연결

이 문서에서는 hello 단계 tooconnect Windows 컴퓨터 온-프레미스 인프라 tooOMS 작업 영역에서 사용자 지정된 된 버전의 Microsoft Monitoring Agent (MMA) hello 사용 하 여 합니다. Tooinstall 필요 하 고 모든 toosend 데이터 toohello 로그 분석 서비스와 tooview 및 해당 데이터에서 작동 되도록 하려면에서 tooonboard hello 컴퓨터에 대 한 에이전트를 연결 합니다. 각 에이전트 toomultiple 작업 영역을 보고할 수 있습니다.

Azure 자동화에서 설정, 명령줄 또는 DSC(필요한 상태 구성)를 사용하여 에이전트를 설치할 수 있습니다.  

>[!NOTE]
Azure에서 실행 중인 가상 컴퓨터에 대 한 hello를 사용 하 여 설치를 단순화할 수 [가상 컴퓨터 확장](log-analytics-azure-vm-extension.md)합니다.

인터넷에 연결 된 컴퓨터에서 hello 에이전트 hello 연결 toohello 인터넷 toosend 데이터 tooOMS를 사용합니다. 인터넷에 연결 되지 않은 컴퓨터를 사용할 수 있습니다는 프록시 또는 hello [OMS 게이트웨이](log-analytics-oms-gateway.md)합니다.

Windows 컴퓨터 tooOMS 연결 하는 것은 세 가지 간단한 단계를 사용 하 여 간단 합니다.

1. Hello OMS 포털에서 hello 에이전트 설치 파일 다운로드
2. 선택한 hello 메서드를 사용 하 여 hello 에이전트를 설치 합니다.
3. Hello 에이전트를 구성 하거나 필요한 경우 추가 작업 영역을 추가 합니다.

hello 다음 다이어그램에서는 Windows 컴퓨터와 OMS 간의 hello 관계를 설치 하 고 에이전트를 구성한 후

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

IT 보안 정책을 네트워크 tooconnect toohello 인터넷에서 컴퓨터를 허용 하지 않으므로, 컴퓨터 tooconnect toohello OMS 게이트웨이 구성할 수 있습니다. 자세한 내용 및 단계 tooconfigure OMS 게이트웨이 toohello OMS 서비스를 통해 서버 toocommunicate 프로그램 참조에 대 한 [hello OMS 게이트웨이 사용 하 여 컴퓨터 tooOMS 연결](log-analytics-oms-gateway.md)합니다.

## <a name="system-requirements-and-required-configuration"></a>시스템 요구 사항 및 필수 구성
설치 하거나 에이전트를 배포 하기 전에 hello 요구 사항을 충족 하는 tooensure 검토 hello 다음에 자세히 설명 합니다.

- Windows 7 SP1 또는 Windows Server 2008 SP 1 이후 버전을 실행 하는 컴퓨터에 OMS MMA hello를만 설치할 수 이상입니다.
- Azure 구독이 필요합니다.  자세한 내용은 [Log Analytics 시작](log-analytics-get-started.md)을 참조하세요.
- 각 Windows 컴퓨터 수 tooconnect toohello 인터넷 있어야 합니다. HTTPS 또는 toohello OMS 게이트웨이 사용 하 여 합니다. 이 연결은 직접 hello OMS 게이트웨이 또는 프록시를 통해 가능 합니다.
- OMS MMA hello 독립 실행형 컴퓨터, 서버 및 가상 컴퓨터에 설치할 수 있습니다. 가상 컴퓨터 호스 티 드 Azure tooOMS tooconnect 참조 [연결 Azure 가상 컴퓨터 tooLog 분석](log-analytics-azure-vm-extension.md)합니다.
- hello 에이전트는 다양 한 리소스에 대 한 toouse TCP 포트 443을 필요합니다.

### <a name="network"></a>네트워크

Windows 에이전트 tooconnect tooand 레지스터 hello OMS 서비스에 대 한 hello 포트 번호 및 도메인 Url을 포함 하 여 toonetwork 리소스에 액세스 가져야 합니다.

- 프록시 서버에 대 한 적절 한 프록시 서버를 에이전트 설정에 구성 된 리소스가 hello tooensure를 해야 합니다.
- 인터넷 액세스 toohello 제한 하는 방화벽, 또는 네트워킹 엔지니어 필요 tooconfigure 사용자 방화벽 toopermit 액세스 tooOMS 합니다. 에이전트 설정에서 아무 작업도 필요하지 않습니다.

다음 표에서 hello 통신에 필요한 리소스를 보여 줍니다.

>[!NOTE]
>Hello 다음 리소스 중 일부 언급 Operational Insights 로그 분석에 대 한 이전 이름 되었습니다.

| 에이전트 리소스 | 포트 | HTTPS 검사 무시 |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | 예 |
| *.oms.opinsights.azure.com | 443 | 예 |
| *.blob.core.windows.net | 443 | 예 |
| *.azure-automation.net | 443 | 예 |



## <a name="download-hello-agent-setup-file-from-oms"></a>OMS에서 hello 에이전트 설치 파일 다운로드
1. Hello에 hello OMS 포털에서 **개요** 페이지에서 hello **설정** 바둑판식으로 배열입니다.  Hello 클릭 **연결 된 원본** hello 위쪽 탭 합니다.  
    ![연결된 원본 탭](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)
2. 클릭 **Windows 서버** 클릭 하 고 **Windows 에이전트 다운로드** 적용 가능한 tooyour 컴퓨터 프로세서 종류 toodownload hello 설치 파일입니다.
3. Hello의 오른쪽에 **작업 영역 ID**hello 복사 아이콘을 클릭 하 고 hello ID를 메모장에 붙여넣습니다.
4. Hello의 오른쪽에 **기본 키**hello 복사 아이콘을 클릭 하 고 hello 키를 메모장에 붙여넣습니다.     

## <a name="install-hello-agent-using-setup"></a>설치 프로그램을 사용 하 여 hello 에이전트 설치
1. Toomanage 지정 하는 컴퓨터에서 설치 프로그램 tooinstall hello 에이전트를 실행 합니다.
2. Hello 시작 페이지에서 클릭 **다음**합니다.
3. Hello 사용 조건 페이지 hello 라이선스 읽고 클릭 **동의**합니다.
4. Hello 대상 폴더 페이지에서 변경 또는 hello 기본 설치 폴더를 유지 하 고 클릭 **다음**합니다.
5. Hello 에이전트 설치 옵션 페이지에서 tooconnect hello 에이전트 tooAzure 로그 분석 (OMS) Operations Manager를 선택할 수 있습니다 하거나 있습니다 비워 둘 수 hello 선택 나중 tooconfigure hello 에이전트 사용 하려는 경우. **다음**을 누릅니다.   
    - Tooconnect tooAzure 로그 분석 (OMS)을 선택한 경우 붙여 hello **작업 영역 ID** 및 **작업 영역 키 (기본 키)** hello 이전 절차에서 메모장에 복사 하 고 클릭  **다음**합니다.  
        ![작업 영역 ID 및 기본 키 붙여넣기](./media/log-analytics-windows-agents/connect-workspace.png)
    - Tooconnect tooOperations 관리자를 선택한 경우 입력 hello **관리 그룹 이름**, **관리 서버** 이름 및 **관리 서버 포트**, 클릭하고**다음**합니다. Hello 에이전트 작업 계정 페이지에서 hello 로컬 시스템 계정 또는 로컬 도메인 계정을 선택 하 고 클릭 **다음**합니다.  
        ![관리 그룹 구성](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![에이전트 작업 계정](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)

6. Hello 준비 tooInstall 페이지에서 선택 사항을 확인 한 다음 클릭 **설치**합니다.
7. 페이지에 구성이 성공적으로 완료 하는 hello **마침**합니다.
8. 완료 되 면 hello **Microsoft Monitoring Agent** 에 표시 **제어판**합니다. 구성에 검토 하 고 hello 에이전트에 연결 된 tooOperational Insights (OMS)은 확인 수 있습니다. 연결 된 tooOMS hello 에이전트 라는 메시지 표시: **hello Microsoft Monitoring Agent toohello Microsoft Operations Management Suite 서비스를 성공적으로 연결 합니다.**

## <a name="configure-proxy-settings"></a>프록시 설정 구성

Microsoft Monitoring Agent 제어판을 사용 하 여 hello에 대 한 프로시저 tooconfigure 프록시 설정을 다음 hello를 사용할 수 있습니다. 각 서버 toouse이이 프로시저가 필요합니다. Tooconfigure 해야 하는 많은 서버를 설정한 경우 알게 될 것 보다 쉽게 toouse 스크립트 tooautomate이이 프로세스입니다. 이 경우 hello 다음 절차를 참조 하십시오. [hello 스크립트를 사용 하 여 Microsoft 모니터링 에이전트에 대 한 프록시 설정을 tooconfigure](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script)합니다.

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a>Microsoft Monitoring Agent 제어판을 사용 하 여 hello에 대 한 프록시 설정을 tooconfigure
1. **제어판**을 엽니다.
2. **Microsoft Monitoring Agent**를 엽니다.
3. Hello 클릭 **프록시 설정을** 탭 합니다.  
    ![프록시 설정 탭](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)
4. 선택 **프록시 서버를 사용 하 여** hello URL을 입력 하 고 필요한 마찬가지로 toohello 표시 된 예의 경우 포트 번호를 합니다. 프록시 서버에 인증이 필요한 경우 hello 사용자 이름 및 암호 tooaccess hello 프록시 서버를 입력 합니다.


### <a name="verify-agent-connectivity-toooms"></a>에이전트 연결 tooOMS 확인

에이전트 절차를 수행 하는 hello를 사용 하 여 OMS와 통신 하 고 있는지 여부를 쉽게 확인할 수 있습니다.

1.  Windows 에이전트 hello와 hello 컴퓨터에서 제어판을 엽니다.
2.  Microsoft Monitoring Agent를 엽니다.
3.  Hello Azure 로그 분석 (OMS) 탭을 클릭 합니다.
4.  Hello 상태 열에 해당 hello 에이전트 연결 toohello Operations Management Suite 서비스 성공적으로 표시 됩니다.

![연결된 에이전트](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a>Microsoft Monitoring Agent는 스크립트를 사용 하 여 hello에 대 한 프록시 설정을 tooconfigure
다음 샘플, 특정 tooyour 환경 정보로 업데이트 하 고, PS1 파일 이름 확장명으로 저장 및 toohello OMS 서비스에 직접 연결 하는 각 컴퓨터에이 hello 스크립트를 실행 하는 hello를 복사 합니다.

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a>Hello 명령줄을 사용 하는 hello 에이전트 설치
- 수정 하 고 다음 명령줄 hello를 사용 하 여 예제 tooinstall hello 에이전트 hello를 사용 합니다. hello 예제는 완전 자동 설치를 수행합니다.

    >[!NOTE]
    에이전트 tooupgrade 원하는 해야 toouse hello 로그 분석 API를 스크립팅 합니다. Hello 다음 섹션 tooupgrade 에이전트를 참조 하십시오.

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

hello 에이전트도의 자동 압축 풀기 IExpress를 사용 하 여 hello를 사용 하 여 `/c` 명령입니다. Hello 명령줄 스위치에서 볼 수 있습니다 [IExpress에 대 한 명령줄 스위치](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) 다음 업데이트 hello 예제 toosuit 필요 하 고 있습니다.

|MMA 관련 옵션                   |참고 사항         |
|---------------------------------------|--------------|
|ADD_OPINSIGHTS_WORKSPACE               | 1 = 구성 hello 에이전트 tooreport tooa 작업 영역                |
|OPINSIGHTS_WORKSPACE_ID                | 작업 영역 tooadd hello에 대 한 작업 영역 Id (guid)                    |
|OPINSIGHTS_WORKSPACE_KEY               | 작업 영역 키 사용 되는 tooinitially hello 작업 영역을 사용 하 여 인증 |
|OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE  | 작업 영역 hello 위치한 hello 클라우드 환경 지정 <br> 0 = Azure 상용 클라우드(기본값) <br> 1 = Azure Government |
|OPINSIGHTS_PROXY_URL               | 프록시 toouse hello에 대 한 URI |
|OPINSIGHTS_PROXY_USERNAME               | 사용자 이름 tooaccess 인증 된 프록시 |
|OPINSIGHTS_PROXY_PASSWORD               | 암호 tooaccess 인증 된 프록시 |

>[!NOTE]
IExpress의 tooavoid 적중 hello 명령줄 길이 제한을 구성 하는 작업 영역이 없는 hello 에이전트를 설치 하 고 hello 작업 영역에 대 한 스크립트 tooset 구성을 사용 합니다.

>[!NOTE]
발생 하는 경우는 `Command line option syntax error.` hello를 사용 하는 경우 `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` 매개 변수를 hello 해결 방법은 다음을 사용할 수 있습니다.
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a>스크립트를 사용하여 작업 영역 추가
다음 예제는 hello로 hello 로그 분석 에이전트 스크립팅 API를 사용 하 여 작업 영역을 추가 합니다.

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

tooadd 미국 정부, 사용 하 여 hello 다음 스크립트 샘플에 대 한 Azure에서 작업 영역:
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
Hello 명령줄 사용한 또는 tooinstall 스크립트 이전에 hello 에이전트를 구성 하거나 경우 `EnableAzureOperationalInsights` 로 바뀌었습니다. `AddCloudWorkspace`합니다.

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a>Azure 자동화에 DSC를 사용 하 여 hello 에이전트 설치

다음 스크립트 예제 tooinstall hello 에이전트 Azure 자동화에 DSC를 사용 하 여 hello를 사용할 수 있습니다. hello 예제 설치 hello hello로 식별 되는 64 비트 에이전트 `URI` 값입니다. Hello URI 값을 대체 하 여 hello 32 비트 버전을 사용할 수도 있습니다. 두 버전 모두에 대 한 Uri hello가 됩니다.

- Windows 64비트 에이전트 - https://go.microsoft.com/fwlink/?LinkId=828603
- Windows 32비트 에이전트 - https://go.microsoft.com/fwlink/?LinkId=828604


>[!NOTE]
이 절차 및 스크립트 예제는 기존 에이전트를 업그레이드하지 않습니다.

1. Hello xPSDesiredStateConfiguration DSC 모듈을 가져올에서 [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) Azure 자동화로 합니다.  
2.  *OPSINSIGHTS_WS_ID* 및 *OPSINSIGHTS_WS_KEY*의 Azure Automation 변수 자산을 만듭니다. 설정 *OPSINSIGHTS_WS_ID* tooyour OMS 로그 분석 작업 영역 ID 설정 및 *OPSINSIGHTS_WS_KEY* toohello 작업 영역의 기본 키입니다.
3.  다음 스크립트를 MMAgent.ps1로 저장 hello를 사용 하 여
4.  수정 하 고 다음 Azure 자동화에 DSC를 사용 하 여 예제 tooinstall hello 에이전트 hello를 사용 합니다. Hello Azure 자동화 인터페이스 또는 cmdlet을 사용 하 여 Azure 자동화로 MMAgent.ps1를 가져옵니다.
5.  노드 toohello 구성을 할당 합니다. 15 분 이내 hello 노드 구성을 확인 하 고 hello MMA toohello 노드 푸시됩니다.

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a>Hello 최신 ProductId 값 가져오기

hello `ProductId value` hello MMAgent.ps1 스크립트는 고유 tooeach 에이전트 버전입니다. 각 에이전트의 업데이트 된 버전이 게시 되 면 hello ProductId 값을 변경 합니다. 따라서 hello ProductId hello 나중에 변경 되 면 간단한 스크립트를 사용 하 여 hello 에이전트 버전을 찾을 수 있습니다. 테스트 서버에 설치 된 hello 최신 에이전트 버전을 설정한 후 다음 스크립트 tooget 설치 hello ProductId 값 hello를 사용할 수 있습니다. Hello 최신 ProductId 값을 사용 하 여 hello MMAgent.ps1 스크립트의에서 hello 값을 업데이트할 수 있습니다.

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a>에이전트를 수동으로 구성하거나 추가 작업 영역 추가
에이전트를 설치 했으면 했지만 구성 하지 않은 경우 또는 hello 에이전트 tooreport toomultiple 작업 영역을 정보 tooenable 에이전트 다음 hello를 사용 하 여 또는 다시 구성할 수 있습니다. Hello 에이전트를 구성 하 고 나면 hello 에이전트 서비스로 등록 하 고 필요한 구성 정보를 가져오고 솔루션 정보를 포함 하는 관리 팩.

1. Hello Microsoft Monitoring Agent를 설치한 후에 열 **제어판**합니다.
2. 열기 **Microsoft Monitoring Agent** hello를 클릭 한 다음 **Azure 로그 분석 (OMS)** 탭 합니다.   
3. 클릭 **추가** tooopen hello **로그 분석 작업 영역 추가** 상자입니다.
4. 붙여넣기 hello **작업 영역 ID** 및 **작업 영역 키 (기본 키)** tooadd 원하고 클릭 hello 작업 영역에 대 한 이전 절차에서 메모장에 복사한 **확인**.  
    ![Operational Insights 구성](./media/log-analytics-windows-agents/add-workspace.png)

Hello 에이전트에서 모니터링 하는 컴퓨터에서 데이터를 수집 하는 hello OMS에서 모니터링 하는 컴퓨터 수가 hello에 hello OMS 포털에 표시 됩니다 **연결 된 원본** 탭에서 **설정** 으로  **연결 된 서버**합니다.


## <a name="toodisable-an-agent"></a>toodisable 에이전트
1. Hello 에이전트를 설치한 후 열려면 **제어판**합니다.
2. Microsoft Monitoring Agent를 열고 클릭 다음 hello **Azure 로그 분석 (OMS)** 탭 합니다.
3. 작업 영역을 선택하고 **제거**를 클릭합니다. 다른 모든 작업 영역에 대해 이 단계를 반복합니다.


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a>필요에 따라 에이전트 tooreport tooan Operations Manager 관리 그룹 구성

IT 인프라에서 Operations Manager를 사용 하는 경우 Operations Manager 에이전트도 hello MMA 에이전트를 사용할 수도 있습니다.

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a>tooconfigure MMA 에이전트 tooreport tooan Operations Manager 관리 그룹
1.  Hello hello 에이전트가 설치 된 컴퓨터에서 엽니다 **제어판**합니다.  
2.  열기 **Microsoft Monitoring Agent** hello를 클릭 한 다음 **Operations Manager** 탭 합니다.  
    ![Microsoft Monitoring Agent Operations Manager 탭](./media/log-analytics-windows-agents/om-mg01.png)
3.  Operations Manager 서버가 Active Directory와 통합된 경우 **AD DS에서 관리 그룹 할당 자동 업데이트**를 클릭합니다.
4.  클릭 **추가** tooopen hello **관리 그룹 추가** 대화 상자.  
    ![Microsoft Monitoring Agent 관리 그룹 추가](./media/log-analytics-windows-agents/oms-mma-om02.png)
5.  **관리 그룹 이름** 상자 관리 그룹의 hello 이름을 입력 합니다.
6.  Hello에 **기본 관리 서버** 상자 hello hello 기본 관리 서버의 컴퓨터 이름을 입력 합니다.
7.  Hello에 **관리 서버 포트** 상자의 형식 hello TCP 포트 번호입니다.
8.  아래 **에이전트 작업 계정**, hello 로컬 시스템 계정 또는 로컬 도메인 계정을 선택 합니다.
9.  클릭 **확인** tooclose hello **관리 그룹 추가** 대화 상자를 클릭 한 다음 **확인** tooclose hello **Microsoft Monitoring Agent 속성**대화 상자.


## <a name="next-steps"></a>다음 단계

- [로그 분석 솔루션 hello 솔루션 갤러리에서에서 추가](log-analytics-add-solutions.md) tooadd 기능 및 수집 데이터입니다.
