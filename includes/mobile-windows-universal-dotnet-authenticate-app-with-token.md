
1. <span data-ttu-id="caa8c-101">Hello MainPage.xaml.cs 프로젝트 파일에서 hello 다음 추가 **를 사용 하 여** 문:</span><span class="sxs-lookup"><span data-stu-id="caa8c-101">In hello MainPage.xaml.cs project file, add hello following **using** statements:</span></span>
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. <span data-ttu-id="caa8c-102">Hello 대체 **AuthenticateAsync** 메서드 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="caa8c-102">Replace hello **AuthenticateAsync** method with hello following code:</span></span>
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses hello Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use hello PasswordVault toosecurely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try tooget an existing credential from hello vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from hello stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set hello user from hello stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check toodetermine if hello token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with hello identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store hello user credentials.
                    credential = new PasswordCredential(provider.ToString(),
                        user.UserId, user.MobileServiceAuthenticationToken);
                    vault.Add(credential);
   
                    success = true;
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (MobileServiceInvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
   
            return success;
        }
   
    <span data-ttu-id="caa8c-103">이 버전의에서 **AuthenticateAsync**, hello 앱 시도 hello에 저장 된 toouse 자격 **PasswordVault** tooaccess hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="caa8c-103">In this version of **AuthenticateAsync**, hello app tries toouse credentials stored in hello **PasswordVault** tooaccess hello service.</span></span> <span data-ttu-id="caa8c-104">일반 로그인은 저장된 자격 증명이 없는 경우에도 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="caa8c-104">A regular sign-in is also performed when there is no stored credential.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="caa8c-105">캐시 된 토큰은 만료 될 수 있습니다, 그리고 및 토큰 만료 hello 앱 사용 중인 경우에 인증 후 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caa8c-105">A cached token may be expired, and token expiration can also occur after authentication when hello app is in use.</span></span> <span data-ttu-id="caa8c-106">toodetermine 토큰이 만료 되 면 확인 하려면 어떻게 해야 toolearn [만료 된 인증 토큰에 대 한 확인](http://aka.ms/jww5vp)합니다.</span><span class="sxs-lookup"><span data-stu-id="caa8c-106">toolearn how toodetermine if a token is expired, see [Check for expired authentication tokens](http://aka.ms/jww5vp).</span></span> <span data-ttu-id="caa8c-107">솔루션 toohandling 권한 부여 오류 관련된 tooexpiring 토큰 참조를 게시 하는 hello [캐싱 및 Azure 모바일 서비스에서 만료 된 토큰 처리 관리 SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="caa8c-107">For a solution toohandling authorization errors related tooexpiring tokens, see hello post [Caching and handling expired tokens in Azure Mobile Services managed SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span></span> 
   > 
   > 
3. <span data-ttu-id="caa8c-108">Hello 응용 프로그램을 두 번 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="caa8c-108">Restart hello app twice.</span></span>
   
    <span data-ttu-id="caa8c-109">Hello 처음 시작할 때 hello 공급자를 사용 하 여 로그인 필수임 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="caa8c-109">Notice that on hello first start-up, sign-in with hello provider is again required.</span></span> <span data-ttu-id="caa8c-110">그러나 hello 두 번째 다시 시작 시 hello 캐시 된 자격 증명을 사용 하 고 로그인에는 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="caa8c-110">However, on hello second restart hello cached credentials are used and sign-in is bypassed.</span></span> 

