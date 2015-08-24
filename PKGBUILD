# Maintainer: Joseph Kogut <joseph.kogut+AUR@gmail.com>
# Contributor: David Sutton <kantras - gmail.com>
# Contributor: Shanmu Thiagaraja <sthiagaraja+AUR@prshanmu.com>
# Contributor: Limao Luo
# Contributor: Luceo
# Contributor: Revellion

pkgname=xen
pkgver=xengt_preview_2015Q2
_xenver=4.5.0
pkgrel=1
pkgdesc="Virtual Machine Hypervisor & Tools"
arch=(i686 x86_64)
url="http://www.xenproject.org/"
license=(GPL2)
depends=(bridge-utils curl gnutls iproute2 libaio libcap-ng libiscsi libjpeg-turbo libnl libpng libseccomp lzo2 nss pixman pciutils python python2 sdl yajl spice usbredir)
[[ "$CARCH" == "x86_64" ]] && depends+=(lib32-glibc)
makedepends=(bin86 cmake dev86 git iasl markdown ocaml-findlib figlet wget spice-protocol)
optdepends=('xen-docs: Official Xen Documentation' 'openvswitch: Optional Networking support')
conflicts=(xen-4.2{,-testing-hg} xen-{gdbsx,hg-unstable,rc,git} xen-4.3{,-testing-hg})
backup=(etc/modules-load.d/$pkgname.conf etc/$pkgname/xl.conf etc/conf.d/xen{stored,consoled,domains,commons} etc/$pkgname/grub.conf)
options=(!buildflags !strip)
install=$pkgname.install
changelog=ChangeLog
source=(git+https://github.com/01org/XenGT-Preview-xen.git#branch=master-2015Q2-4.5
    git+https://github.com/01org/XenGT-Preview-qemu.git
    qemu-xen::git+git://git.qemu-project.org/qemu.git#branch=stable-1.3
    http://xenbits.xen.org/xen-extfiles/ipxe-git-9a93db3f0947484e30e753bbd61a10b17336e20e.tar.gz
    http://xenbits.xen.org/xen-extfiles/lwip-1.3.0.tar.gz
    http://xenbits.xen.org/xen-extfiles/zlib-1.2.3.tar.gz
    http://xenbits.xen.org/xen-extfiles/newlib-1.16.0.tar.gz
    http://xenbits.xen.org/xen-extfiles/pciutils-2.2.9.tar.bz2
    http://xenbits.xen.org/xen-extfiles/polarssl-1.1.4-gpl.tgz
    http://xenbits.xen.org/xen-extfiles/grub-0.97.tar.gz
    http://xenbits.xen.org/xen-extfiles/tpm_emulator-0.7.4.tar.gz
    http://xenbits.xen.org/xen-extfiles/gmp-4.3.2.tar.bz2
    xen.install
    tmpfiles.d-$pkgname.conf
    09_xen
    etherboot-gcc5.patch
    gcc5.patch
    efi-xen.cfg
    grub.conf
    $pkgname.conf
    seabios-gcc5.patch
    0001-Fix-build-error-caused-by-undersized-array.patch)

noextract=(lwip-1.3.0.tar.gz
    zlib-1.2.3.tar.gz
    newlib-1.16.0.tar.gz
    pciutils-2.2.9.tar.bz2
    polarssl-1.1.4-gpl.tgz
    grub-0.97.tar.gz
    tpm_emulator-0.7.4.tar.gz
    gmp-4.3.2.tar.bz2
    ipxe-git-9a93db3f0947484e30e753bbd61a10b17336e20e.tar.gz)

sha256sums=('SKIP'
	    'SKIP'
	    'SKIP'
            '632ce8c193ccacc3012bd354bdb733a4be126f7c098e111930aa41dad537405c'
            '772e4d550e07826665ed0528c071dd5404ef7dbe1825a38c8adbc2a00bca948f'
            '1795c7d067a43174113fdf03447532f373e1c6c57c08d61d9e4e9be5e244b05e'
            'db426394965c48c1d29023e1cc6d965ea6b9a9035d8a849be2750ca4659a3d07'
            'f60ae61cfbd5da1d849d0beaa21f593c38dac9359f0b3ddc612f447408265b24'
            '2d29fd04a0d0ba29dae6bd29fb418944c08d3916665dcca74afb297ef37584b6'
            '4e1d15d12dbd3e9208111d6b806ad5a9857ca8850c47877d36575b904559260b'
            '4e48ea0d83dd9441cc1af04ab18cd6c961b9fa54d5cbf2c2feee038988dea459'
            '936162c0312886c21581002b79932829aa048cfaf9937c6265aeaa14f1cd1775'
            '5bc10f125bdc1ae5f9e3eeb58888970d02e7856e94e2435d66ddb717884db016'
            '40e0760810a49f925f2ae9f986940b40eba477dc6d3e83a78baaae096513b3cf'
            '06c9f6140f7ef4ccfc4b1a7d9732a673313e269733180f53afcd9e43bf6c26bb'
            'deeec880522c1374ad135dc8b4c14c7b301464a60fbac410efb3db70f670eed9'
            'e7cfad0a641bee8d3ef302d4c6ca47779cd1ca6fd9f97c884f5c1fc741346203'
            'ceaff798a92a7aef1465a0a0b27b1817aedd2c857332b456aaa6dd78dc72438f'
            '3f0af16958c3e057b9baa5afc47050d9adf7dd553274dd97ae4f35938fefb568'
            '50a9b7fd19e8beb1dea09755f07318f36be0b7ec53d3c9e74f3266a63e682c0c'
            '091f5eed7e33b45cabb232e9a03dd6c1abae1a820b804c888c20d4b7e673618f'
            '3404b4b0c72a2ccddc21ca5ba00e4e206e26394adf58bdeb06b176341d8b6bdc')

