# Run 
sbt 

# Dependency Syntax
如果你用是 groupID %% artifactID % revision 而不是 groupID % artifactID % revision（区别在于 groupID 后面是 %%），sbt 会在 工件名称中加上项目的 Scala 版本号。 这只是一种快捷方法。你可以这样写不用 %%：

libraryDependencies += "org.scala-tools" % "scala-stm_2.11.1" % "0.3"
假设这个构建的 scalaVersion 是 2.11.1，下面这种方式是等效的（注意 "org.scala-tools" 后面是 %%）：

libraryDependencies += "org.scala-tools" %% "scala-stm" % "0.3"
这个想法是很多依赖都会被编译给多个 Scala 版本，而你想确保和项目匹配的jar是二进制兼容的。

实践中的复杂度在于通常一个依赖会和稍微不同的 Scala 版本一起工作；但是 %% 就没有那么智能了。所以如果一个依赖要求版本为 2.10.1，但是你使用的 scalaVersion := "2.10.4"， 你无法使用 %% 方法即使 2.10.1 的版本很可能也可以工作。如果 %% 无法达到目的，只需要去检查那个依赖是基于哪个 Scala 版本构建的，然后硬编码你认为可以工作的版本号（假设已经有一个）。
