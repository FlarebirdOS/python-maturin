pkgname=python-maturin
pkgver=1.9.6
pkgrel=2
pkgdesc="Build and publish crates with pyo3, rust-cpython and cffi bindings"
arch=('x86_64')
url="https://github.com/PyO3/maturin"
license=('Apache-2.0 OR MIT')
depends=(
    'bzip2'
    'gcc-libs'
    'glibc'
    'openssl'
    'python'
    'rust'
    'xz'
)
makedepends=(
    'python-build'
    'python-installer'
    'python-setuptools'
    'python-setuptools-rust'
    'python-wheel'
)
options=('!lto')
source=(https://github.com/PyO3/maturin/archive/v${pkgver}/${pkgname#*-}-${pkgver}.tar.gz)
sha256sums=(c8aef8af6cd3d5b3331191b21191ec92d7b4ee0633e0799351a01af1c5ea2a6c)

prepare() {
    cd ${pkgname#*-}-${pkgver}

    cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
    cd ${pkgname#*-}-${pkgver}

    MATURIN_SETUP_ARGS="--frozen" python3 -m build --wheel --no-isolation
}

package() {
    cd ${pkgname#*-}-${pkgver}

    python3 -m installer --destdir=${pkgdir} dist/*.whl
}
