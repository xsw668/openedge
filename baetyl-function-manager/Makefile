TAG?=latest
SRC=$(shell find . -type f -name '*.go')

all: baetyl-function-manager package.zip

baetyl-function-manager: $(SRC)
	@echo "BUILD $@"
	@CGO_ENABLED=0 go build ${GOFLAG} .

package.zip: baetyl-function-manager
	install -d -m 0755 __package/bin
	cp $< __package/bin
	cp package.yml __package/
	cd __package && zip -q -r ../package.zip bin/ package.yml
	rm -rf __package

image: baetyl-function-manager
	@echo "IMAGE $<"
	docker build -t $(IMAGE_PREFIX)$<:$(TAG) .

.PHONY: clean
clean:
	rm -f baetyl-function-manager package.zip

.PHONY: rebuild
rebuild: clean all
