Azure는 **다음 조건 모두가 참일 경우**응용 프로그램에서 Python을 사용하도록 결정합니다.

* requirements.txt 파일 hello 루트 폴더
* hello 루트 폴더에 모든.py 파일 또는 runtime.txt python을 지정 하는

않은 hello 경우와 같은 추가 Python 작업 뿐만 아니라 파일, hello 표준 동기화를 수행 하는 Python 특정 배포 스크립트를 사용 합니다.

* 가상 환경 자동 관리
* pip를 사용하여 requirements.txt에 나열된 패키지 설치
* Hello에 따라 hello 적절 한 web.config의 생성 Python 버전을 선택 합니다.
* Django 응용 프로그램에 대한 정적 파일 수집

Toocustomize hello 스크립트 필요 없이 hello 기본 배포 단계의 특정 측면을 제어할 수 있습니다.

모든 Python 특정 배포 단계 tooskip 하려는 경우에이 빈 파일을 만들 수 있습니다.

    \.skipPythonDeployment

배포 보다 자세히 제어는 다음 파일이 hello를 만들어서 hello 기본 배포 스크립트를 재정의할 수 있습니다.

    \.deployment
    \deploy.cmd

Hello를 사용할 수 있습니다 [Azure 명령줄 인터페이스] [ Azure command-line interface] toocreate hello 파일입니다.  프로젝트 폴더에서 다음 명령을 사용합니다.

    azure site deploymentscript --python

이러한 파일이 존재하지 않으면 Azure는 임시 배포 스크립트를 만들고 실행합니다.  것이 동일한 toohello 위의 hello 명령으로 만들 하나 있습니다.

[Azure command-line interface]: http://azure.microsoft.com/downloads/
