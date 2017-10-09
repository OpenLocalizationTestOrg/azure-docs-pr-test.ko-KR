
호스트 구성 파일 및 hello 다음 예제와 같이 별도 함수에 대 한 hello 코드를 포함 하는 각각 하나 이상의 하위 폴더를 포함 하는 루트 폴더에 거주 하 고 hello에 모든 함수가 지정된 함수 응용 프로그램에 대 한 hello 코드:

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

hello *host.json* 파일 일부 런타임 관련 구성을 포함 하 고 hello 함수 앱의 hello 루트 폴더에 위치 합니다. 사용할 수 있는 설정에 대 한 자세한 내용은 참조 [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) hello WebJobs.Script 리포지토리 wiki에서 합니다.

각 함수는 하나 이상의 코드 파일, hello function.json 구성 및 기타 종속성을 포함 하는 폴더를 있습니다.

