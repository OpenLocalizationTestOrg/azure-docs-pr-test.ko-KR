## <a name="build-iot-edge"></a>IoT Edge 빌드

이 자습서에서는 미리 구성 된 솔루션 모니터링 원격 hello로 IoT 가장자리 모듈 toocommunicate 사용자 지정을 사용 합니다. 따라서 사용자 지정 소스 코드에서 toobuild hello IoT 가장자리 모듈을 검색 해야합니다. 다음 섹션 hello tooinstall IoT Edge 및 빌드 사용자 지정 IoT 지 모듈 hello 방법을 설명 합니다.

### <a name="install-iot-edge"></a>IoT Edge 설치

hello 다음 단계로 진행 tooinstall hello Intel NUC hello에 대 한 IoT 가장자리 소프트웨어를 미리 컴파일 방식이 됩니다.

1. Hello 나오는 Intel NUC hello에 명령을 실행 하 여 필요한 hello 스마트 패키지 저장소를 구성 합니다.

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    입력 `y` 때 hello 명령은 묻는 너무**이 채널을 포함?**합니다.

1. Hello 다음 명령을 실행 하 여 hello 스마트 패키지 관리자를 업데이트 합니다.

    ```bash
    smart update
    ```

1. Hello 다음 명령을 실행 하 여 hello Azure IoT 가장자리 패키지를 설치 합니다.

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. Hello "Hello world" 예제를 실행 하 여 hello 설치를 확인 합니다. 이 샘플 5 초 마다 hello world 메시지 toohello log.txT 파일을 씁니다. hello 다음 명령이 실행 hello "Hello world" 예제 추가 정보:

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    무시 **잘못 된 인수** hello 예제를 중지 하면 메시지입니다.

    Hello 로그 파일의 명령을 tooview hello 내용을 다음 hello를 사용 합니다.

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a>문제 해결

Hello 오류가 나타나면 "패키지가 util-linux-dev", 제공 Intel NUC hello를 다시 부팅을 시도 합니다.
