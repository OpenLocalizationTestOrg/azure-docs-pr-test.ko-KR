
<span data-ttu-id="ce677-101">hello 앞의 예제에 살펴보았습니다는 표준 로그인, hello 클라이언트 toocontact 필요한 두 hello id 공급자와 hello 백 엔드 Azure 서비스 hello 앱이 시작 될 때마다.</span><span class="sxs-lookup"><span data-stu-id="ce677-101">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello back-end Azure service every time hello app starts.</span></span> <span data-ttu-id="ce677-102">이 메서드를 비효율적 이며 많은 고객이 시도 toostart 앱 동시에 경우에 사용 관련 문제를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-102">This method is inefficient, and you can have usage-related issues if many customers try toostart your app simultaneously.</span></span> <span data-ttu-id="ce677-103">더 나은 방법은 toocache hello 권한 부여에서 반환 된 토큰 hello Azure 서비스 및 try toouse이는 공급자 기반 로그인에 사용 하기 전에 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-103">A better approach is toocache hello authorization token returned by hello Azure service, and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="ce677-104">Hello 백 엔드 클라이언트 관리 또는 서비스 관리 인증 사용 여부에 관계 없이 Azure 서비스에서 발급 한 hello 토큰을 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-104">You can cache hello token issued by hello back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="ce677-105">이 자습서에서는 서비스 관리 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="ce677-106">Hello ToDoActivity.java 파일을 열고 다음 가져오기 조건 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-106">Open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="ce677-107">다음 멤버 toohello hello 추가 `ToDoActivity` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-107">Add hello following members toohello `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="ce677-108">Hello ToDoActivity.java 파일에서 추가 hello에 대 한 정의 다음 hello `cacheUserToken` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ce677-108">In hello ToDoActivity.java file, add hello following definition for hello `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="ce677-109">이 메서드가 전용으로 표시 하는 기본 설정 파일에 hello 사용자 ID와 토큰을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-109">This method stores hello user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="ce677-110">Hello 장치에서 앱이 다른 앱 액세스 toohello 토큰을 보유 하지 않는 액세스 toohello 캐시를 보호 해야이 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-110">This should protect access toohello cache so that other apps on hello device do not have access toohello token.</span></span> <span data-ttu-id="ce677-111">hello 기본 설정이 hello 앱에 대 한 샌드박스입니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-111">hello preference is sandboxed for hello app.</span></span> <span data-ttu-id="ce677-112">그러나 다른 사람이 액세스 toohello 장치를 다른 수단을 통해 액세스 toohello 토큰 캐시를 얻을 수 있는 가능한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-112">However, if someone gains access toohello device, it is possible that they may gain access toohello token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ce677-113">토큰 액세스 tooyour 데이터는 매우 중요 한 것으로 간주 하 고 사용자 액세스 toohello 장치를 얻을 수 있습니다 hello 토큰 암호화를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-113">You can further protect hello token with encryption, if token access tooyour data is considered highly sensitive and someone may gain access toohello device.</span></span> <span data-ttu-id="ce677-114">그러나 완전히 안전한 솔루션이이 자습서의 hello 범위를 벗어납니다 하며 보안 요구 사항에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-114">A completely secure solution is beyond hello scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="ce677-115">Hello ToDoActivity.java 파일에서 추가 hello에 대 한 정의 다음 hello `loadUserTokenCache` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ce677-115">In hello ToDoActivity.java file, add hello following definition for hello `loadUserTokenCache` method.</span></span>

        private boolean loadUserTokenCache(MobileServiceClient client)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            String userId = prefs.getString(USERIDPREF, null);
            if (userId == null)
                return false;
            String token = prefs.getString(TOKENPREF, null);
            if (token == null)
                return false;

            MobileServiceUser user = new MobileServiceUser(userId);
            user.setAuthenticationToken(token);
            client.setCurrentUser(user);

            return true;
        }
5. <span data-ttu-id="ce677-116">Hello에 *ToDoActivity.java* 파일에서 바꾸기 hello `authenticate` hello 다음 토큰 캐시를 사용 하는 메서드를 사용 하 여 메서드.</span><span class="sxs-lookup"><span data-stu-id="ce677-116">In hello *ToDoActivity.java* file, replace hello `authenticate` method with hello following method, which uses a token cache.</span></span> <span data-ttu-id="ce677-117">Toouse Google 아닌 다른 계정을 사용 하려는 경우 hello 로그인 공급자를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-117">Change hello login provider if you want toouse an account other than Google.</span></span>

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. <span data-ttu-id="ce677-118">올바른 계정을 사용 하 여 hello 앱과 테스트 인증을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="ce677-118">Build hello app and test authentication using a valid account.</span></span> <span data-ttu-id="ce677-119">앱을 두 번 이상 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-119">Run it at least twice.</span></span> <span data-ttu-id="ce677-120">먼저 실행 하 여 hello, 하는 동안에 프롬프트 toosign 수신 해야 하며 hello 토큰 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-120">During hello first run, you should receive a prompt toosign in and create hello token cache.</span></span> <span data-ttu-id="ce677-121">그런 다음 각 실행 인증용 tooload hello 토큰 캐시를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-121">After that, each run attempts tooload hello token cache for authentication.</span></span> <span data-ttu-id="ce677-122">필요한 toosign 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce677-122">You should not be required toosign in.</span></span>
