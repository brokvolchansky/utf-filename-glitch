# SonarLint Bug Illustration

The project contains a file named `FileСоntainsUtfSymbols.tsx`, where the letters `C` and `o` are actually Cyrillic UTF-8 characters.

Environment:
```
OS: Macos 15.0.1 (Sequoia)
IntelliJ IDEA 2024.2.3 (Ultimate Edition)
Build #IU-242.23339.11, built on September 25, 2024
Licensed to ****
Subscription is active until April 30, 2025.
Runtime version: 21.0.4+13-b509.17 aarch64 (JCEF 122.1.9)
VM: OpenJDK 64-Bit Server VM by JetBrains s.r.o.
Toolkit: sun.lwawt.macosx.LWCToolkit
macOS 15.0.1
GC: G1 Young Generation, G1 Concurrent GC, G1 Old Generation
Memory: 4000M
Cores: 12
Metal Rendering is ON
Registry:
  ide.balloon.shadow.size=0
  ide.intellij.laf.enable.animation=true
  ide.experimental.ui=true
  i18n.locale=
  ide.images.show.chessboard=true
Non-Bundled Plugins:
  com.intellij.plugins.macoskeymap (241.13688.16)
  com.mallowigi.idea (23.0.0)
  com.vecheslav.darculaDarkerTheme (1.2.0)
  org.jetbrains.plugins.go (242.23339.11)
  lermitage.jetbrains.darcula.sombre (1.11.0.192)
  Intellij_GitHub_Dark_Theme (1.1.3)
  com.github.voml.neo_theme (0.4.2)
  org.mvnsearch.plugins.justPlugin (0.6.0)
  com.github.iyashpal.intellijgithubthemes (0.0.23)
  club.nutsoft.Github3Theme (1.2.2)
  com.redhat.devtools.lsp4ij (0.6.0)
  PythonCore (242.23339.11)
  aws.toolkit.core (3.31-242)
  com.jetbrains.space (242.23339.11)
  Rider UI Theme Pack (0.15.0)
  com.xrosstools.idea.gef (1.1.1)
  PlantUML integration (7.11.2-IJ2023.2)
  org.plugin.dot.id (1.5.4)
  dev.meanmail.plugin.nginx-intellij-plugin (2024.3)
  com.cppcxy.Intellij-SumnekoLua (3.9.3.33-IDEA241)
  Pythonid (242.23339.11)
  com.intellij.mermaid (0.0.22+IJ.232)
  com.intellij.ml.llm (242.23339.40)
  mobi.hsz.idea.gitignore (4.5.3)
  Dart (242.22855.32)
  org.jetbrains.android (242.23339.11)
  com.jetbrains.packagesearch.intellij-plugin (242.0.12)
  org.intellij.prisma (242.22855.32)
  com.github.jk1.ytplugin (2024.2.123)
  amazon.q (3.31-242)
  net.ashald.envfile (3.4.2)
  org.sonarlint.idea (10.11.1.79663)
  ru.adelf.idea.dotenv (2024.2.1)
  com.ypwang.plugin.go-linter (1.6.6)
  aws.toolkit (3.31-242)
  dev.nx.console (1.32.1)
Kotlin: 242.23339.11-IJ

openjdk version "23" 2024-09-17
OpenJDK Runtime Environment Homebrew (build 23)
OpenJDK 64-Bit Server VM Homebrew (build 23, mixed mode, sharing)

node.js v22.9.0

SonarLint 10.11.1.79663

project type: vite typescript react
```

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
