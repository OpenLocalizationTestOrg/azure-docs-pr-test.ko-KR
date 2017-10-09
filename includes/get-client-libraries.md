### <a name="install-via-composer"></a>작성기를 통해 설치
1. [Git를 설치합니다][install-git]. Windows에서는 추가 해야 한다고도 hello Git 실행 tooyour PATH 환경 변수를 참고 합니다. 
2. 라는 파일을 만들어 **composer.json** 에 프로젝트의 루트 hello 및 다음 코드 tooit hello 추가:
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. 프로젝트 루트에 **[composer.phar][composer-phar]**을 다운로드합니다.
4. 명령 프롬프트를 열고 hello 다음 프로젝트 루트에 명령을 실행 합니다.
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
