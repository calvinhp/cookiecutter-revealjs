slide-theme := minions_white

index.html: slides.md js/reveal.js dist/theme/$(slide-theme).css ## build presentation and theme
	pandoc -t revealjs -s -V revealjs-url=. \
		-V theme=$(slide-theme) \
		-V width=1200 \
		-V center=false \
		-V autoPlayMedia=false \
		-V hash=true \
		-o "$@" "$<"

js/reveal.js:
	curl -LO https://github.com/hakimel/reveal.js/archive/master.zip
	bsdtar --strip-components=1 --exclude .gitignore --exclude LICENSE --exclude README.md --exclude demo.html --exclude index.html -xf master.zip
	rm master.zip
	npm install

css/theme/source/$(slide-theme).scss: themes/$(slide-theme).scss
	cp "$<" "$@"

dist/theme/$(slide-theme).css: css/theme/source/$(slide-theme).scss
	npm run build -- css-themes

start: index.html ## bulid presentation and start server
	@echo "Starting the local presentation server 🚀"
	@npm start

clean: ## clean up the working directory
	rm CONTRIBUTING.md || true
	rm LICENSE || true
	rm .npmignore || true
	rm -rf css/ || true
	rm gulpfile.js || true
	rm index.html || true
	rm -rf examples/ || true
	rm -rf js/ || true
	rm -rf lib/ || true
	rm package-lock.json || true
	rm package.json || true
	rm -rf plugin/ || true
	rm -rf test/ || true
	rm -rf node_modules/ || true
	rm -rf dist/ || true

watch: ## Watch for changes and rebuild
	@echo "♻️ Watching for changes..."
	@watchmedo tricks-from tricks.yaml

help: ## This help.
	@awk 'BEGIN 	{ FS = ":.*##"; target="";printf "\nUsage:\n  make \033[36m<target>\033[33m\n\nTargets:\033[0m\n" } \
		/^[a-zA-Z_-]+:.*?##/ { if(target=="")print ""; target=$$1; printf " \033[36m%-10s\033[0m %s\n\n", $$1, $$2 } \
		/^([a-zA-Z_-]+):/ {if(target=="")print "";match($$0, "(.*):"); target=substr($$0,RSTART,RLENGTH) } \
		/^\t## (.*)/ { match($$0, "[^\t#:\\\\]+"); txt=substr($$0,RSTART,RLENGTH);printf " \033[36m%-10s\033[0m", target; printf " %s\n", txt ; target=""} \
		/^## .*/ {match($$0, "## (.+)$$"); txt=substr($$0,4,RLENGTH);printf "\n\033[33m%s\033[0m\n", txt ; target=""} \
	' $(MAKEFILE_LIST)

.PHONY: help clean start watch
