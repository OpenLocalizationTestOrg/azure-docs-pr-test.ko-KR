Azure 리소스 관리자와 정의한 매개 변수 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때. hello 템플릿은 모든 hello 매개 변수 값이 포함 된 매개 변수 라는 섹션을 포함 합니다.
에 배포 하는 hello 환경에 따라 또는 배포 하는 hello 프로젝트에 따라 달라 집니다는 해당 값에 대 한 매개 변수를 정의 해야 합니다. 항상 유지 되는 값 동일 hello에 대 한 매개 변수를 정의 하지 않습니다. 각 매개 변수 값은 리소스를 배포 하는 hello 템플릿 toodefine hello에 사용 됩니다. 

매개 변수를 정의할 때 사용 하 여 hello **allowedValues** 필드 toospecify 값이 사용자는 배포 중에 제공할 수 있습니다. 사용 하 여 hello **defaultValue** 필드 tooassign 값 toohello 매개 변수를 배포 하는 동안 제공 된 값이 없는 경우.

Hello 서식 파일의 각 매개 변수에 설명 합니다.

### <a name="logicappname"></a>logicAppName
hello 논리 앱 toocreate의 hello 이름입니다.

    "logicAppName": {
        "type": "string"
    }