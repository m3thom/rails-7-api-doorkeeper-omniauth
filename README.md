# Steps

### Create application id and secret
```ruby
Doorkeeper::Application.create name: "Web client"
```

Identical to https://github.com/m3thom/rails-app-with-api-engine-devise-door-keeper

up to https://github.com/m3thom/rails-app-with-api-engine-devise-door-keeper#install-doorkeeper section

### Additional setup - Doorkeeper - Assertion Grant Extension

https://github.com/doorkeeper-gem/doorkeeper-grants_assertion

# React client side
```js
  useEffect(() => {
    // use hook after platform dom ready
    GoogleAuth.initialize({
      clientId: "your secret from google console",
      grantOfflineAccess: false,
    });
  }, [])

  const handleSgnInWithGoogle = async () => {
    console.log('init req');
    let googleUser = await GoogleAuth.signIn();
    console.log('googleUser', googleUser);
    const accessToken = googleUser.authentication.accessToken
    const url = "http://localhost:3000/oauth/token"
    const data = {
      client_id: "api client id",
      client_secret: "api client secret",
      grant_type: "assertion",
      provider: "google",
      assertion: accessToken,
    }
    console.log('call api');
    const response = await fetch(url, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(data),
    });
    console.log('api response', response);
  }
```
