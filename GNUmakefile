BIN = ./node_modules/.bin
BEM = $(BIN)/bem
MOCHA = $(BIN)/mocha
ISTANBUL = $(BIN)/istanbul
JSHINT = $(BIN)/jshint

.PHONY: all
all:

.PHONY: clean
clean: clean-coverage
	-rm -rf test-make-temp

.PHONY: clean-coverage
clean-coverage:
	-rm -rf lib-cov
	-rm -rf html-report

.PHONY: jshint
jshint:
	$(JSHINT) lib test

.PHONY: test
test: jshint
	$(MOCHA)

.PHONY: lib-cov
lib-cov: clean-coverage
	$(ISTANBUL) instrument --output lib-cov --no-compact --variable global.__coverage__ lib

.PHONY: test-cover
test-cover: lib-cov test
	BEM_COVER=1 $(MOCHA) --reporter mocha-istanbul
	@echo
	@echo Open html-report/index.html file in your browser

.PHONY: tests
tests:
	-rm -rf tests/level4
	$(BEM) create level -o tests -l simple -T css -T js -t xsl level4
	$(BEM) create block -l tests/level4 -T css -T js -t xsl first-block
	$(BEM) create elem -l tests/level4 -b first-block -T css -T js -t xsl elem1
	$(BEM) create mod -l tests/level4 -b first-block mod1
	$(BEM) create mod -l tests/level4 -b first-block -v 1 mod1

	-rm -rf tests/level5
	$(BEM) create level -o tests -l tests/level2/.bem/level.js -t css -t css1 -n js -n js1 level5
	$(BEM) create block -l tests/level5 first-block
	$(BEM) create elem -l tests/level5 -b second-block -n css1 elem2
	$(BEM) create mod -l tests/level5 -b second-block mod2
	$(BEM) create mod -l tests/level5 -b second-block -e elem2 -v 221 -v 222 mod22

	$(BEM) build -d tests/decl.js -o tests -n bla -t deps.js -t ie.css -l tests/level1 -l tests/level2 -l tests/level3 -l tests/level4 -l tests/level5
	$(BEM) build -d tests/bla.deps.js -o tests -n bla -t css -t js -l tests/level1 -l tests/level2 -l tests/level3 -l tests/level4 -l tests/level5

	$(BEM) decl subtract -o tests/deps-subtract.deps.js -d tests/deps-subtract-1.deps.js -d tests/deps-subtract-2.deps.js
	$(BEM) decl merge -o tests/deps-merge.deps.js -d tests/deps-merge-1.deps.js -d tests/deps-merge-2.deps.js
