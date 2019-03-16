How to make the flag "Remember Me" for CodeIgniter 4
====================================================

The Basic App stores user authorization data on a site in a regular framework session. The lifetime of this session is determined globally for the entire application, and cannot be changed for a single session.

The Basic App  stores user authorization data on a site in a regular framework session. The lifetime of this session is determined globally for the entire application, and cannot be changed for a single session. To force the application to forget the user’s authorization if he did not set the Remember Me” flag when authorizing, when closing the browser, you need to set up a session cookie without a lifetime, and then check whether the user is authorized by its presence.

This conforms to the HTTP specification, but unfortunately, it does not always work. For example if Google Chrome has the option "Continue where you left off" or "Continue running background apps when Google Chrome is closed" then session cookies are not deleted. In other browsers there may be similar options in which session cookies are not deleted.

This is a big headache for developers but we wil not argue whether it is good or bad, the fact is that for most users of the site the option "Remember Me" implemented according to the classical scheme will not work as it should if this flag is not installed. This creates a security risk for user data. If user logs in from someone else`s computer and doesn`t specifically set the "Remember Me" flag he wants the one who logs on to this computer after him to be not logged in to this account.

To solve this problem there is no 100% correct universal solution, because the surest solution is to follow the HTTP specification but it does not always works. A simple solution would be to set an extra cookie with a lifetime, but it does not solve the whole security problem, since if you put the lifetime of the secondary cookie too small, then the user may lose authorization if it does not refresh the page for too long, and it does not make sense to set the cookie lifetime longer.

JavaScript will help us. Since we cannot track the closure of the browser by the user, we will have to track its activity on the page, and if it is not there, then delete its authorization data. We will hang a timer on the page that will send a ping command every 10 seconds. When each such command is received, the server will overwrite the user's last access time to the account, and when opening the page, check whether too much time has passed since that moment, for example, more than 30 seconds, and if it has passed, then delete the authorization.

In our opinion, this is not an ideal, but quite acceptable solution. And what do you think about it?