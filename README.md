# sbt-fresh #

sbt-fresh is a plugin for sbt to scaffold an opinionated fresh sbt project: it
creates an sbt build according to established best practices, creates a useful
package object for the root package, initializes a Git repository, creates an
initial commit, etc.

Notice: The build definition created by sbt-fresh is incompatible with the
-Yno-adapted-args scalac option.

Add sbt-fresh to your global plugins definition, which most probably resides
under `~/.sbt/0.13/plugins/plugins.sbt`:

``` scala
addSbtPlugin("de.heikoseeberger" % "sbt-fresh" % "2.3.0")
```

You can define the following settings in your global build definition, which
most probably sits at `~/.sbt/0.13/build.sbt`:

``` scala
import de.heikoseeberger.sbtfresh.FreshPlugin.autoImport._
import de.heikoseeberger.sbtfresh.license.License

freshOrganization := "doe.john"        // Organization – "default" by default
freshAuthor       := "John Doe"        // Author – value of "user.name" system property or "default" by default
freshLicense      := Some(License.mit) // Optional license – `apache20` by default
freshSetUpGit     := true              // Initialize a Git repo and create an initial commit – `true` by default
```

Other settings which probably shouldn't be set globally:

``` scala
freshName := ??? // Name – name of build directory by default; doesn't make much sense as a permanent setting

```

In order to scaffold a fresh sbt project, just start sbt in an empty directory.
Then call the `fresh` command, optionally passing one or more of the following
arguments (hit tab for auto completion) which override the respective settings:

- `organization`
- `name`
- `author`
- `license`
- `setUpGit`

Example:

```
sbt> fresh license=bsd3 setUpGit=false
```

The following values are available for the license argument:
- `apache20`
- `bsd2`
- `bsd3`
- `gpl3`
- `mit`

## Layout

sbt-fresh creates a project with the following layout:

```
+ .gitignore
+ .scalafmt.conf
+ build.sbt                      // build settings
+ LICENSE                        // license file (Apache by default)
+ NOTICE
+ project
--+ AutomateScalafmtPlugin.scala // settings for scalafmt automation
--+ build.properties             // sbt version
--+ plugins.sbt                  // sbt-git, sbt-header, sbt-scalafmt
+ README.md
+ shell-prompt.sbt               // show project id
+ src
--+ main
----+ scala
------+ package.scala            // type aliases repointing `Seq` and friends to immutable
```

## Contribution policy ##

Contributions via GitHub pull requests are gladly accepted from their original
author. Along with any pull requests, please state that the contribution is your
original work and that you license the work to the project under the project's
open source license. Whether or not you state this explicitly, by submitting any
copyrighted material via pull request, email, or other means you agree to
license the material under the project's open source license and warrant that
you have the legal authority to do so.

## License ##

This code is open source software licensed under the
[Apache 2.0 License]("http://www.apache.org/licenses/LICENSE-2.0.html").
