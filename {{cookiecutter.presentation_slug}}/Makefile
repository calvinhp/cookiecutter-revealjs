.PHONY: clean start index.html

slide-theme := wildclouds_white

index.html: slides.md js/reveal.js css/theme/$(slide-theme).css
	pandoc -t revealjs -s -V revealjs-url=. \
		-V theme=$(slide-theme) \
		-V autoPlayMedia=false \
		-o "$@" "$<"

js/reveal.js:
	curl -LO https://github.com/hakimel/reveal.js/archive/master.zip
	bsdtar --strip-components=1 --exclude .gitignore --exclude LICENSE --exclude README.md --exclude demo.html --exclude index.html -xf master.zip
	rm master.zip
	npm install

css/theme/source/$(slide-theme).scss: themes/$(slide-theme).scss
	cp "$<" "$@"

css/theme/$(slide-theme).css: css/theme/source/$(slide-theme).scss
	node_modules/node-sass/bin/node-sass "$<" > "$@"

start: index.html
	npm start

clean:
	rm CONTRIBUTING.md || true
	rm LICENSE || true
	rm bower.json || true
	rm -rf css/ || true
	rm gruntfile.js || true
	rm index.html || true
	rm -rf js/ || true
	rm -rf lib/ || true
	rm package-lock.json || true
	rm package.json || true
	rm -rf plugin/ || true
	rm -rf test/ || true
	rm -rf node_modules/ || true
