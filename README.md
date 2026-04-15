

## Supported Hardware and Software
Platform is the Orion O6, supports the Armv9-A SVE2 and its cryptographic extensionsm and the SVE2 vector length is 128 bits. Evaluation is built on liboqs 0.15.0, oqs-provider 0.10.0, and OpenSSL 3.5.0.

## PQC Test
1. cd source_lib/liboqs_source
2. mkdir build && cd build
3. CC=clang CXX=clang++ ASM=clang cmake -GNinja .. \
  -DOQS_USE_OPENSSL=ON \
  -DOQS_DIST_BUILD=OFF \
  -DOQS_ENABLE_KEM_KYBER=OFF \
  -DCMAKE_C_FLAGS="-march=armv9-a+sve+sve2+sve2-aes+crypto+sve2-sha3 -DOQS_ENABLE_SVE2" \
  -DCMAKE_ASM_FLAGS="-march=armv9-a+sve+sve2+sve2-aes+crypto+sve2-sha3"
4. ninja
5. ./tests/kat_kem *
6. ./tests/kat_sig *
7. ./tests/speed_kem *
8. ./tests/speed_kem *

## TLS Handshake Test

### Installation Instructions
1. cp -r source_lib ../anon-sys-2026/tmp
2. bash ./setup.sh --use-local-sources
3. rm -rf ./test_data/alg_lists
4. cp -r ./source_lib/alg_lists ./test_data/alg_lists

### TLS Performance Testing
1. bash ./scripts/test_scripts/tls_generate_keys.sh
2. bash ./scripts/test_scripts/pqc_tls_performance_test.sh

### Testing Output Files
After the testing has been completed, unparsed results and automatically parsed results will be stored in the generated `test_data/` directory:

**Unparsed Results:** `test_data/up_results/`

**Parsed Results:** `test_data/results/`

### Project Clean
1. bash ./cleaner.sh

