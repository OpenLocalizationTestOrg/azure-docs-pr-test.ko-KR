## <a name="install-hello-prerequisites"></a>Hello 필수 구성 요소 설치

1. [Visual Studio 2015 또는 2017](https://www.visualstudio.com)을 설치합니다. Hello를 사용할 수 있습니다 hello 라이선스 요구 사항을 충족 하는 경우 Community Edition을 해제 합니다. 있는지 tooinclude Visual c + + 및 NuGet 패키지 관리자 여야 합니다.

1. 설치 [git](http://www.git-scm.com) git.exe hello 명령줄에서 실행할 수 있는지 확인 합니다.

1. 설치 [CMake](https://cmake.org/download/) cmake.exe hello 명령줄에서 실행할 수 있는지 확인 합니다. CMake 버전 3.7.2 이상을 사용하는 것이 좋습니다. hello **.msi** 설치 관리자가 windows hello 가장 쉬운 옵션입니다. CMake toohello 추가 hello 설치 관리자의 메시지에 따라 최소한 현재 사용자를 hello에 대 한 경로입니다.

1. [Python 2.7](https://www.python.org/downloads/release/python-27)을 설치합니다. 추가 Python tooyour `PATH` 환경 변수를 **제어판-> 시스템-> 고급 시스템 설정에는 환경 변수->**합니다.

1. 명령 프롬프트에서 명령을 tooclone hello Azure IoT 가장자리 GitHub 리포지토리 tooyour 로컬 컴퓨터를 다음 hello를 실행 합니다.

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a>Toobuild 샘플 hello 하는 방법

이제 빌드할 수 hello IoT 가장자리 런타임 및 샘플 로컬 컴퓨터에서:

1. **VS 2015용 개발자 명령 프롬프트** 또는 **VS 2017용 개발자 명령 프롬프트** 명령 프롬프트를 엽니다.

1. Hello의 로컬 복사본에 toohello 루트 폴더를 이동 **iot 가장자리** 저장소입니다.

1. 빌드 스크립트를 다음과 같이 실행합니다.

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

이 스크립트는 Visual Studio 솔루션 파일을 만듭니다. 고 hello 솔루션을 빌드합니다. Hello에서 hello Visual Studio 솔루션을 찾을 수 있습니다 **빌드** hello의 로컬 복사본에서 폴더 **iot 가장자리** 저장소입니다. 원하는 toobuild hello 단위 테스트를 실행 하는 경우 추가 hello `--run-unittests` 매개 변수입니다. 원하는 toobuild hello 끝 tooend 테스트를 실행 하는 경우 추가 hello `--run-e2e-tests`합니다.

> [!NOTE]
> Hello를 실행할 때마다 **build.cmd** 스크립트를 삭제 하 고 다음 hello를 다시 만듭니다 **빌드** hello의 로컬 복사본의 hello 루트 폴더에 폴더 **iot 가장자리** 저장소입니다.
