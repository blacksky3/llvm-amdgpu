# _     _            _        _          _____
#| |__ | | __ _  ___| | _____| | ___   _|___ /
#| '_ \| |/ _` |/ __| |/ / __| |/ / | | | |_ \
#| |_) | | (_| | (__|   <\__ \   <| |_| |___) |
#|_.__/|_|\__,_|\___|_|\_\___/_|\_\\__, |____/
#                                  |___/

#Maintainer: blacksky3 <https://github.com/blacksky3>

major=5.4.3
libdrm_major=2.4.113
minor1=50403
minor2=1538762
ubuntu_ver=22.04
repo_folder_ver=5.4.3
llvm_ver=15.0

pkgbase=llvm-amdgpu
pkgname=(llvm-amdgpu lib32-llvm-amdgpu)
pkgver=${major}
pkgrel=1
url='https://repo.radeon.com/amdgpu'
license=(MIT)
source=(https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/libllvm${llvm_ver}.${minor1}-amdgpu_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/libllvm${llvm_ver}.${minor1}-amdgpu_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu-${llvm_ver}.${minor1}-dev_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu-${llvm_ver}.${minor1}-dev_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu-${llvm_ver}.${minor1}-runtime_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu-${llvm_ver}.${minor1}-runtime_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu-${llvm_ver}.${minor1}_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu-${llvm_ver}.${minor1}_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu-dev_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu-dev_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu-runtime_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu-runtime_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
        https://repo.radeon.com/amdgpu/${repo_folder_ver}/ubuntu/pool/main/l/llvm-amdgpu/llvm-amdgpu_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb)

extract_deb(){
  local tmpdir="$(basename "${1%.deb}")"
  rm -Rf "$tmpdir"
  mkdir "$tmpdir"
  cd "$tmpdir"
  ar x "$1"
  tar -C "${pkgdir}" -xf data.tar.xz
}

move_libdir(){
  local deb_libdir="$1"
  local arch_libdir="$2"

  if [ -d "${pkgdir}/${deb_libdir}" ]; then
    if [ ! -d "${pkgdir}/${arch_libdir}" ]; then
      mkdir -p "${pkgdir}/${arch_libdir}"
    fi
    mv -t "${pkgdir}/${arch_libdir}/" "${pkgdir}/${deb_libdir}"/*
    find ${pkgdir} -type d -empty -delete
  fi
}

move_copyright(){
  find ${pkgdir}/usr/share/doc -name "changelog.Debian.gz" -delete
  mkdir -p ${pkgdir}/usr/share/licenses/${pkgname}
  find ${pkgdir}/usr/share/doc -name "copyright" -exec mv {} ${pkgdir}/usr/share/licenses/${pkgname} \;
  find ${pkgdir}/usr/share/doc -type d -empty -delete
}

package_llvm-amdgpu(){
  pkgdesc='AMDGPU LLVM'
  arch=(x86_64)

  extract_deb "${srcdir}"/libllvm${llvm_ver}.${minor1}-amdgpu_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
  extract_deb "${srcdir}"/llvm-amdgpu-${llvm_ver}.${minor1}-dev_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
  extract_deb "${srcdir}"/llvm-amdgpu-${llvm_ver}.${minor1}-runtime_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
  extract_deb "${srcdir}"/llvm-amdgpu-${llvm_ver}.${minor1}_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
  extract_deb "${srcdir}"/llvm-amdgpu-dev_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
  extract_deb "${srcdir}"/llvm-amdgpu-runtime_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
  extract_deb "${srcdir}"/llvm-amdgpu_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_amd64.deb
  move_libdir "opt/amdgpu/lib/x86_64-linux-gnu/" "opt/amdgpu/lib"
  move_copyright

  rm -rf "$pkgdir"/opt/amdgpu/bin
  rm -rf "$pkgdir"/opt/amdgpu/include
  rm -rf "$pkgdir"/opt/amdgpu/lib/cmake
  rm -rf "$pkgdir"/opt/amdgpu/lib/*.so*
  move_libdir "opt/amdgpu/lib/llvm-15.0/bin" "opt/amdgpu/bin"
  move_libdir "opt/amdgpu/lib/llvm-15.0/include" "opt/amdgpu/include"
  move_libdir "opt/amdgpu/lib/llvm-15.0/share" "opt/amdgpu/share"
  move_libdir "opt/amdgpu/lib/llvm-15.0/lib" "opt/amdgpu/lib"

  mv "$pkgdir"/usr/share/binfmts/llvm-amdgpu-15.0.50403-runtime.binfmt "$pkgdir"/usr/share/binfmts/llvm-amdgpu-15.0.50403-runtime.binfmt-x86_64
}

package_lib32-llvm-amdgpu(){
  pkgdesc='AMDGPU LLVM (32-bit)'
  arch=(i686 x86_64)
  depends=(llvm-amdgpu=${major})

  extract_deb "${srcdir}"/libllvm${llvm_ver}.${minor1}-amdgpu_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
  extract_deb "${srcdir}"/llvm-amdgpu-${llvm_ver}.${minor1}-dev_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
  extract_deb "${srcdir}"/llvm-amdgpu-${llvm_ver}.${minor1}-runtime_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
  extract_deb "${srcdir}"/llvm-amdgpu-${llvm_ver}.${minor1}_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
  extract_deb "${srcdir}"/llvm-amdgpu-dev_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
  extract_deb "${srcdir}"/llvm-amdgpu-runtime_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
  extract_deb "${srcdir}"/llvm-amdgpu_${llvm_ver}.${minor1}-${minor2}.${ubuntu_ver}_i386.deb
  move_libdir "opt/amdgpu/lib/i386-linux-gnu" "opt/amdgpu/lib32"
  move_copyright

  rm -rf "$pkgdir"/opt/amdgpu/bin
  rm -rf "$pkgdir"/opt/amdgpu/include
  rm -rf "$pkgdir"/opt/amdgpu/lib/cmake
  rm -rf "$pkgdir"/opt/amdgpu/lib/*.so*
  #rm -rf "$pkgdir"/opt/amdgpu/lib32/llvm-15.0/bin
  rm -rf "$pkgdir"/opt/amdgpu/lib32/llvm-15.0/include
  rm -rf "$pkgdir"/opt/amdgpu/lib32/llvm-15.0/share
  move_libdir "opt/amdgpu/lib32/llvm-15.0/lib" "opt/amdgpu/lib32"
  move_libdir "opt/amdgpu/lib32/llvm-15.0/bin" "opt/amdgpu/bin"

  mv "$pkgdir"/usr/share/binfmts/llvm-amdgpu-15.0.50403-runtime.binfmt "$pkgdir"/usr/share/binfmts/llvm-amdgpu-15.0.50403-runtime.binfmt-i386
  sed -i 's|lli|lli32|' "$pkgdir"/usr/share/binfmts/llvm-amdgpu-15.0.50403-runtime.binfmt-i386

  rm -rf "$pkgdir"/opt/amdgpu/bin/llvm-addr2line
  ln -s /opt/amdgpu/bin/llvm-symbolizer32 "$pkgdir"/opt/amdgpu/bin/llvm-addr2line
  rm -rf "$pkgdir"/opt/amdgpu/bin/llvm-bitcode-strip
  ln -s /opt/amdgpu/bin/llvm-objcopy32 "$pkgdir"/opt/amdgpu/bin/llvm-bitcode-strip
  rm -rf "$pkgdir"/opt/amdgpu/bin/llvm-dlltool
  ln -s /opt/amdgpu/bin/llvm-ar32 "$pkgdir"/opt/amdgpu/bin/llvm-dlltool
  rm -rf "$pkgdir"/opt/amdgpu/bin/llvm-install-name-tool
  ln -s /opt/amdgpu/bin/llvm-objcopy32 "$pkgdir"/opt/amdgpu/bin/llvm-install-name-tool
  rm -rf "$pkgdir"/opt/amdgpu/bin/llvm-lib
  ln -s /opt/amdgpu/bin/llvm-ar32 "$pkgdir"/opt/amdgpu/bin/llvm-lib
  rm -rf "$pkgdir"/opt/amdgpu/bin/llvm-ranlib
  ln -s /opt/amdgpu/bin/llvm-ar32 "$pkgdir"/opt/amdgpu/bin/llvm-ranlib
  rm -rf "$pkgdir"/opt/amdgpu/bin/llvm-readelf
  ln -s /opt/amdgpu/bin/llvm-readobj32 "$pkgdir"/opt/amdgpu/bin/llvm-readelf
  rm -rf "$pkgdir"/opt/amdgpu/bin/llvm-strip
  ln -s /opt/amdgpu/bin/llvm-objcopy32 "$pkgdir"/opt/amdgpu/bin/llvm-strip
  rm -rf "$pkgdir"/opt/amdgpu/bin/llvm-windres
  ln -s /opt/amdgpu/bin/llvm-rc32 "$pkgdir"/opt/amdgpu/bin/llvm-windres

  # append 32 at the end of binary files
  for i in "${pkgdir}/opt/amdgpu/bin/"*; do
    mv "$i" "$i"32
  done
}

sha256sums=('df94a0e8971f9c9f2e0070e0f633c4e6778cfef6c86961089391e6a16b1160e3'
            'da277c9b3d7a9ee9a1dc551a9f3d1deca09193bcb5be637d5675291022ac3349'
            '4306494cd5631b2df1f13f307961e89203ffd65b47e6e89bab1e26510b92694b'
            '2bd699d747a954bbb319c32217e7bbb785cfde10722581a8c9ca14e3e938b520'
            'e75954bd98d5f3df0b573b409159d957b9f90c4f79e509c8ebdbae12407511eb'
            '9cef345ff9996bf2c53abebb93c5383b1212a6ad207dd2f918dbb1d1b8756c25'
            '807043f82573f6e34737dc1a049473d5ac55a3d70cd4c21868b09818614329b8'
            '30619f01ded722c2683ca0e27771501e7c226aefa3bb11d739a125c864d4ae91'
            '00a8192c302366fb6e26292ee69723eb315455ce5f88e8ebd323979286000f3d'
            'a8fc7894b68b2f9733234a293f477b21842999bc2df3300104bcb18128804fa3'
            'de0ac0bb70bcddc8ab01790ed46fdd687c557f8756516984302fa24f950a782d'
            '740c7e1ad250cdc76a295d70deed9e60869e6b58852df734ae5c189b10b77784'
            '2dad1ad2a1742cc32c4f0b51996045ba3255d400ff46210e002bd5d8b09ef088'
            'e8bff3dfc5a1dece8d1b138bf2205383a95eb32c73555778a84b6a2ad98abe7c')
