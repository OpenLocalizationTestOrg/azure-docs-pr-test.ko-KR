지속적인 개발 인해 Android Studio에서 설치 된 hello Android SDK 버전 hello 버전 hello 코드에서와 다릅니다. 이 자습서에서 참조 되는 Android SDK hello는 hello 작성 시점에 최신 버전, 23 hello입니다. 새 버전의 SDK 표시 hello로 hello 버전 번호가 증가 하 고 사용 가능한 최신 버전 hello를 사용 하는 것이 좋습니다.

버전 불일치의 두 가지 증상은 다음과 같습니다.

- 같은 Gradle 오류 메시지를 작성 하거나 hello 프로젝트를 다시 작성할 때 발생할 수 있습니다 "**toofind 대상 Google Inc.:Google APIs:n 실패**"입니다.
- `import` 문을 기반으로 확인되는 코드의 표준 Android 개체에서 오류 메시지를 생성할 수 있습니다.

이들 중 하나가 표시 되 면 hello 버전의 hello Android Studio에 설치 된 Android SDK 다운로드 hello 프로젝트의 hello SDK 대상을 일치 하지 않습니다. tooverify hello 버전 hello 다음 변경 내용을 확인 하십시오.

1. Android Studio에서 **Tools** > **Android** > **SDK Manager**를 클릭합니다. Hello hello SDK 플랫폼의 최신 버전을 설치 하지 않은 경우 tooinstall 클릭 것입니다. Hello 버전 번호를 기록해 둡니다.
2. Hello에 **프로젝트 탐색기** 탭의 **Gradle 스크립트**개방형 hello 파일 **의 build.gradle (modeule: 응용 프로그램)**합니다. 해당 hello 확인 **compileSdkVersion** 및 **buildToolsVersion** 설치 된 toohello 최신 SDK 버전을 설정 합니다. hello 태그는 다음과 같이 표시 될 수 있습니다.

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. Android Studio 프로젝트 탐색기에서 마우스 오른쪽 단추로 클릭 hello 프로젝트 노드를 hello 선택 **속성**, hello 왼쪽된 열에서 선택 하 고 **Android**합니다. 해당 hello 확인 **프로젝트 빌드 대상** toohello 설정 hello와 같은 SDK 버전 **targetSdkVersion**합니다.

Android Studio에서 hello 매니페스트 파일을 더 이상 사용 되는 toospecify hello 대상 SDK 및 hello 경우 Eclipse와 달리 최소 SDK 버전입니다.
