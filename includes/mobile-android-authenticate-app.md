
1. <span data-ttu-id="236ba-101">Android Studio에서 hello 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-101">Open hello project in Android Studio.</span></span>

2. <span data-ttu-id="236ba-102">**프로젝트 탐색기** Android Studio에서 hello ToDoActivity.java 파일을 열고 hello 다음 import 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-102">In **Project Explorer** in Android Studio, open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="236ba-103">다음 메서드 toohello hello 추가 **ToDoActivity** 클래스:</span><span class="sxs-lookup"><span data-stu-id="236ba-103">Add hello following method toohello **ToDoActivity** class:</span></span>

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    <span data-ttu-id="236ba-104">이 코드에서는 메서드 toohandle hello Google 인증 프로세스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-104">This code creates a method toohandle hello Google authentication process.</span></span> <span data-ttu-id="236ba-105">대화 상자는 hello 인증 된 사용자의 hello ID를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-105">A dialog displays hello ID of hello authenticated user.</span></span> <span data-ttu-id="236ba-106">성공적으로 인증을 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="236ba-107">Google 이외의 id 공급자를 사용 하는 경우 변경 toohello 전달 된 값이 hello **로그인** 의 다음 값에는 hello 메서드 tooone: _MicrosoftAccount_, _Facebook_, _Twitter_, 또는 _windowsazureactivedirectory_합니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-107">If you are using an identity provider other than Google, change hello value passed toohello **login** method tooone of hello following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="236ba-108">Hello에 **onCreate** 메서드를 hello hello를 인스턴스화하는 hello 코드 뒤의 다음 코드 줄을 추가 `MobileServiceClient` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-108">In hello **onCreate** method, add hello following line of code after hello code that instantiates hello `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="236ba-109">이 호출이 hello 인증 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-109">This call starts hello authentication process.</span></span>

5. <span data-ttu-id="236ba-110">이동 후 코드 남은 hello `authenticate();` hello에 **onCreate** 메서드 tooa 새 **createTable** 메서드:</span><span class="sxs-lookup"><span data-stu-id="236ba-110">Move hello remaining code after `authenticate();` in hello **onCreate** method tooa new **createTable** method:</span></span>

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. <span data-ttu-id="236ba-111">tooensure 리디렉션 works 예상 대로 추가의 코드 조각은 다음 hello _RedirectUrlActivity_ too_AndroidManifest.xml_:</span><span class="sxs-lookup"><span data-stu-id="236ba-111">tooensure redirection works as expected, add hello following snippet of _RedirectUrlActivity_ too_AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="236ba-112">Android 응용 프로그램의 redirectUriScheme too_build.gradle_를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-112">Add redirectUriScheme too_build.gradle_ of your Android application.</span></span>

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. <span data-ttu-id="236ba-113">사용자의 build.gradle에 com.android.support:customtabs:23.0.1 toohello 종속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-113">Add com.android.support:customtabs:23.0.1 toohello dependencies in your build.gradle:</span></span>

      <span data-ttu-id="236ba-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span><span class="sxs-lookup"><span data-stu-id="236ba-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="236ba-115">Hello에서 **실행** 메뉴를 클릭 하 여 **응용 프로그램을 실행** toostart hello 응용 프로그램 및 선택한 id 공급자를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-115">From hello **Run** menu, click **Run app** toostart hello app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="236ba-116">hello 언급 URL 체계는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-116">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="236ba-117">확인의 항목을 모두 `{url_scheme_of_you_app}` 사용 하 여 hello 동일한 대/소문자입니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use hello same case.</span></span>

<span data-ttu-id="236ba-118">로그인 했습니다. 오류 없이 실행 되는 hello 앱 및 수 tooquery hello 백 엔드 서비스 하 고 업데이트 toodata 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="236ba-118">When you are successfully signed in, hello app should run without errors, and you should be able tooquery hello back-end service and make updates toodata.</span></span>
