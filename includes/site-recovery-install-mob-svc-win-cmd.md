1. Tooprotect hello 서버 hello installer tooa 로컬 폴더 (예: C:\Temp)를 복사 합니다. Hello 명령을 명령 프롬프트에서 관리자 권한으로 다음을 실행 합니다.

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. tooinstall 모바일 서비스 hello 다음 명령을 실행 하는 중:

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. 이제 hello 에이전트 toobe hello 구성 서버에 등록 해야 합니다.

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a>모바일 서비스 설치 관리자 명령줄 인수

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| 매개 변수를 포함해야 합니다.|형식|설명|가능한 값|
|-|-|-|-|
|/Role|필수|MS(모바일 서비스) 설치 여부 또는 MT(마스터 대상) 설치 여부를 지정합니다.|MS </br> MT|
|/InstallLocation|옵션|모바일 서비스를 설치하는 위치|Hello 컴퓨터의 임의 폴더|
|/Platform|필수|모바일 서비스 설치 가져오기는 hello에 hello 플랫폼 지정 </br> </br>- **VMware**: *VMware vSphere ESXi 호스트*, *Hyper-V 호스트* 및 *물리적 서버*에서 실행되는 VM에 모바일 서비스를 설치하는 경우 이 값을 사용합니다. </br> - **Azure**: Azure IaaS VM에 에이전트를 설치하는 경우 이 값을 사용합니다.| VMware </br> Azure|
|/Silent|옵션|자동 모드에서 toorun hello 설치 관리자를 지정합니다.| 해당 없음|

>[!TIP]
> %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log 아래 hello 설치 로그를 볼 수 있습니다.

#### <a name="mobility-service-registration-command-line-arguments"></a>모바일 서비스 등록 명령줄 인수

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | 매개 변수를 포함해야 합니다.|형식|설명|가능한 값|
  |-|-|-|-|
  |/CSEndPoint |필수|Hello 구성 서버 IP 주소| 모든 유효한 IP 주소|
  |/PassphraseFilePath|필수|Hello 암호의 위치 |모든 유효한 UNC 또는 로컬 파일 경로|


>[!TIP]
> hello AgentConfiguration 로그 %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log 아래에서 확인할 수 있음