prepare() {
    cd qemu-xen
    patch -p1 -i "$srcdir/XenGT-Preview-qemu/qemu-vgt.patch"

    cd ..
    cp -r ./qemu-xen ./XenGT-Preview-xen/tools/   

    cd ./XenGT-Preview-xen
    patch -p1 -i "$srcdir/gcc5.patch"
    patch -p1 -i "$srcdir/0001-Fix-build-error-caused-by-undersized-array.patch"
    echo "etherboot-gcc5.patch" >> tools/firmware/etherboot/patches/series
    cp "$srcdir/seabios-gcc5.patch" tools/firmware/
    cp "$srcdir/etherboot-gcc5.patch" tools/firmware/etherboot/patches/

    sed -i '/QEMU_UPSTREAM_URL/s:http\://xenbits.xen.org/git-http/qemu-upstream-4.5-testing.git:XenGT-Preview-xen/tools/qemu-xen:' Config.mk 
    sed -i '/QEMU_UPSTREAM_URL/s:git\://xenbits.xen.org/git-http/qemu-upstream-4.5-testing.git:XenGT-Preview-xen/tools/qemu-xen:' Config.mk 

    ## Fix Install Paths
    sed -i 's:\$localstatedir/run/xen:/run/xen:' m4/paths.m4
    sed -i 's:/var/run:/run:' tools/ocaml/xenstored/define.ml
    sed -i 's:/var/run:/run:' tools/ocaml/xenstored/systemd_stubs.c

    # Copy supporting tarballs into place
    cp "$srcdir/lwip-1.3.0.tar.gz" stubdom/
    cp "$srcdir/zlib-1.2.3.tar.gz" stubdom/
    cp "$srcdir/newlib-1.16.0.tar.gz" stubdom/
    cp "$srcdir/pciutils-2.2.9.tar.bz2" stubdom/
    cp "$srcdir/polarssl-1.1.4-gpl.tgz" stubdom/
    cp "$srcdir/grub-0.97.tar.gz" stubdom/
    cp "$srcdir/tpm_emulator-0.7.4.tar.gz" stubdom/
    cp "$srcdir/gmp-4.3.2.tar.bz2" stubdom/
    cp "$srcdir/ipxe-git-9a93db3f0947484e30e753bbd61a10b17336e20e.tar.gz" tools/firmware/etherboot/ipxe.tar.gz
}

build() {
    cd XenGT-Preview-xen
    export CFLAGS=-fno-caller-saves
    ./autogen.sh
    ./configure PYTHON=/usr/bin/python2 --prefix=/usr --sbindir=/usr/bin --with-sysconfig-leaf-dir=conf.d --with-initddir=/etc/init.d \
		--enable-systemd --disable-docs --enable-stubdom  --disable-qemu-traditional --enable-rombios \
		--with-extra-qemuu-configure-args="--disable-bluez --enable-spice --enable-usb-redir"
    make LANG=C PYTHON=python2
}

package() {
    cd XenGT-Preview-xen

    make DESTDIR="$pkgdir" LANG=C PYTHON=python2 install

    cd "$pkgdir"

    # Install files from AUR package
    install -Dm644 "$srcdir/tmpfiles.d-$pkgname.conf" usr/lib/tmpfiles.d/$pkgname.conf
    install -Dm644 "$srcdir/grub.conf" etc/xen/grub.conf
    install -Dm755 "$srcdir/09_xen" etc/grub.d/09_xen
    install -Dm644 "$srcdir/efi-xen.cfg" etc/xen/efi-xen.cfg

    # Fix paths in scripts, move to right locations and create missing directories
    sed -i 's:/var/run:/run:' etc/init.d/xencommons
    sed -i 's:/var/lock:/run/lock:' etc/xen/scripts/hotplugpath.sh
    sed -i 's:/var/run:/run:' etc/xen/scripts/locking.sh
    sed -i 's:/var/run:/run:' usr/lib/systemd/system/xenstored.service
    sed -i 's:/var/run:/run:' usr/lib/systemd/system/xenstored.socket
    sed -i 's:/var/run:/run:' usr/lib/systemd/system/xenstored_ro.socket

    mkdir var/log/xen/console

    # Sanitize library path (if lib64 exists)
    if [[ -d usr/lib64 ]]; then
        cd usr/
        cp -r lib64/* lib/
        rm -rf lib64
	cd ../
    fi

    # If EFI binaries build, move to /boot
    if [[ -f usr/lib/efi/xen.efi ]]; then
        mv usr/lib/efi/xen-$_xenver.efi boot/xen-$_xenver.efi
        rm -rf usr/lib/efi
    fi

    # Compress syms file and move to a share location
    gzip boot/xen-syms-*
    mv boot/xen-syms-*.gz usr/share/xen

    ##### Kill unwanted stuff #####
    # hypervisor symlinks
    rm -f boot/xen{,-4,-4.5,-4.5-rc}.gz

    # Documentation cleanup ( see xen-docs package )
    rm -rf usr/share/doc
    rm -rf usr/share/man

    # adhere to Static Library Packaging Guidelines
    rm -rf usr/lib/*.a

}
