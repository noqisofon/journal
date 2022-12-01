---
title: Grab に失敗する
date: 2022-12-01T21:10:30+09:00
draft: false
section: groovy
---

``` groovy
@Grab(group='org.openjfx', module='javafx-base', version='19')
import javafx.application.Application
```

これを実行すると以下のような表示が出る。

```
Caught: java.lang.NoClassDefFoundError: org/apache/ivy/util/MessageLogger
java.lang.NoClassDefFoundError: org/apache/ivy/util/MessageLogger
    at java.base/java.lang.Class.forName0(Native Method)
    at java.base/java.lang.Class.forName(Class.java:390)
    at java.base/java.lang.Class.forName(Class.java:381)
    at groovy.grape.Grape.getInstance(Grape.java:124)
    at groovy.grape.Grape$1.run(Grape.java:161)
    at groovy.grape.Grape$1.run(Grape.java:158)
    at java.base/java.security.AccessController.doPrivileged(AccessController.java:318)
    at groovy.grape.Grape.grab(Grape.java:158)
    at groovy.grape.GrabAnnotationTransformation.visit(GrabAnnotationTransformation.java:380)
    at org.codehaus.groovy.transform.ASTTransformationVisitor.lambda$addPhaseOperationsForGlobalTransforms$5(ASTTransformationVisitor.java:377)
    at org.codehaus.groovy.control.CompilationUnit$ISourceUnitOperation.doPhaseOperation(CompilationUnit.java:896)
    at org.codehaus.groovy.control.CompilationUnit.processPhaseOperations(CompilationUnit.java:692)
    at org.codehaus.groovy.control.CompilationUnit.compile(CompilationUnit.java:666)
    at groovy.lang.GroovyClassLoader.doParseClass(GroovyClassLoader.java:373)
    at groovy.lang.GroovyClassLoader.lambda$parseClass$2(GroovyClassLoader.java:316)
    at org.codehaus.groovy.runtime.memoize.StampedCommonCache.compute(StampedCommonCache.java:163)
    at org.codehaus.groovy.runtime.memoize.StampedCommonCache.getAndPut(StampedCommonCache.java:154)
    at groovy.lang.GroovyClassLoader.parseClass(GroovyClassLoader.java:314)
    at groovy.lang.GroovyShell.parseClass(GroovyShell.java:572)
    at groovy.lang.GroovyShell.run(GroovyShell.java:392)
    at groovy.lang.GroovyShell.run(GroovyShell.java:382)
    at groovy.ui.GroovyMain.processOnce(GroovyMain.java:649)
    at groovy.ui.GroovyMain.run(GroovyMain.java:389)
    at groovy.ui.GroovyMain.access$1400(GroovyMain.java:67)
    at groovy.ui.GroovyMain$GroovyCommand.process(GroovyMain.java:313)
    at groovy.ui.GroovyMain.processArgs(GroovyMain.java:141)
    at groovy.ui.GroovyMain.main(GroovyMain.java:114)
    at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:104)
    at java.base/java.lang.reflect.Method.invoke(Method.java:578)
    at org.codehaus.groovy.tools.GroovyStarter.rootLoader(GroovyStarter.java:109)
    at org.codehaus.groovy.tools.GroovyStarter.main(GroovyStarter.java:132)
Caused by: java.lang.ClassNotFoundException: org.apache.ivy.util.MessageLogger
    at java.base/jdk.internal.loader.BuiltinClassLoader.loadClass(BuiltinClassLoader.java:641)
    at java.base/jdk.internal.loader.ClassLoaders$AppClassLoader.loadClass(ClassLoaders.java:188)
    at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:521)
    ... 31 more
```

全然良くわからないんだが、 `Grape` 機能が使えないようだ。

`org.apache.ivy.util.MessageLogger` クラスが見つからないらしい。
というか、 `pantsbuild/ivy` が `archived` になっとるーーｗ

...というのは多分関係ない。

以下のように修正しても、ダメっぽかった。

``` groovy
@Grab(group='org.apache.ivy', module='ivy', version='2.5.1')
@Grab(group='org.openjfx', module='javafx-base', version='19')
import javafx.application.Application
```

`@Grab` を使う時に `ivy` を使うため、 `ivy` の `MessageLogger`
クラスが見つからないので多分ダメなのだろう。

``` groovy
@Grab(group='org.apche.commons', module='commons-lang3', version='3.1')
import org.apache.commons.lang3.StringUtils

println StringUtils.join( args, ', ' )
```

もちろん、このコードでも同じ。

``` groovy
@GrabConfig(systemClassLoader=true)
@Grab(group='org.openjfx', module='javafx-base', version='19')
import javafx.application.Application
```
