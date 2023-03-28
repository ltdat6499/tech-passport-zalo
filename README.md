# passport-zalo

Passport strategy for authenticating with Facebook using the OAuth 2.0 API.

This module lets you authenticate using Zalo in your Node.js applications. By plugging into Passport, Zalo authentication can be easily and unobtrusively integrated into any application or framework that supports Connect-style middleware Zalo authentication strategy for Passport and Node.js

[![npm](https://camo.githubusercontent.com/fdc6f7d2d8deeec4bfc087aa4145a78fff3d4a9dbd7f6009c0b37f782376253f/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f762f70617373706f72742d66616365626f6f6b2e737667)](https://www.npmjs.com/package/passport-facebook) [![build](https://camo.githubusercontent.com/f25e9041b9ae3fb79630d40ed72ca2a3fdb5c0d24bb97b13f631f30501db1622/68747470733a2f2f696d672e736869656c64732e696f2f7472617669732f6a6172656468616e736f6e2f70617373706f72742d66616365626f6f6b2e737667)](https://travis-ci.org/jaredhanson/passport-facebook) [![coverage](https://camo.githubusercontent.com/23145916ab9bf1afc606887657c4583594ac49d5aaa6b6d9767e53b438e0b6e2/68747470733a2f2f696d672e736869656c64732e696f2f636f766572616c6c732f6a6172656468616e736f6e2f70617373706f72742d66616365626f6f6b2e737667)](https://coveralls.io/github/jaredhanson/passport-facebook) [...](https://github.com/jaredhanson/passport-facebook/wiki/Status)

## Install

```
npm install koa-passport-zalo
```

## Usage

#### Create an Application

Before using `passport-zalo`, you must register an application with Zalo. If you have not already done so, a new application can be created at [Zalo Developers](https://developers.zalo.me/). Your application will be issued an app ID and app secret, which need to be provided to the strategy. You will also need to configure a redirect URI which matches the route in your application.

#### Configure Strategy

The Zalo authentication strategy authenticates users using a Zalo account and OAuth 2.0 tokens. The app ID and secret obtained when creating an application are supplied as options when creating the strategy. The strategy also requires a verify callback, which receives the access token and optional refresh token, as well as profile which contains the authenticated user's Zalo profile. The verify callback must call done providing a user to complete authentication.

```
import passport from "koa-passport";
import { Strategy as ZaloStrategy } from "zalo-passport";

passport.use(
	new ZaloStrategy(
		{
			clientID: "ZALO_CLIENT_ID",
			clientSecret: "ZALO_CLIENT_SECRET",
			callbackURL: "ZALO_CALLBACK_URL",
		},
		async (accessToken, refreshToken, profile, done) => {
			try {
				const member = await Member.findOrCreate())// Find or Create your member by profile
				return done(null, member);
			} catch (error) {
				return done(error, null);
			}
		}
	)
);
```

#### Authenticate Requests

Use passport.authenticate(), specifying the 'zalo' strategy, to authenticate requests. For example, as route middleware in an Koa application:

```
router.get("/zalo", passport.authenticate("zalo"));

router.get("/zalo/callback", async (ctx) =>
	passport.authenticate("zalo", (err, token) => {
		ctx.body = { err, token };
	})(ctx)
);
```

## Examples

[koa-zalo-example](https://github.com/ltdat6499/koa-zalo-example)

Illustrates how to use the Zalo strategy within an Koa application.

## FAQ

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2022 Lý Thành Đạt
