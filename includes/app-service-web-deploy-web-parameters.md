Azure 리소스 관리자와 정의한 매개 변수 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때. hello 템플릿은 모든 hello 매개 변수 값이 포함 된 매개 변수 라는 섹션을 포함 합니다.
에 배포 하는 hello 환경에 따라 또는 배포 하는 hello 프로젝트에 따라 달라 집니다는 해당 값에 대 한 매개 변수를 정의 해야 합니다. 항상 유지 되는 값 동일 hello에 대 한 매개 변수를 정의 하지 않습니다. 각 매개 변수 값은 배포 된 hello 템플릿 toodefine hello 리소스에 사용 됩니다. 

매개 변수를 정의할 때 사용 하 여 hello **allowedValues** 필드 toospecify 값이 사용자는 배포 중에 제공할 수 있습니다. 사용 하 여 hello **defaultValue** 필드 tooassign 값 toohello 매개 변수를 배포 하는 동안 제공 된 값이 없는 경우.

Hello 서식 파일의 각 매개 변수에 설명 합니다.

### <a name="sitename"></a>siteName
원하는 toocreate hello 웹 앱의 hello 이름입니다.

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a>hostingPlanName
hello 앱 서비스의 hello 이름 toouse hello 웹 앱을 호스트에 대 한 계획 합니다.

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a>sku
가격 책정 계층 hello 호스팅 계획에 대 한 번호입니다.

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

hello 서식 파일에이 매개 변수를 허용 되는 hello 값을 정의 하 고 값을 지정 하는 경우 기본값 (S1)를 할당 합니다.

### <a name="workersize"></a>workerSize
호스팅 계획 (소형, 중형, 또는 대형) hello의 hello 인스턴스 크기입니다.

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

hello 서식 파일 (0, 1 또는 2)이 매개이 변수에 대해 허용 되는 hello 값을 정의 하 고 값을 지정 하는 경우 기본값 (0)을 할당 합니다. hello 값 toosmall, 중간 규모 및 대규모 해당합니다.

