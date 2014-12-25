# Maintainer: Vinson Chuong <vinsonchuong@gmail.com>
pkgname='transmission-utils'
pkgver='0.0.1'
pkgrel=1
pkgdesc='A set of command-line scripts that automate common tasks in Transmission'
arch=('any')
url='https://github.com/vinsonchuong/transmission-utils'
license=('MIT')
depends=('transmission-cli')
makedepends=('git' 'ruby-ronn' 'xidel')
source=("https://github.com/vinsonchuong/$pkgname/archive/v$pkgver.tar.gz")
md5sums=('SKIP')

build() {
	cd "$srcdir/$pkgname"
	ronn docs/*.md
	mkdir 'help'
	local script
	for script in $(find 'bin' -type f -printf "%f\n")
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

package() {
	cd "$srcdir/$pkgname"
	install -Dm755 -t "$pkgdir/usr/bin" bin/*
	install -Dm644 -t "$pkgdir/usr/share/doc/$pkgname" 'README.md'
	install -Dm644 -t "$pkgdir/usr/share/doc/$pkgname/docs" docs/*.md
	install -Dm644 -t "$pkgdir/usr/share/licenses/$pkgname" 'LICENSE'
	install -Dm644 -t "$pkgdir/usr/share/man/man1" docs/*.1
}
