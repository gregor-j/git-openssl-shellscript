# git-openssl-shellscript
Shellscript to compile git with OpenSSL

There are at times when you need to use git with https instead of ssh (behind firewalls where ssh is not allowed but https is, for instance). There is a gnutls issue that prevents communication with some https behind such firewalls or unusual proxy configurations, etc. You will typically see an error such as this:
```
fatal: unable to access 'http://paul.baker@git.overstock.com/scm/scratch/git-openssl-shellscript.git': gnutls_handshake() failed: Illegal parameter
```
The only way to resolve this is by re-compiling git with `openssl` instead of `gnutls`.

This shellscript does that by downloading the source for git, switching it to `openssl` and and then building it. If you are using a managed version of git (eg: through ubuntu's package manager) you will have to re-run the script every time you recieve an updated version of git because the managed version will overwrite your compiled version.

Compiling and running the tests to ensure functionailty are long. To save time, uncomment
```
#sed -i -- '/TEST\s*=\s*test/d' ./debian/rules
```
so it looks like this
```
sed -i -- '/TEST\s*=\s*test/d' ./debian/rules
```

Related confluence page:
https://confluence.overstock.com/display/~paul.baker/Resolving+git+gnutls_handshake%28%29+failed+error
