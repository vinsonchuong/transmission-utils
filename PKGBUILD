# Maintainer: Vinson Chuong <vinsonchuong@gmail.com>
pkgname='transmission-utils'
pkgver='0.0.1'
pkgrel=1
pkgdesc='A set of command-line scripts that automate common tasks in Transmission'
arch=('any')
url='https://github.com/vinsonchuong/transmission-utils'
license=('MIT')
groups=()
depends=('transmission-cli')
makedepends=('git' 'ruby-ronn' 'xidel')
checkdepends=()
optdepends=()
conflicts=()
provides=()
replaces=()
backup=()
options=()
install="$pkgname.install"
changelog="$pkgname.changelog"
source=("git+https://github.com/vinsonchuong/$pkgname#tag=v$pkgver")
noextract=()
md5sums=()

prepare() {
	return
}

build() {
	ls "$srcdir"
	exit
	cd "$srcdir"
	ronn docs/*.md
	mkdir 'help'
	local script
	for script in bin/*
	do
		local html=$(cat "docs/$script.1.html")
		html=$(echo "$HTML" | sed 's/<var>\([^<]*\)<\/var>/\&lt;\1\&gt;/g')
		{
			echo "$html" \
				| xidel -q --css '.man-name' -
			echo
			echo 'Usage:'
			echo "$html" \
				| xidel -q --css '#SYNOPSIS + p' - \
				| sed 's/^/  /'
			echo
			echo 'Options:'
			echo "$html" \
				| xidel -q --css '#OPTIONS + dl > *' - \
				| paste -d ':' - - \
				| column -t -s ':' \
				| sed 's/^/ /'
		} > "help/$script"
	done
}

check() {
	return
}

package() {
	exit
	cd "$srcdir"
	install -Dm755 -t "$pkgdir/usr/bin" $srcdir/bin/*
	install -Dm644 -t "$pkgdir/usr/share/doc/$pkgname" "$srcdir/README.md"
	install -Dm644 -t "$pkgdir/usr/share/doc/$pkgname/docs" $srcdir/docs/*
	install -Dm644 -t "$pkgdir/usr/share/licenses/$pkgname" "$srcdir/LICENSE"
	install -Dm644 -t "$pkgdir/usr/share/man/man1" $srcdir/docs/*.1
}
