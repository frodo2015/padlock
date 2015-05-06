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

