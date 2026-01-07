.PHONY: help
help:
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'
.DEFAULT_GOAL := help

.PHONY: install-deps-dev
install-deps-dev: ## install dependencies for development
	@which npm || echo "Please install Node.js ref. https://nodejs.org/en/download"
	@which marp || npm install -g @marp-team/marp-cli

THEME ?= themes/custom.css
INPUT_DIR ?= slides
OUTPUT_DIR ?= outputs

.PHONY: pptx
pptx: ## build pptx artifacts via Marp CLI (requires installing both of the browser and LibreOffice Impress. ref. https://github.com/marp-team/marp-cli)
	marp \
		--input-dir $(INPUT_DIR) \
		--theme $(THEME) \
		--output $(OUTPUT_DIR)/pptx \
		--html \
		--pptx \
		--pptx-editable \

.PHONY: pdf
pdf: ## build pdf artifacts via Marp CLI
	marp \
		--input-dir $(INPUT_DIR) \
		--theme $(THEME) \
		--output $(OUTPUT_DIR)/pdf \
		--html \
		--pdf \

.PHONY: build
build: pptx pdf ## build artifacts

.PHONY: clean
clean: ## clean artifacts
	rm -rf $(OUTPUT_DIR)/*

.PHONY: ci-test
ci-test: clean install-deps-dev build ## run CI test

.PHONY: run
run: ## run applications
	marp \
		--input-dir slides \
		--theme $(THEME) \
		--html \
		--watch \
		--server
