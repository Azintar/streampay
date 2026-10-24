PYTHON ?= python3
VECTORS_BUILDER := vectors/builder

.PHONY: help spec generate check check-spec vectors

help:
	@echo "spec              re-derive spec/streampay.spec.json + FINGERPRINT from the contract"
	@echo "generate          run every language emitter whose package is present"
	@echo "check             schema guard + spec/vector/catalog tests + generated-output drift"
	@echo "check-spec        schema guard + tests only"
	@echo "vectors           rebuild conformance vectors (deterministic)"

spec:
	$(PYTHON) generator/check_contract_surface.py --write-spec

generate:
	$(PYTHON) generator/generate.py

check-spec:
	$(PYTHON) generator/check_contract_surface.py
	$(PYTHON) -m unittest discover -s generator -p "test_*.py" -v

check: check-spec
	$(PYTHON) generator/generate.py --check

vectors:
	cd $(VECTORS_BUILDER) && npm ci && node build-vectors.mjs
