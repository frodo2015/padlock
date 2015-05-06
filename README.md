# padlock

apt-get install devscripts fakeroot build-essential zlib1g-dev

wget https://github.com/frodo2015/padlock/blob/master/0001-crypto-hmac-support-EVP_MD_CTX_FLAG_ONESHOT-and-set-.patch \

wget https://github.com/frodo2015/padlock/blob/master/0002-engines-e_padlock-backport-cvs-head-changes.patch

wget https://github.com/frodo2015/padlock/blob/master/0003-engines-e_padlock-implement-sha1-sha224-sha256-accel.patch 

wget https://github.com/frodo2015/padlock/blob/master/0004-crypto-engine-autoload-padlock-dynamic-engine.patch

wget https://github.com/frodo2015/padlock/blob/master/0005-auto-engine.diff
     
dget http://security.debian.org/debian-security/pool/updates/main/o/openssl/openssl_1.0.1e-2+deb7u13.dsc

#check current URL for actual *.dsc at https://packages.debian.org/wheezy/openssl

dpkg-source -x *.dsc

cd openssl*/

patch -p1 < ../0001*; patch -p1 < ../0002*; patch -p1 < ../0003*; patch -p1 < ../0004*; patch -p1 < ../0005*

dpkg-source --commit

#You will be asked for a filename (enter "padlock") and launch a text editor, just press Ctrl-X(nano) or enter :x(vim) to exit

dpkg-buildpackage -rfakeroot -b

#Check output in order to install missing development packages. Then retry.

cd ..
dpkg -i openssl*.deb libssl1.0.0*.deb
aptitude hold openssl libssl1.0.0
