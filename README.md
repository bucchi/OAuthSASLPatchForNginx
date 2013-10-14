OAuthSASLPatchForNginx
======================

Nginx patch to support OAuth SASL mechanism


[SASL XOAUTH2]

In this mechanism, OAuth Token should be base64 encoding of the following format string;
<pre><code>user=someuser@example.com^Aauth=Bearer vF9dft4qmTc2Nvb3RlckBhdHRhdmlzdGEuY29tCg==^A^A
</pre></code>

(*)^A represents a Control+A (\001) here.<br />
<br />
<br />

The base64 encoded value is sent to server with Authenticate command and XOAUTH2 parameter of IMAP like this;
<pre><code>AUTHENTICATE XOAUTH2 dXNlcj1zb21ldXNlckBleGFtcGxlLmNvbQFhdXRoPUJlYXJlciB2RjlkZnQ0cW1UYzJOdmIzUmxja0JoZEhSaGRtbHpkR0V1WTI5dENnPT0BAQo=
</pre></code>

Full protcol flow example of IMAP is the following; 
<pre><code>
[connection begins]
C: C01 CAPABILITY
S: * CAPABILITY IMAP4rev1 UNSELECT IDLE NAMESPACE QUOTA XLIST CHILDREN XYZZY SASL-IR AUTH=XOAUTH2
S: C01 OK Completed
C: A01 AUTHENTICATE XOAUTH2 dXNlcj1zb21ldXNlckBleGFtcGxlLmNvbQFhdXRoPUJlYXJlciB2RjlkZnQ0cW1UYzJOdmIzUmxja0JoZEhSaGRtbHpkR0V1WTI5dENnPT0BAQo=
S: A01 OK Success
[connection continues...]
</code></pre>
<br />
<br />

When nginx recieve AUTHENTICATE command, HTTP headers below are used by nginx to communicate with the authentication server.
<pre><code>Auth-Method: oauth
Auth-User: someuser@example.com
Auth-Pass: dXNlcj1zb21ldXNlckBleGFtcGxlLmNvbQFhdXRoPUJlYXJlciB2RjlkZnQ0cW1UYzJOdmIzUmxja0JoZEhSaGRtbHpkR0V1WTI5dENnPT0BAQo=
Auth-Protocol: imap
</code></pre>

Detais about other headers are documented [here](http://nginx.org/en/docs/mail/ngx_mail_auth_http_module.html#protocol).


[SASL OAUTHBEARER]

TBD


[SASL OAUTH10A]

TBD

