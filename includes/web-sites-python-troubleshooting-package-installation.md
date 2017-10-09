일부 패키지는 Azure에서 실행할 때 pip를 사용하여 설치되지 않을 수 있습니다.  단순히 해당 hello 패키지에서 사용할 수 없으면 hello Python 패키지 인덱스 수 있습니다.  컴파일러는 필요한 수 있습니다 (컴파일러는 hello 컴퓨터 실행 중인 hello 웹 응용 프로그램을 Azure 앱 서비스에서 사용할 수 없음).

이 섹션에서는 살펴보게 toodeal 방법으로이 문제에 있습니다.

### <a name="request-wheels"></a>휠 요청
Hello 패키지를 설치 하는 컴파일러를 필요한 경우 바퀴 hello 패키지에 사용할 수 있는 hello 패키지 소유자 toorequest에 게 문의 하십시오.

hello 최근 가용성과 함께 [Python 2.7 용 Microsoft Visual c + + 컴파일러][Microsoft Visual C++ Compiler for Python 2.7], Python 2.7에 대 한 네이티브 코드를 있는 쉽게 toobuild 패키지 됩니다.

### <a name="build-wheels-requires-windows"></a>휠 빌드(Windows 필요)
참고:이 옵션을 사용할 때는 확인 되었는지 toocompile hello 패키지 버전과 일치 하는 hello 플랫폼/아키텍처/Azure 앱 서비스의 hello 웹 응용 프로그램에 사용 되는 Python 환경을 사용 하 여 (Windows/32-bit/2.7 또는 3.4).

Hello 패키지 컴파일러 필요 하기 때문에 설치 하지 않는 경우 hello 컴파일러 로컬 컴퓨터에 설치 하 고 저장소에 포함할 hello 패키지용 휠을 구축할 수 있습니다.

Mac/Linux 사용자: 액세스 tooa Windows 컴퓨터를 설정 하지 않은 경우 참조 [가상 컴퓨터 실행 기간을 만들] [ Create a Virtual Machine Running Windows] 방법에 대 한 Azure에서 VM toocreate 합니다.  Toobuild hello 바퀴 사용 지정, toohello 리포지토리를 추가 및 원한다 면 hello VM을 삭제 합니다. 

Python 2.7 설치 [Python 2.7 용 Microsoft Visual c + + 컴파일러][Microsoft Visual C++ Compiler for Python 2.7]합니다.

Python 3.4 설치 [Microsoft Visual c + + 2010 Express][Microsoft Visual C++ 2010 Express]합니다.

toobuild 바퀴 hello 휠 패키지가 필요 합니다.

    env\scripts\pip install wheel

사용 하 여 `pip wheel` toocompile 종속성:

    env\scripts\pip wheel azure==0.8.4

.Whl 파일을 hello \wheelhouse 폴더에 만들어집니다.  Hello \wheelhouse 폴더 마우스 휠 파일 tooyour 리포지토리를 추가 합니다.

Requirements.txt tooadd hello 편집 `--find-links` hello 위쪽 옵션입니다. 진행 중인 toohello python 패키지 인덱스 하기 전에 hello 로컬 폴더에 정확히 일치에 대 한 pip toolook을 인지 나타냅니다.

    --find-links wheelhouse
    azure==0.8.4

모든 종속성 hello \wheelhouse 폴더와 사용 하지 않으므로 hello python 패키지에서 인덱스 전혀 tooinclude를 원하는 경우 추가 하 여 pip tooignore hello 패키지 인덱스를 강제할 수 있습니다 `--no-index` toohello 맨 프로그램 requirements.txt 합니다.

    --no-index

### <a name="customize-installation"></a>설치 사용자 지정
배포 스크립트 tooinstall hello를 사용 하 여 다른 설치 관리자와 같은 쉽게 hello 가상 환경에서 패키지를 사용자 지정할 수 있습니다\_설치 합니다.  deploy.cmd에서 주석 처리된 예제를 확인합니다.  이러한 패키지 requirements.txt, 설치에서 tooprevent pip에에서 나열 되지 있는지 확인 합니다.

이 toohello 배포 스크립트를 추가 합니다.

    env\scripts\easy_install somepackage

쉽게 수 toouse 수도 있습니다\_tooinstall exe 설치 관리자에서 설치 (일부는 호환, 쉽지 zip\_설치가 지 원하는).  Hello installer tooyour 리포지토리를 추가 하 고 쉽게 호출\_hello 경로 toohello 실행 파일을 전달 하 여 설치 합니다.

이 toohello 배포 스크립트를 추가 합니다.

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a>가상 환경 hello hello 저장소 (Windows 필요)에 포함
참고:이 옵션을 사용할 경우 확인 되었는지 toouse 버전과 일치 하는 hello 플랫폼/아키텍처/Azure 앱 서비스의 hello 웹 응용 프로그램에 사용 되는 가상 환경 (Windows/32-bit/2.7 또는 3.4).

Hello 리포지토리에 hello 가상 환경을 포함 하는 경우 빈 파일을 만들어 Azure에서 가상 환경 관리를 수행 하에서 hello 배포 스크립트를 방지할 수 있습니다.

    .skipPythonDeployment

Hello 가상 환경을 자동으로 관리 하는 경우 hello 기존 가상 환경에서 나머지 파일 tooprevent hello 응용 프로그램을 삭제 하는 것이 좋습니다.

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
