1. Hello installer tooa 로컬 폴더 (예를 들어 /tmp) tooprotect hello 서버에 복사 합니다. 종료, hello 다음 명령을 실행 합니다.
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. tooinstall 모바일 서비스 hello 다음 명령을 실행 하는 중:

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. 설치가 완료 되 면 tooget 등록된 toohello 구성 서버 hello 모바일 서비스에 필요 합니다. 구성 서버와 명령 tooregister hello 모바일 서비스를 수행 하는 hello를 실행 합니다.

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a>모바일 서비스 설치 관리자 명령줄

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|매개 변수를 포함해야 합니다.|형식|설명|가능한 값|
|-|-|-|-|
|-r |필수|MS(모바일 서비스) 설치 여부 또는 MT(마스터 대상) 설치 여부를 지정합니다.|MS </br> MT|
|일시 중지되고 |옵션|모바일 서비스를 설치하는 위치|/usr/local/ASR|
|-v|필수|모바일 서비스 설치 가져오기는 hello에 hello 플랫폼 지정 </br> </br>- **VMware**: *VMware vSphere ESXi 호스트*, *Hyper-V 호스트* 및 *물리적 서버*에서 실행되는 VM에 모바일 서비스를 설치하는 경우 이 값을 사용합니다. </br> - **Azure**: Azure IaaS VM에 에이전트를 설치하는 경우 이 값을 사용합니다.| VMware </br> Azure|
|-q|옵션|자동 모드에서 toorun 설치 관리자를 지정합니다.| 해당 없음|


#### <a name="mobility-service-configuration-command-line"></a>모바일 서비스 구성 명령줄

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|매개 변수를 포함해야 합니다.|형식|설명|가능한 값|
|-|-|-|-|
|-i |필수|hello 구성 서버 IP|모든 유효한 IP 주소|
|-P |필수|Hello 연결 암호 저장 되는 전체 파일 경로 hello 파일|모든 유효한 폴더|
