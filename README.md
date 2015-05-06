https://raw.githubusercontent.com/frodo2015/padlock/master/README.md

Testing performance 

dd if=/dev/zero bs=1M count=512 | openssl sha256

Thanks to
    https://romanrm.net/openssl-padlock
    
More about VIA Padlock and OpenSSL
    https://debianforum.de/forum/viewtopic.php?f=26&t=139728
    https://bugzilla.redhat.com/attachment.cgi?id=433962
    
    http://www.logix.cz/michal/devel/padlock/
    http://sys4.de/de/blog/2013/09/21/openssl-performance-eden-padlock/
    http://git.alpinelinux.org/cgit/aports/plain/main/openssl/
    http://openssl.6102.n7.nabble.com/PATCH-Modification-to-VIA-padlock-patch-td44055.html
    https://packages.debian.org/wheezy/openssl

HOWTO:
https://raw.githubusercontent.com/frodo2015/padlock/master/README.md

apt-get install devscripts fakeroot build-essential zlib1g-dev

wget https://romanrm.net/dl/padlock/0001-crypto-hmac-support-EVP_MD_CTX_FLAG_ONESHOT-and-set-.patch \
     https://romanrm.net/dl/padlock/0002-engines-e_padlock-backport-cvs-head-changes.patch \
     https://romanrm.net/dl/padlock/0003-engines-e_padlock-implement-sha1-sha224-sha256-accel.patch \
     https://romanrm.net/dl/padlock/0004-crypto-engine-autoload-padlock-dynamic-engine.patch \
     https://romanrm.net/dl/padlock/0005-auto-engine.diff

dget http://security.debian.org/debian-security/pool/updates/main/o/openssl/openssl_1.0.1e-2+deb7u16.dsc
# Check https://packages.debian.org/wheezy/openssl for last revision

dpkg-source -x *.dsc

cd openssl*/
patch -p1 < ../0001*; patch -p1 < ../0002*; patch -p1 < ../0003*; patch -p1 < ../0004*; patch -p1 < ../0005*

dpkg-source --commit
# You will be asked for a filename (enter "padlock") and launch a text editor, just press Ctrl-X(nano) or enter :x(vim) to exit

dpkg-buildpackage -rfakeroot -b
# If needed install additional development packages. Try again

cd ..
dpkg -i openssl*.deb libssl1.0.0*.deb
aptitude hold openssl libssl1.0.0

