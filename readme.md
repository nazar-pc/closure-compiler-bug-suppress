Reproducible example for https://github.com/google/closure-compiler/issues/2621
```
npm install
java -jar node_modules/google-closure-compiler/compiler.jar bad.js --compilation_level ADVANCED_OPTIMIZATIONS --language_in ECMASCRIPT5 --externs closure-externs.js --externs node-externs/util.js --externs node-externs/path.js --externs node-externs/fs.js --externs node-externs/events.js --externs node-externs/process.js --externs node-externs/https.js --externs node-externs/dgram.js --externs node-externs/string_decoder.js --externs node-externs/child_process.js --externs node-externs/net.js --externs node-externs/punycode.js --externs node-externs/core.js --externs node-externs/zlib.js --externs node-externs/vm.js --externs node-externs/stream.js --externs node-externs/tls.js --externs node-externs/readline.js --externs node-externs/http.js --externs node-externs/url.js --externs node-externs/dns.js --externs node-externs/repl.js --externs node-externs/cluster.js --externs node-externs/domain.js --externs node-externs/querystring.js --externs node-externs/crypto.js --externs node-externs/os.js --externs node-externs/tty.js --externs browser-externs/fileapi_synchronous.js
```

`good.js` and `bad.js` contain the same function with `/** @suppress {uselessCode} */`, but in one file it works (smaller in size), while in another (bigger in size) it throws a lot of warnings like this (it is asm.js, this is why warnings are expected):
```
bad.js:188769: WARNING - Suspicious code. The result of the 'bitor' operator is not being used.
                                                                                ua(142, x | 0, 73927) | 0;
                                                                                ^^^^^^^^^^^^^^^^^^^^^^^^^

bad.js:189002: WARNING - Suspicious code. The result of the 'bitor' operator is not being used.
                                                                na(77, A | 0, 0, 73880) | 0;
                                                                ^^^^^^^^^^^^^^^^^^^^^^^^^^^

bad.js:189018: WARNING - Suspicious code. The result of the 'bitor' operator is not being used.
                                                                        ua(142, z | 0, 74013) | 0;
                                                                        ^^^^^^^^^^^^^^^^^^^^^^^^^

bad.js:189288: WARNING - Suspicious code. The result of the 'bitor' operator is not being used.
                                                                na(77, A | 0, 0, 73880) | 0;
                                                                ^^^^^^^^^^^^^^^^^^^^^^^^^^^

bad.js:189304: WARNING - Suspicious code. The result of the 'bitor' operator is not being used.
                                                                        ua(142, z | 0, 74042) | 0;
                                                                        ^^^^^^^^^^^^^^^^^^^^^^^^^

bad.js:189462: WARNING - Suspicious code. The result of the 'bitor' operator is not being used.
                                                                        ua(142, t | 0, 74046) | 0;
                                                                        ^^^^^^^^^^^^^^^^^^^^^^^^^

bad.js:189480: WARNING - Suspicious code. The result of the 'bitor' operator is not being used.
                                                                                na(73, s | 0, (d ? f[A >> 2] | 0 : A) | 0, (d ? f[A + 4 >> 2] | 0 : a & 255) | 0) | 0;
                                                                                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

bad.js:189496: WARNING - Suspicious code. The result of the 'bitor' operator is not being used.
                                                                                        ua(142, r | 0, 74052) | 0;
                                                                                        ^^^^^^^^^^^^^^^^^^^^^^^^^

bad.js:189514: WARNING - Suspicious code. The result of the 'bitor' operator is not being used.
                                                                                                na(73, w | 0, (d ? f[B >> 2] | 0 : B) | 0, (d ? f[B + 4 >> 2] | 0 : a & 255) | 0) | 0;
                                                                                                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

bad.js:189530: WARNING - Suspicious code. The result of the 'bitor' operator is not being used.
                                                                                                        ua(142, v | 0, 73878) | 0;
                                                                                                        ^^^^^^^^^^^^^^^^^^^^^^^^^
```
