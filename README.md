Run [PskTlsTest.java](https://github.com/justincranford/bc-tls-psk/blob/main/src/test/java/com/github/justincranford/psk/PskTlsTest.java) as a JUnit 5 test. It runs a client/server echo test, 10 times using Plaintext, and 10 times using TLS PSK.
1. 100%: Plaintext tests #1 through #10 always pass.
2. ~10%: TLS PSK test #1 intermittently passes (10%), or fails (90%) with exception `TlsFatalAlertReceived: bad_record_mac(20)`.
3. 100%: TLS PSK tests #2 through #10 always pass.

As a quick estimate, I seem to have to re-run the JUnit test about 10 times before I get all tests to pass. The rest of the runs, the first TLS PSK test fails.

Below are screenshots showing all tests passed (1 run of 10), versus all tests passed except the first TLS PSK test (9 runs out of 10).

![image](https://github.com/user-attachments/assets/813b0665-2b37-4d87-b643-b9a009035398)
![image](https://github.com/user-attachments/assets/3a6ca94b-fa85-4875-ae30-4bd9d3f97b01)

If TLS PSK test #1 fails, the stack trace is:
```
com.github.justincranford.psk.PskTlsTest
testTlsPsk(com.github.justincranford.psk.PskTlsTest)
org.bouncycastle.tls.TlsFatalAlertReceived: bad_record_mac(20)
	at org.bouncycastle.tls.TlsProtocol.handleAlertMessage(TlsProtocol.java:245)
	at org.bouncycastle.tls.TlsProtocol.processAlertQueue(TlsProtocol.java:740)
	at org.bouncycastle.tls.TlsProtocol.processRecord(TlsProtocol.java:563)
	at org.bouncycastle.tls.RecordStream.readRecord(RecordStream.java:247)
	at org.bouncycastle.tls.TlsProtocol.safeReadRecord(TlsProtocol.java:879)
	at org.bouncycastle.tls.TlsProtocol.blockForHandshake(TlsProtocol.java:427)
	at org.bouncycastle.tls.TlsClientProtocol.connect(TlsClientProtocol.java:88)
	at com.github.justincranford.psk.PskTlsTest$PskTlsClient.send(PskTlsTest.java:79)
	at com.github.justincranford.psk.PskTlsTest.doClientServer(PskTlsTest.java:62)
	at com.github.justincranford.psk.PskTlsTest.testTlsPsk(PskTlsTest.java:51)
	at java.base/java.lang.reflect.Method.invoke(Method.java:580)
	at java.base/java.util.stream.ForEachOps$ForEachOp$OfRef.accept(ForEachOps.java:184)
	at java.base/java.util.stream.ReferencePipeline$3$1.accept(ReferencePipeline.java:197)
	at java.base/java.util.stream.ReferencePipeline$2$1.accept(ReferencePipeline.java:179)
	at java.base/java.util.stream.ReferencePipeline$3$1.accept(ReferencePipeline.java:197)
	at java.base/java.util.stream.ForEachOps$ForEachOp$OfRef.accept(ForEachOps.java:184)
	at java.base/java.util.stream.ReferencePipeline$3$1.accept(ReferencePipeline.java:197)
	at java.base/java.util.stream.ForEachOps$ForEachOp$OfRef.accept(ForEachOps.java:184)
	at java.base/java.util.stream.ForEachOps$ForEachOp$OfRef.accept(ForEachOps.java:184)
	at java.base/java.util.stream.ReferencePipeline$3$1.accept(ReferencePipeline.java:197)
	at java.base/java.util.Spliterators$ArraySpliterator.forEachRemaining(Spliterators.java:1024)
	at java.base/java.util.stream.AbstractPipeline.copyInto(AbstractPipeline.java:509)
	at java.base/java.util.stream.AbstractPipeline.wrapAndCopyInto(AbstractPipeline.java:499)
	at java.base/java.util.stream.ForEachOps$ForEachOp.evaluateSequential(ForEachOps.java:151)
	at java.base/java.util.stream.ForEachOps$ForEachOp$OfRef.evaluateSequential(ForEachOps.java:174)
	at java.base/java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:234)
	at java.base/java.util.stream.ReferencePipeline.forEach(ReferencePipeline.java:596)
	at java.base/java.util.stream.ReferencePipeline$7$1.accept(ReferencePipeline.java:276)
	at java.base/java.util.ArrayList$ArrayListSpliterator.forEachRemaining(ArrayList.java:1708)
	at java.base/java.util.stream.AbstractPipeline.copyInto(AbstractPipeline.java:509)
	at java.base/java.util.stream.AbstractPipeline.wrapAndCopyInto(AbstractPipeline.java:499)
	at java.base/java.util.stream.ForEachOps$ForEachOp.evaluateSequential(ForEachOps.java:151)
	at java.base/java.util.stream.ForEachOps$ForEachOp$OfRef.evaluateSequential(ForEachOps.java:174)
	at java.base/java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:234)
	at java.base/java.util.stream.ReferencePipeline.forEach(ReferencePipeline.java:596)
	at java.base/java.util.stream.ReferencePipeline$7$1.accept(ReferencePipeline.java:276)
	at java.base/java.util.stream.ReferencePipeline$3$1.accept(ReferencePipeline.java:197)
	at java.base/java.util.stream.ReferencePipeline$3$1.accept(ReferencePipeline.java:197)
	at java.base/java.util.stream.ReferencePipeline$3$1.accept(ReferencePipeline.java:197)
	at java.base/java.util.ArrayList$ArrayListSpliterator.forEachRemaining(ArrayList.java:1708)
	at java.base/java.util.stream.AbstractPipeline.copyInto(AbstractPipeline.java:509)
	at java.base/java.util.stream.AbstractPipeline.wrapAndCopyInto(AbstractPipeline.java:499)
	at java.base/java.util.stream.ForEachOps$ForEachOp.evaluateSequential(ForEachOps.java:151)
	at java.base/java.util.stream.ForEachOps$ForEachOp$OfRef.evaluateSequential(ForEachOps.java:174)
	at java.base/java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:234)
	at java.base/java.util.stream.ReferencePipeline.forEach(ReferencePipeline.java:596)
	at java.base/java.util.stream.ReferencePipeline$7$1.accept(ReferencePipeline.java:276)
	at java.base/java.util.ArrayList$ArrayListSpliterator.forEachRemaining(ArrayList.java:1708)
	at java.base/java.util.stream.AbstractPipeline.copyInto(AbstractPipeline.java:509)
	at java.base/java.util.stream.AbstractPipeline.wrapAndCopyInto(AbstractPipeline.java:499)
	at java.base/java.util.stream.ForEachOps$ForEachOp.evaluateSequential(ForEachOps.java:151)
	at java.base/java.util.stream.ForEachOps$ForEachOp$OfRef.evaluateSequential(ForEachOps.java:174)
	at java.base/java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:234)
	at java.base/java.util.stream.ReferencePipeline.forEach(ReferencePipeline.java:596)
	at java.base/java.util.ArrayList.forEach(ArrayList.java:1596)
	at java.base/java.util.ArrayList.forEach(ArrayList.java:1596)
```
