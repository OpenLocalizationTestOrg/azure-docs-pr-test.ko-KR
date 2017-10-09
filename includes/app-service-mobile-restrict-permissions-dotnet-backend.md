
기본적으로 Mobile Apps 백 엔드의 API는 익명으로 호출할 수 있습니다. 다음으로, toorestrict 액세스 인증 tooonly 클라이언트 해야 합니다.  

* **Node.js 다시 (Azure 포털 hello)를 통해 종료** :  

    Mobile Apps 설정에서 **간편한 테이블**을 클릭하고 테이블을 선택합니다. **사용 권한 변경**을 클릭하고 모든 사용 권한에 대해 **인증된 액세스만**을 선택한 다음 **저장**을 클릭합니다.
* **.NET 백 엔드(C#)**:  

    Hello 서버 프로젝트에서 이동 너무**컨트롤러** > **TodoItemController.cs**합니다. Hello 추가 `[Authorize]` toohello 특성 **TodoItemController** 클래스를 다음과 같이 합니다. toorestrict 액세스만 toospecific 메서드 hello 클래스 대신이 특성 정당한 toothose 메서드를 적용할 수도 있습니다. Hello 서버 프로젝트를 다시 게시 합니다.

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* **(Node.js 코드를 통해) Node.js 백 엔드** :  

    테이블 액세스를 위한 toorequire 인증 hello 다음 줄 toohello Node.js 서버 스크립트를 추가 합니다.

        table.access = 'authenticated';

    자세한 내용은 참조 하십시오. [하는 방법: 액세스 tootables에 인증 필요](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth)합니다. 사이트에서 toodownload hello 퀵 스타트 코드 프로젝트를 확인 하려면 어떻게 toolearn [하는 방법: Git를 사용 하 여 다운로드 hello Node.js 백 엔드 퀵 스타트 코드 프로젝트](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)합니다.
