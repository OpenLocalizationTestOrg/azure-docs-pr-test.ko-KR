## <a name="install-hello-prerequisites"></a>Hello 필수 구성 요소 설치

이 자습서의 단계에서는 hello Ubuntu Linux를 실행 하는 가정 합니다.

셸을 열고 다음 명령을 tooinstall hello에 대 한 필수 구성 요소 패키지가 hello를 실행 합니다.

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

Hello 셸에서 hello 명령 tooclone hello Azure IoT 가장자리 GitHub 리포지토리 tooyour 로컬 컴퓨터에 다음을 실행 합니다.

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a>Toobuild 샘플 hello 하는 방법

이제 빌드할 수 hello IoT 가장자리 런타임 및 샘플 로컬 컴퓨터에서:

1. 셸을 엽니다.

1. Hello의 로컬 복사본에 toohello 루트 폴더를 이동 **iot 가장자리** 저장소입니다.

1. 빌드 스크립트를 다음과 같이 실행합니다.

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

이 스크립트를 사용 하는 **cmake** 폴더 라는 유틸리티 toocreate **빌드** hello 루트 폴더의 로컬 복사본에는 **iot 가장자리** 리포지토리 메이크파일을 생성 합니다. hello 스크립트는 다음 단위 테스트 및 최종 tooend 테스트 건너뛰기 hello 솔루션을 작성 합니다. 원하는 toobuild hello 단위 테스트를 실행 하는 경우 추가 hello `--run-unittests` 매개 변수입니다. 원하는 toobuild hello 끝 tooend 테스트를 실행 하는 경우 추가 hello `--run-e2e-tests`합니다.

> [!NOTE]
> Hello를 실행할 때마다 **build.sh** 스크립트를 삭제 하 고 다음 hello를 다시 만듭니다 **빌드** hello의 로컬 복사본의 hello 루트 폴더에 폴더 **iot 가장자리** 저장소입니다.
