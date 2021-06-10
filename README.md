# Introduction

Minimal reproduction repo for the Renovate issue.

## Current behavior

The exception will be thrown during lock file update because "My Package Source" contains whitespaces:

```log
DEBUG: nuget.updateArtifacts(src/Functions/Functions.csproj) (repository=ONE/poc-renovate, branch=renovate/patch-.net-core-3.x)
DEBUG: found NuGet.config (repository=ONE/poc-renovate, branch=renovate/patch-.net-core-3.x)
       "nuGetConfigPath": "/tmp/renovate/repos/azure/ONE/poc-renovate/src/NuGet.Config"
DEBUG: clearing registry URLs (repository=ONE/poc-renovate, branch=renovate/patch-.net-core-3.x)
DEBUG: adding registry URL (repository=ONE/poc-renovate, branch=renovate/patch-.net-core-3.x)
       "registryUrl": "https://api.nuget.org/v3/index.json#protocolVersion=3"
DEBUG: adding registry URL (repository=ONE/poc-renovate, branch=renovate/patch-.net-core-3.x)
       "registryUrl": "https://my.myget.org/F/my/auth/guid/api/v3/index.json"
DEBUG: dotnet command (repository=ONE/poc-renovate, branch=renovate/patch-.net-core-3.x)
       "cmd": [
         "dotnet nuget add source https://api.nuget.org/v3/index.json --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config --name nuget.org",
         "dotnet nuget add source https://my.myget.org/F/my/auth/guid/api/v3/index.json --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config --name My Package Source",
         "dotnet restore src/Functions/Functions.csproj --force-evaluate --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config"
       ]
DEBUG: Executing command (repository=ONE/poc-renovate, branch=renovate/patch-.net-core-3.x)
       "command": "dotnet nuget add source https://api.nuget.org/v3/index.json --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config --name nuget.org"
DEBUG: exec completed (repository=ONE/poc-renovate, branch=renovate/patch-.net-core-3.x)
       "cmd": "dotnet nuget add source https://api.nuget.org/v3/index.json --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config --name nuget.org",
       "durationMs": 252,
       "stdout": "Package source with Name: nuget.org added successfully.\n",
       "stderr": ""
DEBUG: Executing command (repository=ONE/poc-renovate, branch=renovate/patch-.net-core-3.x)
       "command": "dotnet nuget add source https://my.myget.org/F/my/auth/guid/api/v3/index.json --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config --name My Package Source"
DEBUG: rawExec err (repository=ONE/poc-renovate, branch=renovate/patch-.net-core-3.x)
       "err": {
         "killed": false,
         "code": 1,
         "signal": null,
         "cmd": "dotnet nuget add source https://my.myget.org/F/my/auth/guid/api/v3/index.json --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config --name My Package Source",
         "stdout": "Specify --help for a list of available options and commands.\nerror: Unrecognized command or argument 'Package'\n\n\nUsage: dotnet nuget add source [arguments] [options]\n\nArguments:\n  PackageSourcePath  Path to the package source.\n\nOptions:\n  -n|--name                       Name of the source.\n  -u|--username                   Username to be used when connecting to an authenticated source.\n  -p|--password                   Password to be used when connecting to an authenticated source.\n  --store-password-in-clear-text  Enables storing portable package source credentials by disabling password encryption.\n  --valid-authentication-types    Comma-separated list of valid authentication types for this source. Set this to basic if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server. Other valid values include negotiate, kerberos, ntlm, and digest, but these values are unlikely to be useful.\n  --configfile                    The NuGet configuration file. If specified, only the settings from this file will be used. If not specified, the hierarchy of configuration files from the current directory will be used. For more information, see https://docs.microsoft.com/nuget/consume-packages/configuring-nuget-behavior.\n  -h|--help                       Show help information\n",
         "stderr": "",
         "message": "Command failed: dotnet nuget add source https://my.myget.org/F/my/auth/guid/api/v3/index.json --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config --name My Package Source\n",
         "stack": "Error: Command failed: dotnet nuget add source https://my.myget.org/F/my/auth/guid/api/v3/index.json --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config --name My Package Source\n\n    at ChildProcess.exithandler (child_process.js:319:12)\n    at ChildProcess.emit (events.js:376:20)\n    at ChildProcess.emit (domain.js:470:12)\n    at maybeClose (internal/child_process.js:1055:16)\n    at Process.ChildProcess._handle.onexit (internal/child_process.js:288:5)"
       }
DEBUG: Failed to generate lock file (repository=ONE/poc-renovate, branch=renovate/patch-.net-core-3.x)
       "err": {
         "killed": false,
         "code": 1,
         "signal": null,
         "cmd": "dotnet nuget add source https://my.myget.org/F/my/auth/guid/api/v3/index.json --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config --name My Package Source",
         "stdout": "Specify --help for a list of available options and commands.\nerror: Unrecognized command or argument 'Package'\n\n\nUsage: dotnet nuget add source [arguments] [options]\n\nArguments:\n  PackageSourcePath  Path to the package source.\n\nOptions:\n  -n|--name                       Name of the source.\n  -u|--username                   Username to be used when connecting to an authenticated source.\n  -p|--password                   Password to be used when connecting to an authenticated source.\n  --store-password-in-clear-text  Enables storing portable package source credentials by disabling password encryption.\n  --valid-authentication-types    Comma-separated list of valid authentication types for this source. Set this to basic if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server. Other valid values include negotiate, kerberos, ntlm, and digest, but these values are unlikely to be useful.\n  --configfile                    The NuGet configuration file. If specified, only the settings from this file will be used. If not specified, the hierarchy of configuration files from the current directory will be used. For more information, see https://docs.microsoft.com/nuget/consume-packages/configuring-nuget-behavior.\n  -h|--help                       Show help information\n",
         "stderr": "",
         "message": "Command failed: dotnet nuget add source https://my.myget.org/F/my/auth/guid/api/v3/index.json --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config --name My Package Source\n",
         "stack": "Error: Command failed: dotnet nuget add source https://my.myget.org/F/my/auth/guid/api/v3/index.json --configfile /tmp/renovate/cache/others/nuget/95b70eaa518ea942/nuget.config --name My Package Source\n\n    at ChildProcess.exithandler (child_process.js:319:12)\n    at ChildProcess.emit (events.js:376:20)\n    at ChildProcess.emit (domain.js:470:12)\n    at maybeClose (internal/child_process.js:1055:16)\n    at Process.ChildProcess._handle.onexit (internal/child_process.js:288:5)"
       }
```

## Expected behavior

No exception is thrown.
