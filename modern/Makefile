include ../Makefile.inc
OUTPUT_FILES=$(PUBNUB_MIN_JS) $(PUBNUB_CRYPTO_MIN_JS)

.PHONY	: all
all: build

.PHONY	: build
build: $(PUBNUB_MIN_JS) $(PUBNUB_CRYPTO_MIN_JS)

$(PUBNUB_MIN_JS) : $(PUBNUB_COMMON_JS) $(WEBSOCKET_JS) $(PUBNUB_PLATFORM_JS)
	## Full Version
	$(ECHO) -n "// Version: $(VERSION)\n" > $(PUBNUB_JS)
	cat $(JSON_JS) $(PUBNUB_COMMON_JS) $(PUBNUB_PLATFORM_JS) $(WEBSOCKET_JS) >> $(PUBNUB_JS)
	## Minfied Version
	$(ECHO) -n "// Version: $(VERSION)\n" > $(PUBNUB_MIN_JS)
	$(ECHO) "(function(){" > $(PUBNUB_MIN_JS)
	cat $(PUBNUB_JS) | java -jar $(GOOGLE_MINIFY) --compilation_level=ADVANCED_OPTIMIZATIONS >> $(PUBNUB_MIN_JS)
	$(ECHO) "})();" >> $(PUBNUB_MIN_JS)

$(PUBNUB_CRYPTO_MIN_JS) : $(GIBBERISH_JS) $(ENCRYPTO_JS)
	## Cryptography
	$(ECHO) "(function(){" > $(PUBNUB_CRYPTO_MIN_JS)
	cat $(GIBBERISH_JS) $(ENCRYPT_JS) | java -jar $(GOOGLE_MINIFY) >> $(PUBNUB_CRYPTO_MIN_JS)
	$(ECHO) "})();" >> $(PUBNUB_CRYPTO_MIN_JS)

.PHONY	: clean
clean:
	rm -f $(OUTPUT_FILES)
