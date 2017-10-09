### <a name="install-via-composer"></a><span data-ttu-id="27c37-101">작성기를 통해 설치</span><span class="sxs-lookup"><span data-stu-id="27c37-101">Install via Composer</span></span>
1. <span data-ttu-id="27c37-102">[Git를 설치합니다][install-git].</span><span class="sxs-lookup"><span data-stu-id="27c37-102">[Install Git][install-git].</span></span> <span data-ttu-id="27c37-103">Windows에서는 추가 해야 한다고도 hello Git 실행 tooyour PATH 환경 변수를 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c37-103">Note that on Windows, you must also add hello Git executable tooyour PATH environment variable.</span></span> 
2. <span data-ttu-id="27c37-104">라는 파일을 만들어 **composer.json** 에 프로젝트의 루트 hello 및 다음 코드 tooit hello 추가:</span><span class="sxs-lookup"><span data-stu-id="27c37-104">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="27c37-105">프로젝트 루트에 **[composer.phar][composer-phar]**을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="27c37-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="27c37-106">명령 프롬프트를 열고 hello 다음 프로젝트 루트에 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c37-106">Open a command prompt and execute hello following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
