OAuthSASLPatchForNginx
======================

Nginx patch to support OAuth SASL mechanism


[SASL XOAUTH2]
In this mechanism, OAuth Token should be base64 encoding of the following format string;
<pre><code>user=someuser@example.com^Aauth=Bearer vF9dft4qmTc2Nvb3RlckBhdHRhdmlzdGEuY29tCg==^A^A
</pre></code>

Authenticate command is sent to server like this;
<pre><code>AUTHENTICATE XOAUTH2 dXNlcj1zb21ldXNlckBleGFtcGxlLmNvb
QFhdXRoPUJlYXJlciB2RjlkZnQ0cW1UYzJOdmIzUmxja0JoZEhSaGRtbHpkR0
V1WTI5dENnPT0BAQo=
</pre></code>
