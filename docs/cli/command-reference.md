toyhauler-cli
=============

Local interface for registering and maintaining Toyhauler assets and pipelines

[![oclif](https://img.shields.io/badge/cli-oclif-brightgreen.svg)](https://oclif.io)
[![Version](https://img.shields.io/npm/v/toyhauler-cli.svg)](https://npmjs.org/package/toyhauler-cli)
[![Downloads/week](https://img.shields.io/npm/dw/toyhauler-cli.svg)](https://npmjs.org/package/toyhauler-cli)
[![License](https://img.shields.io/npm/l/toyhauler-cli.svg)](https://github.com/mfreydl/toyhauler-cli/blob/master/package.json)

<!-- toc -->
* [Usage](#usage)
* [Commands](#commands)
<!-- tocstop -->
# Usage
<!-- usage -->
```sh-session
$ npm install -g codiac-cli
$ codiac COMMAND
running command...
$ codiac (-v|--version|version)
codiac-cli/0.0.8-0 darwin-x64 node-v10.15.0
$ codiac --help [COMMAND]
USAGE
  $ codiac COMMAND
...
```
<!-- usagestop -->
# Commands
<!-- commands -->
* [`codiac adhoc [FILE]`](#codiac-adhoc-file)
* [`codiac api:client:create`](#codiac-apiclientcreate)
* [`codiac asset:create [SETTING]`](#codiac-assetcreate-setting)
* [`codiac asset:destroy`](#codiac-assetdestroy)
* [`codiac branch [NAME]`](#codiac-branch-name)
* [`codiac branch:current`](#codiac-branchcurrent)
* [`codiac branch:list`](#codiac-branchlist)
* [`codiac build`](#codiac-build)
* [`codiac cabinet:create CABINET`](#codiac-cabinetcreate-cabinet)
* [`codiac cabinet:obliterate [CABINET]`](#codiac-cabinetobliterate-cabinet)
* [`codiac cli`](#codiac-cli)
* [`codiac commit [MESSAGE]`](#codiac-commit-message)
* [`codiac config:add [SETTING]`](#codiac-configadd-setting)
* [`codiac config:delete [SETTING]`](#codiac-configdelete-setting)
* [`codiac config:view [SETTING]`](#codiac-configview-setting)
* [`codiac dep [NAME]`](#codiac-dep-name)
* [`codiac dep:create [URL]`](#codiac-depcreate-url)
* [`codiac dep:install`](#codiac-depinstall)
* [`codiac dep:list`](#codiac-deplist)
* [`codiac dep:remove [NAME]`](#codiac-depremove-name)
* [`codiac dep:source [NAME]`](#codiac-depsource-name)
* [`codiac dep:syncup [DEPENDENCY]`](#codiac-depsyncup-dependency)
* [`codiac dep:unsource [NAME]`](#codiac-depunsource-name)
* [`codiac dep:upgrade [DEPENDENCY]`](#codiac-depupgrade-dependency)
* [`codiac deploy`](#codiac-deploy)
* [`codiac env:add [SETTING]`](#codiac-envadd-setting)
* [`codiac hello [FILE]`](#codiac-hello-file)
* [`codiac help [COMMAND]`](#codiac-help-command)
* [`codiac identity [TOKENNAME]`](#codiac-identity-tokenname)
* [`codiac identity:delete [NAME]`](#codiac-identitydelete-name)
* [`codiac identity:list`](#codiac-identitylist)
* [`codiac images:add IMAGENAME`](#codiac-imagesadd-imagename)
* [`codiac images:list [HELLO]`](#codiac-imageslist-hello)
* [`codiac images:patch IMAGENAME`](#codiac-imagespatch-imagename)
* [`codiac images:remove IMAGENAME`](#codiac-imagesremove-imagename)
* [`codiac init DIRECTORY`](#codiac-init-directory)
* [`codiac login`](#codiac-login)
* [`codiac merge [BRANCH]`](#codiac-merge-branch)
* [`codiac noc:cluster:create [NAME]`](#codiac-nocclustercreate-name)
* [`codiac noc:cluster:deinit [FILE]`](#codiac-nocclusterdeinit-file)
* [`codiac noc:cluster:destroy [NAME]`](#codiac-nocclusterdestroy-name)
* [`codiac noc:cluster:init [NAME]`](#codiac-nocclusterinit-name)
* [`codiac pkg:add [DEFINITIONFILE]`](#codiac-pkgadd-definitionfile)
* [`codiac pkg:list [HELLO]`](#codiac-pkglist-hello)
* [`codiac pkg:patch PACKAGENAME`](#codiac-pkgpatch-packagename)
* [`codiac pkg:remove [PACKAGENAME]`](#codiac-pkgremove-packagename)
* [`codiac publish [NAME]`](#codiac-publish-name)
* [`codiac pull [NAME]`](#codiac-pull-name)
* [`codiac push [NAME]`](#codiac-push-name)
* [`codiac run`](#codiac-run)
* [`codiac stage [FILES]`](#codiac-stage-files)
* [`codiac stash [FILE]`](#codiac-stash-file)
* [`codiac status`](#codiac-status)
* [`codiac stop`](#codiac-stop)
* [`codiac switch [NAME]`](#codiac-switch-name)
* [`codiac sync [NAME]`](#codiac-sync-name)
* [`codiac unstage [FILES]`](#codiac-unstage-files)
* [`codiac view:dashboard`](#codiac-viewdashboard)
* [`codiac view:pods`](#codiac-viewpods)
* [`codiac view:services`](#codiac-viewservices)
* [`codiac whereami [FILE]`](#codiac-whereami-file)
* [`codiac whoami`](#codiac-whoami)

## `codiac adhoc [FILE]`

describe the command here

```
USAGE
  $ codiac adhoc [FILE]

OPTIONS
  -f, --force
  -h, --help       show CLI help
  -n, --name=name  name to print
```

_See code: [src/commands/adhoc.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/adhoc.ts)_

## `codiac api:client:create`

describe the command here

```
USAGE
  $ codiac api:client:create

OPTIONS
  -h, --help  show CLI help
```

## `codiac asset:create [SETTING]`

Creates a new asset in the given enterprise from an image that exists in a container registry.

```
USAGE
  $ codiac asset:create [SETTING]

ARGUMENTS
  SETTING  The key for the config setting to add

OPTIONS
  -c, --code=code              The host name to assign this asset in the domain url.  eg: 'myasset' in
                               'myasset.your-domain.com' (Optional: defaults to the asset name).

  -e, --enterprise=enterprise  The name of the enterprise in which to create this asset. (defaults to the current
                               enterprise context)

  -g, --hasIngress             Declaration that the asset service is to be externally accessible (optional: defaults to
                               false).

  -h, --help                   show CLI help

  -i, --image=image            The image name including scope prefix if applicable (eg: '@yourCompany/your-api-image').

  -n, --name=name              The name to give the enterprise asset (Optional: defaults to the image name without the
                               scope prefix).

  -o, --routedWithoutName      Declaration that the asset service is to be externally accessible (optional: defaults to
                               false).

  -p, --port=port              The default port to assign the asset when deployed to a cabinet (optional).

  -r, --registry=registry      The container registry in which the image exists (defaults to docker hub).

ALIASES
  $ codiac asset:new
```

_See code: [src/commands/asset/create.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/asset/create.ts)_

## `codiac asset:destroy`

Deploys a given asset to a given cabinet.  Defaults to current version.

```
USAGE
  $ codiac asset:destroy

OPTIONS
  -a, --asset=asset      Search string for the name of the asset to destroy (use ? to be prompted).
  -h, --help             show CLI help

  -s, --scorch           (Optional: defaults to false) Destroys the service too, instead of just the deployment and
                         pods.

  -v, --version=version  Search string for the version of the asset to destroy  (use ? to be prompted).

  -y, --silent           (Optional: defaults to false) Prevents confirmations of user-values that are remembered from
                         prior runs.
```

_See code: [src/commands/asset/destroy.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/asset/destroy.ts)_

## `codiac branch [NAME]`

Creates a new branch for the parent project and any sourced dependencies.

```
USAGE
  $ codiac branch [NAME]

ARGUMENTS
  NAME  The name of the branch to create.

OPTIONS
  -h, --help  show CLI help
```

_See code: [src/commands/branch.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/branch.ts)_

## `codiac branch:current`

Renders the name of the current branch (for the main project and for any sourced dependencies).

```
USAGE
  $ codiac branch:current

OPTIONS
  -h, --help  show CLI help

ALIASES
  $ codiac branches:current
```

_See code: [src/commands/branch/current.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/branch/current.ts)_

## `codiac branch:list`

Lists out existing branches for the project repo.

```
USAGE
  $ codiac branch:list

OPTIONS
  -h, --help     Displays the help document for this command.
  -l, --locals   (Optional, defaults to false) Limits to local branches only.
  -r, --remotes  (Optional, defaults to false) Limits to remote branches only.

ALIASES
  $ codiac branches:list
```

_See code: [src/commands/branch/list.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/branch/list.ts)_

## `codiac build`

Builds the project and the docker container

```
USAGE
  $ codiac build

OPTIONS
  -M, --major                              Increments the version by one Major version number (using Major.Minor.Patch).
  -c, --clear                              Completely deletes the output folder before building.

  -f, --frameworkVersion=frameworkVersion  (Future) Explicitly sets the version of the Toyhauler base image to use
                                           (default: latest).

  -h, --help                               show CLI help

  -m, --minor                              Increments the version by one Minor version number (using Major.Minor.Patch).

  -n, --noCache                            Ignores the local Docker image cache, thereby forcing a fresh download of
                                           each image from its container registry layer in the build.

  -p, --patch                              Increments the version by one Patch version number (using Major.Minor.Patch).

  -r, --prerelease                         Increments the prerelease number (using Major.Minor.Patch-PreRelease).  NOTE:
                                           Increments the Patch version number when appending.

  -s, --skip=(images|packages)             (optional) Prevents the building of any declared container images or
                                           packages.

  -v, --verbose                            Renders additional logging levels (detail, trace, and debug) to the console
                                           output.

  --as=as                                  Fires this command with an argument list that was previously remembered using
                                           the --rememberAs flag.

  --remember                               Saves the arguments, so they are invoked as defaults whenever this command
                                           gets called.

  --rememberAs=rememberAs                  Saves the given argument list so that it can be called by name.

  --unremember=unremember                  Administrative only: DOES NOT fire the actual command.  Simply clears the
                                           arguments that were previously stored under the given name (use "--unRemember
                                           default" to clear default argument list memorized with the --remember flag).

  --version=version                        Overwrites the full version for the build (using Major.Minor.Patch).

  --withoutdefaults                        Prevents any relevant saved defaults from being invoked for this call.
```

_See code: [src/commands/build.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/build.ts)_

## `codiac cabinet:create CABINET`

Initializes a cabinet for a given enterprise and environment.  Overwrites any existing if forced, otherwise returns an error if the cabinet already exists.

```
USAGE
  $ codiac cabinet:create CABINET

ARGUMENTS
  CABINET  The name of the cabinet to create

OPTIONS
  -e, --environment=environment  (optional: defaults to that of the current project branch) The name of the environment
                                 this cabinet will be grouped under.

  -f, --force                    Overwrites and reinitializes if the cabinet already exists.

  -h, --help                     show CLI help

  -v, --verbose                  Renders additional logging levels (detail, trace, and debug) to the console output.

  --as=as                        Fires this command with an argument list that was previously remembered using the
                                 --rememberAs flag.

  --remember                     Saves the arguments, so they are invoked as defaults whenever this command gets called.

  --rememberAs=rememberAs        Saves the given argument list so that it can be called by name.

  --unremember=unremember        Administrative only: DOES NOT fire the actual command.  Simply clears the arguments
                                 that were previously stored under the given name (use "--unRemember default" to clear
                                 default argument list memorized with the --remember flag).

  --withoutdefaults              Prevents any relevant saved defaults from being invoked for this call.

ALIASES
  $ codiac cab:create
```

_See code: [src/commands/cabinet/create.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/cabinet/create.ts)_

## `codiac cabinet:obliterate [CABINET]`

Hard-deletes an entire cabinet and everything in it; makes it as if the cabinet itself never existed.

```
USAGE
  $ codiac cabinet:obliterate [CABINET]

ARGUMENTS
  CABINET  The name of the cabinet

OPTIONS
  -e, --environment=environment  (optional: defaults to that of the current project branch) The name of the environment
                                 this cabinet will be grouped under.

  -h, --help                     show CLI help

  -v, --verbose                  Renders additional logging levels (detail, trace, and debug) to the console output.

  --as=as                        Fires this command with an argument list that was previously remembered using the
                                 --rememberAs flag.

  --remember                     Saves the arguments, so they are invoked as defaults whenever this command gets called.

  --rememberAs=rememberAs        Saves the given argument list so that it can be called by name.

  --unremember=unremember        Administrative only: DOES NOT fire the actual command.  Simply clears the arguments
                                 that were previously stored under the given name (use "--unRemember default" to clear
                                 default argument list memorized with the --remember flag).

  --withoutdefaults              Prevents any relevant saved defaults from being invoked for this call.

ALIASES
  $ codiac cab:obliterate
```

_See code: [src/commands/cabinet/obliterate.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/cabinet/obliterate.ts)_

## `codiac cli`

Applies settings to the Codiac CLI itself (scoped to the local machine).

```
USAGE
  $ codiac cli

OPTIONS
  -h, --help     Show the help docs for this command.

  -s, --set=set  A key=value expression for the setting to apply.  Leave this argument out of your call to get a list of
                 the available settings keys and their types.
```

_See code: [src/commands/cli.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/cli.ts)_

## `codiac commit [MESSAGE]`

Commits the currently staged changes on the current branch of the main project and on any sourced dependencies.

```
USAGE
  $ codiac commit [MESSAGE]

ARGUMENTS
  MESSAGE  The description to include in this particular commit.

OPTIONS
  -h, --help  show CLI help
```

_See code: [src/commands/commit.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/commit.ts)_

## `codiac config:add [SETTING]`

Adds a key value pair to the app config

```
USAGE
  $ codiac config:add [SETTING]

ARGUMENTS
  SETTING  The key for the config setting to add

OPTIONS
  -c, --cabinet=cabinet          The name of the cabinet to which this value is to apply.
  -e, --environment=environment  The name of the environment to which this value is to apply.

  -f, --file=file                The path-name to the file to which the settings are written, relative to the root of
                                 the Codiac project.

  -h, --help                     show CLI help

  -n, --enterprise=enterprise    The name of the enterprise to which this value is to apply.

  -s, --setting=setting          The config key (in dotpath/JSONPath), relative to the root of the config.

  -v, --value=value              The actual concrete data to be applied as the setting value.

ALIASES
  $ codiac cfg:add
```

_See code: [src/commands/config/add.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/config/add.ts)_

## `codiac config:delete [SETTING]`

Removes the given keys from the app config

```
USAGE
  $ codiac config:delete [SETTING]

ARGUMENTS
  SETTING  (optional) Specific config key to remove. Omit to select from a list. Enter "all" to clear the entire config.

OPTIONS
  -c, --cabinet=cabinet          The name of the cabinet to which this value is to apply.
  -e, --environment=environment  The name of the environment to which this value is to apply.

  -f, --file=file                The path-name to the config file holding the settings, relative to the root of the
                                 Codiac project.

  -h, --help                     show CLI help

  -n, --enterprise=enterprise    The name of the enterprise to which this value is to apply.

  -s, --setting=setting          The config key (in dotpath/JSONPath), relative to the root of the config.

ALIASES
  $ codiac cfg:delete
```

_See code: [src/commands/config/delete.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/config/delete.ts)_

## `codiac config:view [SETTING]`

Shows the values that are explicitly set in the given config

```
USAGE
  $ codiac config:view [SETTING]

ARGUMENTS
  SETTING  (optional) Name of specific setting value to view; omit to show all.

OPTIONS
  -c, --cabinet=cabinet  The name of the cabinet to assemble the configuration for.

  -f, --file=file        [default: app-config.json] The relative pathname of the config file to view (relative to the
                         root of the codiac project).

  -h, --help             show CLI help

  -p, --prompt           Invokes a prompt to select from the existing settings.

ALIASES
  $ codiac cfg:view

EXAMPLES
  $ thaul config:view
  $ thaul config:view port
  $ thaul config:view -p
```

_See code: [src/commands/config/view.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/config/view.ts)_

## `codiac dep [NAME]`

Installs a package into current project.

```
USAGE
  $ codiac dep [NAME]

ARGUMENTS
  NAME  The official unique name of the package to install.

OPTIONS
  -h, --help             show CLI help
  -v, --version=version  version of the package to install
```

_See code: [src/commands/dep.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/dep.ts)_

## `codiac dep:create [URL]`

Sources a new dependency into the project from an existing repo url, initializes it with the package repository, and publishes the initial version if it is not already.  If the package repository is already initialized, the latest package version is used.

```
USAGE
  $ codiac dep:create [URL]

ARGUMENTS
  URL  The official clone url for the repository.

OPTIONS
  -h, --help             show CLI help
  -v, --version=version  Version to apply to the dependency package if it has not yet been initialized.
```

_See code: [src/commands/dep/create.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/dep/create.ts)_

## `codiac dep:install`

installs any missing dependency packages into the local project folder.

```
USAGE
  $ codiac dep:install

OPTIONS
  -h, --help  show CLI help
```

_See code: [src/commands/dep/install.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/dep/install.ts)_

## `codiac dep:list`

Shows the dependencies for the project.

```
USAGE
  $ codiac dep:list

OPTIONS
  -h, --help  show CLI help
```

_See code: [src/commands/dep/list.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/dep/list.ts)_

## `codiac dep:remove [NAME]`

Removes a dependency from the project.

```
USAGE
  $ codiac dep:remove [NAME]

ARGUMENTS
  NAME  The official unique name of the dependency package.

OPTIONS
  -d, --discard  If the dependency to remove is sourced into the project, setting this flag discards all uncommitted
                 changes (staged and unstaged) before removing it.  Again, uncomitted changes are LOST when this flag is
                 set.

  -h, --help     show CLI help
```

_See code: [src/commands/dep/remove.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/dep/remove.ts)_

## `codiac dep:source [NAME]`

Loads the source code for the given dependency

```
USAGE
  $ codiac dep:source [NAME]

ARGUMENTS
  NAME  The official unique name of the dependency package.

OPTIONS
  -h, --help  show CLI help

ALIASES
  $ codiac dep:src
```

_See code: [src/commands/dep/source.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/dep/source.ts)_

## `codiac dep:syncup [DEPENDENCY]`

Publishes the dependency in its current state and upgrades to it in the main project.

```
USAGE
  $ codiac dep:syncup [DEPENDENCY]

ARGUMENTS
  DEPENDENCY  The package name of the dependency to sync up into the main project

OPTIONS
  -h, --help  show CLI help
```

_See code: [src/commands/dep/syncup.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/dep/syncup.ts)_

## `codiac dep:unsource [NAME]`

Exits source mode for the given dependency by physically removing its source code folder from the project, and points the project dependency back to the package version it previously depended on.

```
USAGE
  $ codiac dep:unsource [NAME]

ARGUMENTS
  NAME  The official unique name of the dependency package.

OPTIONS
  -c, --comment  The commit message for any outstanding changes.

  -d, --discard  Discards all uncommitted changes (staged and unstaged) before unsourcing, and goes back to the
                 previously installed version of the dependency.  Again, uncomitted changes are LOST when this flag is
                 set.

  -h, --help     show CLI help

ALIASES
  $ codiac dep:unsrc
```

_See code: [src/commands/dep/unsource.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/dep/unsource.ts)_

## `codiac dep:upgrade [DEPENDENCY]`

describe the command here

```
USAGE
  $ codiac dep:upgrade [DEPENDENCY]

ARGUMENTS
  DEPENDENCY  The dependency to upgrade

OPTIONS
  -h, --help             show CLI help
  -v, --version=version  version of the package to install
```

_See code: [src/commands/dep/upgrade.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/dep/upgrade.ts)_

## `codiac deploy`

Deploys a given asset to a given cabinet.  Defaults to current version.

```
USAGE
  $ codiac deploy

OPTIONS
  -a, --asset=asset      Search string for the name of the asset to deploy (use ? to be prompted).
  -h, --help             show CLI help
  -v, --version=version  Search string for the version of the asset to deploy  (use ? to be prompted).

  -y, --silent           (Optional: defaults to false) Prevents confirmations of user-values that are remembered from
                         prior runs.
```

_See code: [src/commands/deploy.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/deploy.ts)_

## `codiac env:add [SETTING]`

Adds a key value pair to the app config

```
USAGE
  $ codiac env:add [SETTING]

ARGUMENTS
  SETTING  The name of the environment variable to add

OPTIONS
  -c, --cabinet=cabinet          The name of the cabinet to which this value is to apply.
  -e, --environment=environment  The name of the environment to which this value is to apply.
  -h, --help                     show CLI help
  -n, --enterprise=enterprise    The name of the enterprise to which this value is to apply.
  -s, --setting=setting          The name of the environment variable to add.
  -v, --value=value              The actual concrete data to be applied as the setting value.
```

_See code: [src/commands/env/add.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/env/add.ts)_

## `codiac hello [FILE]`

describe the command here

```
USAGE
  $ codiac hello [FILE]

OPTIONS
  -f, --force
  -h, --help       show CLI help
  -n, --name=name  name to print

EXAMPLE
  $ oclif-example hello
  hello world from ./src/hello.ts!
```

## `codiac help [COMMAND]`

display help for codiac

```
USAGE
  $ codiac help [COMMAND]

ARGUMENTS
  COMMAND  command to show help for

OPTIONS
  --all  see all commands in CLI
```

_See code: [@oclif/plugin-help](https://github.com/oclif/plugin-help/blob/v2.2.3/src/commands/help.ts)_

## `codiac identity [TOKENNAME]`

Stores an identity token for the current user, for use with a component tool (such as npm).  This command acts as an upsert.

```
USAGE
  $ codiac identity [TOKENNAME]

ARGUMENTS
  TOKENNAME  (optional) Conventional name (token_for_[provider]_[scope]) for the tokenized identity.  This name will
             also be used for the build environment variable carrying the token.

OPTIONS
  -e, --email=email                 (Azure Artifacts [aka: azart] only) The email address for this identity.  Npm
                                    requires for this, but never uses it.

  -f, --feed=feed                   (Azure Artifacts [aka: azart] only) The human readable identifier for the package
                                    feed

  -g, --organization=organization   (Azure Artifacts [aka: azart] only) Human readable identifier for the organization
                                    account with the provider.

  -h, --help                        Renders the help document for this command.

  -p, --provider=(npm|azart|other)  [default: npm] The source of the token.

  -r, --registryUrl=registryUrl     The component tool that issued and can consume the token.

  -s, --scope=scope                 The subdivision within the registry for which this token is honored.

  -t, --token=token                 (required) The actual raw token string itself issued by the provider

ALIASES
  $ codiac identify
  $ codiac token
```

_See code: [src/commands/identity.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/identity.ts)_

## `codiac identity:delete [NAME]`

Removes an identity token from storage for the current user.

```
USAGE
  $ codiac identity:delete [NAME]

ARGUMENTS
  NAME  The name of the token to delete.  Use the 'identity:list' command to view the currently stored tokens.

OPTIONS
  -h, --help  Displays the help document for this command.

ALIASES
  $ codiac identity:remove
  $ codiac token:delete
  $ codiac token:remove
```

_See code: [src/commands/identity/delete.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/identity/delete.ts)_

## `codiac identity:list`

Lists out the identity tokens currently stored for the current user.

```
USAGE
  $ codiac identity:list

OPTIONS
  -h, --help                              Displays the help document for this command.
  -o, --output=(table|extended|json|csv)  [default: table] Format for the response data.

ALIASES
  $ codiac token:list
```

_See code: [src/commands/identity/list.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/identity/list.ts)_

## `codiac images:add IMAGENAME`

Configures a container image to be built and published by the project.

```
USAGE
  $ codiac images:add IMAGENAME

ARGUMENTS
  IMAGENAME  image name including, scope prefix. eg:  "your-company/your-image"

OPTIONS
  -e, --environment=environment
      (optional) Declaration that this registry shall be the target when publishing to the given environment.

  -f, --sourceFile=sourceFile
      Path and filename of the image definition file, relative to the thaul project root, (eg: "./Dockerfile").  If 
      omitted, the build will use an in-memory image definition auto-generated at build time.

  -h, --help
      show CLI help

  -i, --infoUrl=infoUrl
      (Optional) Address on the registry website or portal of the human-readable web page for the image.

  -p, --port=port
      Recommended port number to assign, in the toybox template, to an Asset defined by this image.

  -r, --registryUrl=registryUrl
      [default: https://index.docker.io/v1] (Optional, defaults to Docker Hub) Address of the container registry to which 
      the image will be published (without protocol prefix), eg: "yourimages.azurecr.io".  NOTE: This registry will be 
      used by the "thaul publish" command, whereas when running in "local" mode, images will instead be registered to the 
      built-in image registry on the local machine.  NOTE:  This url shall define the default publishing target, for use 
      when publishing for any environment, unless otherwise specified.

  -s, --password=password
      (optional) Password credential for the given registry.  WARNING!! these username/password credentials will be stored 
      in the thaul config file in this project, and therefore configuring username and password in this manner is not 
      recommended!

  -u, --username=username
      (optional) Login credential for the given registry.  WARNING!! these username/password credentials will be stored in 
      the thaul config file in this project, and therefore configuring username and password in this manner is not 
      recommended!

ALIASES
  $ codiac image
  $ codiac image:add
  $ codiac img
  $ codiac img:add
```

_See code: [src/commands/images/add.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/images/add.ts)_

## `codiac images:list [HELLO]`

Renders the list of container images that are configured as project exports.

```
USAGE
  $ codiac images:list [HELLO]

OPTIONS
  -h, --help                              show CLI help
  -o, --output=(table|extended|json|csv)  [default: table] Format for the response data.

ALIASES
  $ codiac image:list
  $ codiac img:list
```

_See code: [src/commands/images/list.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/images/list.ts)_

## `codiac images:patch IMAGENAME`

Applies the given values to an existing image export configuration.  Both registryUrl and environment act as filters to limit the operation.  That is, an upsert of registry targets is performed for the given image, based on the given registryUrl and/or environment.

```
USAGE
  $ codiac images:patch IMAGENAME

ARGUMENTS
  IMAGENAME  image name including, scope prefix. eg:  "your-company/your-image"

OPTIONS
  -h, --help         show CLI help

  -s, --set=set      Space-delimited list of key-value pairs tp apply with json-path on the left and the desired value
                     on the right.  (eg:  --set .targets.default.registryUrl=mystuff.azurecr.io)

  -u, --unset=unset  Space-delimited list of properties to clear, in json-path format.  (eg:  --unset .targets.default)

ALIASES
  $ codiac image:patch
  $ codiac img:patch
```

_See code: [src/commands/images/patch.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/images/patch.ts)_

## `codiac images:remove IMAGENAME`

Deletes the given image export from the configuration.

```
USAGE
  $ codiac images:remove IMAGENAME

ARGUMENTS
  IMAGENAME  image name including, scope prefix. eg:  "your-company/your-image"

OPTIONS
  -h, --help  show CLI help

ALIASES
  $ codiac image:remove
  $ codiac img:remove
  $ codiac image:delete
  $ codiac img:delete
```

_See code: [src/commands/images/remove.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/images/remove.ts)_

## `codiac init DIRECTORY`

Declares the given folder as a project root

```
USAGE
  $ codiac init DIRECTORY

ARGUMENTS
  DIRECTORY  Path to the desired project root, relative to current directory.

OPTIONS
  -c, --clone=clone              (Optional) The git repo from which to hydrate the project folder.
  -h, --help                     show CLI help
  -t, --projectType=projectType  (Optional) The type of Codiac project to scaffold.
```

_See code: [src/commands/init.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/init.ts)_

## `codiac login`

Dialog with user to authenticate under a tenant.

```
USAGE
  $ codiac login

OPTIONS
  -h, --help  show CLI help

ALIASES
  $ codiac user:login
```

_See code: [src/commands/login.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/login.ts)_

## `codiac merge [BRANCH]`

Merges the given branch into the current branch of the main project and on any sourced dependencies.

```
USAGE
  $ codiac merge [BRANCH]

ARGUMENTS
  BRANCH  The branch name to merge into the current one.

OPTIONS
  -c, --commit  Commits if merge succeeds.
  -h, --help    show CLI help
```

_See code: [src/commands/merge.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/merge.ts)_

## `codiac noc:cluster:create [NAME]`

describe the command here

```
USAGE
  $ codiac noc:cluster:create [NAME]

ARGUMENTS
  NAME  Proposed name of the cluster

OPTIONS
  -g, --resourceGroup=resourceGroup                The Azure resource group to create for the cluster.
  -h, --help                                       show CLI help

  -l, --location=location                          The short name of the azure data center in which the cliuster is to
                                                   reside.

  -n, --nodeSpec=nodeSpec                          The identifier for the type of VM to use for nodes in the cluster.

  -p, --owner=owner                                Tenant code of the private owner of the cluster

  -q, --nodeQty=nodeQty                            The starting node count with which to create the cluster.

  -s, --providerSubscription=providerSubscription  The Azure subscription Id under which to create the cluster.
```

_See code: [src/commands/noc/cluster/create.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/noc/cluster/create.ts)_

## `codiac noc:cluster:deinit [FILE]`

describe the command here

```
USAGE
  $ codiac noc:cluster:deinit [FILE]

OPTIONS
  -f, --force
  -h, --help       show CLI help
  -n, --name=name  name to print
```

_See code: [src/commands/noc/cluster/deinit.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/noc/cluster/deinit.ts)_

## `codiac noc:cluster:destroy [NAME]`

describe the command here

```
USAGE
  $ codiac noc:cluster:destroy [NAME]

ARGUMENTS
  NAME  Proposed name of the cluster

OPTIONS
  -h, --help            show CLI help

  -i, --deleteIdentity  (optional: defaults to false) Ensures that identity security account for the cluster shall also
                        be deleted after the cluster itself is destroyed.

  -n, --name=name       Name of the cluster.
```

_See code: [src/commands/noc/cluster/destroy.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/noc/cluster/destroy.ts)_

## `codiac noc:cluster:init [NAME]`

Post-create initialization for the cluster (installs the ingress controller service)

```
USAGE
  $ codiac noc:cluster:init [NAME]

ARGUMENTS
  NAME  Name of existing cluster to initialize.

OPTIONS
  -h, --help       show CLI help
  -n, --name=name  Name of the cluster.
```

_See code: [src/commands/noc/cluster/init.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/noc/cluster/init.ts)_

## `codiac pkg:add [DEFINITIONFILE]`

Configures a package to be built and published by the project.

```
USAGE
  $ codiac pkg:add [DEFINITIONFILE]

ARGUMENTS
  DEFINITIONFILE  Path and filename of the package definition file, relative to the codiac project root, (eg:
                  "./package.json")

OPTIONS
  -e, --environment=environment
      (optional) Declaration that this registry shall be the target when publishing to the given environment.

  -h, --help
      show CLI help

  -r, --registryUrl=registryUrl
      Address of the registry to which the package will be published (without protocol prefix), eg: 
      "yourpackages.azurecr.io".  NOTE: This registry will be used by the "codiac publish" command, whereas when running 
      in "local" mode, packages will instead be registered to the built-in package registry on the local machine.  NOTE:  
      This url shall define the default publishing target, for use when publishing for any environment, unless otherwise 
      specified.

  -s, --password=password
      (optional) Password credential for the given registry.  WARNING!! these username/password credentials will be stored 
      in the codiac config file in this project, and therefore configuring username and password in this manner is not 
      recommended!

  -u, --username=username
      (optional) Login credential for the given registry.  WARNING!! these username/password credentials will be stored in 
      the codiac config file in this project, and therefore configuring username and password in this manner is not 
      recommended!
```

_See code: [src/commands/pkg/add.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/pkg/add.ts)_

## `codiac pkg:list [HELLO]`

Renders the list of packages that are configured as project exports.

```
USAGE
  $ codiac pkg:list [HELLO]

OPTIONS
  -h, --help  show CLI help
```

_See code: [src/commands/pkg/list.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/pkg/list.ts)_

## `codiac pkg:patch PACKAGENAME`

Applies the given values to an existing package export configuration.  Both registryUrl and environment act as filters to limit the operation.  That is, an upsert of registry targets is performed for the given package, based on the given registryUrl and/or environment.

```
USAGE
  $ codiac pkg:patch PACKAGENAME

ARGUMENTS
  PACKAGENAME  package name including, scope prefix. eg:  "your-company/your-package"

OPTIONS
  -h, --help         show CLI help

  -s, --set=set      Space-delimited list of key-value pairs tp apply with json-path on the left and the desired value
                     on the right.  (eg:  --set .targets.default.registryUrl=mystuff.azurecr.io)

  -u, --unset=unset  Space-delimited list of properties to clear, in json-path format.  (eg:  --unset .targets.default)
```

_See code: [src/commands/pkg/patch.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/pkg/patch.ts)_

## `codiac pkg:remove [PACKAGENAME]`

Deletes the given package export from the configuration.

```
USAGE
  $ codiac pkg:remove [PACKAGENAME]

ARGUMENTS
  PACKAGENAME  package name including, scope prefix. eg:  "your-company/your-package"

OPTIONS
  -h, --help  show CLI help

ALIASES
  $ codiac pkg:delete
```

_See code: [src/commands/pkg/remove.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/pkg/remove.ts)_

## `codiac publish [NAME]`

Publishes the exports (packages and images) declared in the codiac.json.

```
USAGE
  $ codiac publish [NAME]

ARGUMENTS
  NAME  The official unique name of a currently sourced dependency.  Applies the command to ONLY this sourced
        dependency.

OPTIONS
  -h, --help         show CLI help
  -i, --includeDeps  Also performs the operation on any currently source dependencies.

  -l, --local        Publishes to the local built-in image registry.  NOTE: this setting gets remembered and is used for
                     subsequent calls unless otherwise specified.

  -o, --only         Applies the command only the sourced dependencies selected from a prompt. Quits if no dependencies
                     are currently sourced.

  -r, --remote       Publishes to the remote image registry.  NOTE: this setting gets remembered and is used for
                     subsequent calls unless otherwise specified.
```

_See code: [src/commands/publish.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/publish.ts)_

## `codiac pull [NAME]`

Pulls all commits from upstream to local.

```
USAGE
  $ codiac pull [NAME]

ARGUMENTS
  NAME  The official unique name of a currently sourced dependency.  Applies the command to ONLY this sourced
        dependency.

OPTIONS
  -h, --help         show CLI help
  -i, --includeDeps  Also performs the operation on any currently source dependencies.

  -o, --only         Applies the command only the sourced dependencies selected from a prompt. Quits if no dependencies
                     are currently sourced.
```

_See code: [src/commands/pull.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/pull.ts)_

## `codiac push [NAME]`

Pushes all local commits upstream.

```
USAGE
  $ codiac push [NAME]

ARGUMENTS
  NAME  The official unique name of a currently sourced dependency.  Applies the command to ONLY this sourced
        dependency.

OPTIONS
  -h, --help         show CLI help
  -i, --includeDeps  Also performs the operation on any currently source dependencies.

  -o, --only         Applies the command only the sourced dependencies selected from a prompt. Quits if no dependencies
                     are currently sourced.
```

_See code: [src/commands/push.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/push.ts)_

## `codiac run`

Runs the latest build of the api container locally.

```
USAGE
  $ codiac run

OPTIONS
  -b, --build                  Triggers a new local build beforehand.
  -d, --detach                 Run container in background and print the container ID.
  -e, --entrypoint=entrypoint  Overrides the default container startup command.
  -h, --help                   Renders the help document for this command.

  -i, --interactive            Run the container interactively (in the console; dies with the console).  Use
                               -e|--entrypoint to override the startup command for the container.

  -n, --network=network        The docker network to which the container will be attached (defaults to a network named
                               as the company code, which will be created on demand as a bridge network).

  -p, --port=port              (default: 5775) Sets the external port to open on the container.  That is, the port on
                               which the api will be listening to calls from outside the container.

  -v, --verbose                Renders additional logging levels (detail, trace, and debug) to the console output.

  -w, --watch                  Forces a detach run and follows log output from the container.

  --as=as                      Fires this command with an argument list that was previously remembered using the
                               --rememberAs flag.

  --remember                   Saves the arguments, so they are invoked as defaults whenever this command gets called.

  --rememberAs=rememberAs      Saves the given argument list so that it can be called by name.

  --unremember=unremember      Administrative only: DOES NOT fire the actual command.  Simply clears the arguments that
                               were previously stored under the given name (use "--unRemember default" to clear default
                               argument list memorized with the --remember flag).

  --withoutdefaults            Prevents any relevant saved defaults from being invoked for this call.
```

_See code: [src/commands/run.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/run.ts)_

## `codiac stage [FILES]`

Flags files to be included in the next commit.

```
USAGE
  $ codiac stage [FILES]

ARGUMENTS
  FILES  Space-separated list of files to stage. Paths are relative to the main project root.

OPTIONS
  -A, --all             Include all modified files.
  -c, --commit=message  Commit the staged changes using the given message
  -h, --help            show CLI help
```

_See code: [src/commands/stage.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/stage.ts)_

## `codiac stash [FILE]`

describe the command here

```
USAGE
  $ codiac stash [FILE]

OPTIONS
  -f, --force
  -h, --help       show CLI help
  -n, --name=name  name to print
```

_See code: [src/commands/stash.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/stash.ts)_

## `codiac status`

Shows the current uncommitted changes in the current branch.

```
USAGE
  $ codiac status

OPTIONS
  -h, --help      show CLI help
  -s, --staged    Include the list of staged changes.
  -u, --unstaged  Include the list of unstaged changes.
```

_See code: [src/commands/status.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/status.ts)_

## `codiac stop`

Stops the api container

```
USAGE
  $ codiac stop

OPTIONS
  -h, --help    show CLI help
  -r, --remove  Deletes the container after stopping it
```

_See code: [src/commands/stop.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/stop.ts)_

## `codiac switch [NAME]`

Changes branch on the main project and any sourced dependencies.

```
USAGE
  $ codiac switch [NAME]

ARGUMENTS
  NAME  The name of the branch to switch to (Optional: will prompt the user when missing).

OPTIONS
  -h, --help  show CLI help
```

_See code: [src/commands/switch.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/switch.ts)_

## `codiac sync [NAME]`

Merges the given branch into the current branch.

```
USAGE
  $ codiac sync [NAME]

ARGUMENTS
  NAME  The official unique name of a currently sourced dependency.  Applies the command to ONLY this sourced
        dependency.

OPTIONS
  -b, --with=with    (required) Branch to merge into this one
  -h, --help         show CLI help
  -i, --includeDeps  Also performs the operation on any currently source dependencies.

  -o, --only         Applies the command only the sourced dependencies selected from a prompt. Quits if no dependencies
                     are currently sourced.
```

_See code: [src/commands/sync.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/sync.ts)_

## `codiac unstage [FILES]`

Flags files to be included in the next commit.

```
USAGE
  $ codiac unstage [FILES]

ARGUMENTS
  FILES  Space-separated list of files to stage. Paths are relative to the main project root.

OPTIONS
  -A, --all   Include all modified files.
  -h, --help  show CLI help
```

_See code: [src/commands/unstage.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/unstage.ts)_

## `codiac view:dashboard`

Spins up the dashboard for a given cabinet

```
USAGE
  $ codiac view:dashboard

OPTIONS
  -h, --help  show CLI help

ALIASES
  $ codiac view:dash
  $ codiac dash
```

_See code: [src/commands/view/dashboard.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/view/dashboard.ts)_

## `codiac view:pods`

Spins up the k9s cli pod viewer

```
USAGE
  $ codiac view:pods

OPTIONS
  -h, --help  show CLI help

ALIASES
  $ codiac view:k9s
  $ codiac k9s
```

_See code: [src/commands/view/pods.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/view/pods.ts)_

## `codiac view:services`

View pods, deployments, services, and namespaces of one or all image assets.

```
USAGE
  $ codiac view:services

OPTIONS
  -c, --component=component  View info for a single image asset.
  -h, --help                 show CLI help
```

_See code: [src/commands/view/services.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/view/services.ts)_

## `codiac whereami [FILE]`

Redners the current cabinet context the image project is pointed to.  ie:  Tenant, Enterprise, Environment, Cabinet.

```
USAGE
  $ codiac whereami [FILE]

OPTIONS
  -f, --force
  -h, --help       show CLI help
  -n, --name=name  name to print
```

_See code: [src/commands/whereami.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/whereami.ts)_

## `codiac whoami`

Renders the codiac username and its current tenant.

```
USAGE
  $ codiac whoami

OPTIONS
  -h, --help                show CLI help
  -o, --output=(text|json)  [default: text] Format for the response data.

ALIASES
  $ codiac user:show
```

_See code: [src/commands/whoami.ts](https://github.com/codiac/codiac-cli/blob/v0.0.8-0/src/commands/whoami.ts)_
<!-- commandsstop -->
