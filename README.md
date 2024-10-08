# SonarLint Bug Illustration

The project contains a file named `FileСоntainsUtfSymbols.tsx`, where the letters `C` and `o` are actually Cyrillic UTF-8 characters.

This leads to errors such as:

```
 [2024-10-08T13:17:39.587] [SonarLint Server RPC request executor] ERROR org.eclipse.lsp4j.jsonrpc.RemoteEndpoint - Internal error: java.lang.IllegalArgumentException: Bad escape
java.util.concurrent.CompletionException: java.lang.IllegalArgumentException: Bad escape
	at java.base/java.util.concurrent.CompletableFuture.encodeThrowable(CompletableFuture.java:315)
	at java.base/java.util.concurrent.CompletableFuture.completeThrowable(CompletableFuture.java:320)
	at java.base/java.util.concurrent.CompletableFuture$UniApply.tryFire(CompletableFuture.java:649)
	at java.base/java.util.concurrent.CompletableFuture$Completion.run(CompletableFuture.java:482)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1144)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:642)
	at java.base/java.lang.Thread.run(Thread.java:1583)
Caused by: java.lang.IllegalArgumentException: Bad escape
	at java.base/sun.nio.fs.UnixUriUtils.fromUri(UnixUriUtils.java:88)
	at java.base/sun.nio.fs.UnixFileSystemProvider.getPath(UnixFileSystemProvider.java:125)
	at java.base/java.nio.file.Path.of(Path.java:204)
	at org.sonarsource.sonarlint.core.commons.util.FileUtils.getFileRelativePath(FileUtils.java:39)
	at org.sonarsource.sonarlint.core.commons.SonarLintGitIgnore.getFileRelativePath(SonarLintGitIgnore.java:68)
	at org.sonarsource.sonarlint.core.commons.SonarLintGitIgnore.isIgnored(SonarLintGitIgnore.java:44)
	at org.sonarsource.sonarlint.core.commons.SonarLintGitIgnore.isFileIgnored(SonarLintGitIgnore.java:61)
	at org.sonarsource.sonarlint.core.analysis.AnalysisService.lambda$toInputFiles$44(AnalysisService.java:775)
	at java.base/java.util.stream.ReferencePipeline$2$1.accept(ReferencePipeline.java:178)
	at java.base/java.util.stream.ReferencePipeline$2$1.accept(ReferencePipeline.java:179)
	at java.base/java.util.ArrayList$ArrayListSpliterator.forEachRemaining(ArrayList.java:1708)
	at java.base/java.util.stream.AbstractPipeline.copyInto(AbstractPipeline.java:509)
	at java.base/java.util.stream.AbstractPipeline.wrapAndCopyInto(AbstractPipeline.java:499)
	at java.base/java.util.stream.ReduceOps$ReduceOp.evaluateSequential(ReduceOps.java:921)
	at java.base/java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:234)
	at java.base/java.util.stream.ReferencePipeline.collect(ReferencePipeline.java:682)
	at org.sonarsource.sonarlint.core.analysis.AnalysisService.toInputFiles(AnalysisService.java:817)
	at org.sonarsource.sonarlint.core.analysis.AnalysisService.getAnalysisConfigForEngine(AnalysisService.java:276)
	at org.sonarsource.sonarlint.core.analysis.AnalysisService.analyze(AnalysisService.java:643)
	at org.sonarsource.sonarlint.core.rpc.impl.AnalysisRpcServiceDelegate.lambda$analyzeFilesAndTrack$8(AnalysisRpcServiceDelegate.java:141)
	at org.sonarsource.sonarlint.core.rpc.impl.AbstractRpcServiceDelegate.lambda$requestAsync$0(AbstractRpcServiceDelegate.java:67)
	at org.sonarsource.sonarlint.core.rpc.impl.AbstractRpcServiceDelegate.computeWithLogger(AbstractRpcServiceDelegate.java:135)
	at org.sonarsource.sonarlint.core.rpc.impl.AbstractRpcServiceDelegate.lambda$requestAsync$1(AbstractRpcServiceDelegate.java:65)
	at java.base/java.util.concurrent.CompletableFuture$UniApply.tryFire(CompletableFuture.java:646)
	... 4 common frames omitted

Error during analysis ID c4d0d261-77a3-4dfc-a2a5-2f26f38fe310
org.eclipse.lsp4j.jsonrpc.ResponseErrorException: Internal error.
	at org.eclipse.lsp4j.jsonrpc.RemoteEndpoint.handleResponse(RemoteEndpoint.java:220)
	at org.eclipse.lsp4j.jsonrpc.RemoteEndpoint.consume(RemoteEndpoint.java:204)
	at org.sonarsource.sonarlint.core.rpc.protocol.SingleThreadedMessageConsumer.lambda$new$0(SingleThreadedMessageConsumer.java:51)
	at java.base/java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:572)
	at java.base/java.util.concurrent.FutureTask.run(FutureTask.java:317)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1144)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:642)
	at java.base/java.lang.Thread.run(Thread.java:1583)

```
