# Live Values & Results for Terraform

[Polski](README.pl.md) · [Release history](CHANGELOG.md)

See the values your Terraform code produces while you edit it. Select an expression or place the cursor in it to inspect the result in VS Code, including changes you have not saved.

The preview covers variables, locals, function calls, collection transformations, local-module outputs and configured resource arguments. It uses your code and selected inputs. You can check a `for` filter, follow a value through modules or inspect arguments for a `for_each` instance without adding a debug output or running a plan.

Current release: **0.0.12**. The extension ID is `valuescope.valuescope-iac`; settings use the `valuescope.*` prefix.

Author: **Michal 'bryn1u' Bryniarski** · [michal.bryniarski@gmail.com](mailto:michal.bryniarski@gmail.com).

## Start with a value

1. In VS Code, run **Extensions: Install from VSIX…** and choose the package for your system from the table below. Reload the window after updating.
2. Open the folder containing your Terraform configuration.
3. If your inputs are in a file such as `environment/prod.tfvars`, choose it with **tfvars file** in the results panel.
4. Place the cursor in an expression and press **Ctrl+Alt+V** (**Cmd+Alt+V** on macOS). You can also select an expression, hover over it or click **Preview** above a supported block.

The panel follows your selection. Pin a result to keep inspecting the same source while you move through the code. You can resize the panel, wrap long values and copy the displayed result.

The package includes the calculation engine. Using it requires VS Code 1.90 or later; Go, Node.js and Terraform CLI are not needed. Match the package to the operating system and architecture of your VS Code installation.

| System / VS Code architecture | Package |
|---|---|
| Linux x64 | [valuescope-iac-0.0.12-linux-x64.vsix](https://github.com/bryn1u/live-values-results-for-terraform/raw/refs/tags/v0.0.12/downloads/v0.0.12/valuescope-iac-0.0.12-linux-x64.vsix) |
| Windows x64 | [valuescope-iac-0.0.12-win32-x64.vsix](https://github.com/bryn1u/live-values-results-for-terraform/raw/refs/tags/v0.0.12/downloads/v0.0.12/valuescope-iac-0.0.12-win32-x64.vsix) |
| macOS Apple Silicon (ARM64) | [valuescope-iac-0.0.12-darwin-arm64.vsix](https://github.com/bryn1u/live-values-results-for-terraform/raw/refs/tags/v0.0.12/downloads/v0.0.12/valuescope-iac-0.0.12-darwin-arm64.vsix) |
| macOS Intel (x64) | [valuescope-iac-0.0.12-darwin-x64.vsix](https://github.com/bryn1u/live-values-results-for-terraform/raw/refs/tags/v0.0.12/downloads/v0.0.12/valuescope-iac-0.0.12-darwin-x64.vsix) |

[SHA-256 checksums](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/downloads/v0.0.12/SHA256SUMS.txt) are available for all four packages. macOS requires version 13 or later.

All four packages include the variable declaration preview fix. Version 0.0.12 passed VS Code integration tests on Linux. Windows and macOS packages are cross-compiled with archive checks; this release has not been run on those systems.

**Linux:** an exhausted `inotify` limit can leave previews showing old values after files change on disk. If your limit is 128, consider increasing it to 1024 on a busy development machine. See [Linux: inotify](#linux-inotify) for the explanation and commands.

## Demo videos

Both walkthroughs go from the simplest examples to more complex Terraform configurations: variables and locals, collection functions, resource instances, then module outputs. Click markers show where to look, and a border highlights the result. Each recording is about seven minutes long, with captions and no voice-over.

[![English walkthrough](https://raw.githubusercontent.com/bryn1u/live-values-results-for-terraform/main/media/thumbnail-en.png)](https://github.com/bryn1u/live-values-results-for-terraform/raw/refs/heads/main/media/demo-en-1080p.mp4)

[Watch in English](https://github.com/bryn1u/live-values-results-for-terraform/raw/refs/heads/main/media/demo-en-1080p.mp4) · [English video description](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/demo-video.en.md)

[Watch in Polish](https://github.com/bryn1u/live-values-results-for-terraform/raw/refs/heads/main/media/demo-pl-1080p.mp4) · [Polish video description](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/demo-video.pl.md)

The recordings show version 0.0.11. The packages above contain version 0.0.12.

## An example

```hcl
variable "routes" {
  default = {
    internet = { enabled = true,  prefix = "0.0.0.0/0" }
    internal = { enabled = false, prefix = "10.0.0.0/8" }
  }
}

locals {
  enabled_routes = {
    for name, route in var.routes :
    name => route
    if route.enabled
  }
}
```

Inspect `local.enabled_routes`. The result contains `internet`; the filter removes `internal`. Change an `enabled` flag and inspect it again. The next calculation uses the current editor buffer, even before you save.

The same workflow works for supported calls such as `merge`, `flatten`, `concat` and `zipmap`. For repeated resources, choose an instance to inspect its `each.key`, `each.value` or `count.index`.

## What a preview contains

| Where you open it | What you see |
|---|---|
| Expression, variable, local or selection | The calculated value, its type and any unresolved parts |
| Resource or data block header | Arguments written in the configuration, calculated for the selected inputs and instances, plus supported nested and `dynamic` blocks |
| Module header | Its existing outputs, including configured arguments of resources passed through supported outputs |

A resource preview describes configuration from code. Provider defaults, generated IDs and the resource's actual cloud state are outside this view. The module header shows existing outputs; it does not list every resource in the module.

In a `variable` declaration, the header, the `type` constraint and a selection of the whole block show the variable's value for the current inputs and module context. You can inspect an expression inside `default` separately; its result may differ from the value overridden by tfvars.

For a direct reference whose value cannot be calculated, the preview may show its target, for example `<reference: azurerm_route_table.this["management"].id>`. A locally known public name can appear beside it. That tells you where the reference leads without inventing an ID.

Whole-resource expressions still require a complete provider shape. A module preview can therefore show configured fields while `jsonencode(module.network.whole_resource)` remains unavailable. Configuration previews do not turn partial objects into complete Terraform values.

## When a value is incomplete

| Status | Meaning |
|---|---|
| `known` | The value described by this preview is known |
| `partial` | Some parts are known and some are unresolved |
| `unknown` | The Terraform value cannot be known yet |
| `unavailable` | An expression error or a limitation of this extension prevents calculation |

The panel shows the reason and the affected path. A missing variable, an invalid expression and an unsupported function need different fixes. Without provider schema information, a field may be unavailable even if Terraform could evaluate it with that information. A field named `id` is not assumed to be a known string.

An error outside the inspected expression's dependencies should not block its result. Large values are shortened for display and marked as truncated; hidden elements still contribute to the reported status. When the engine cannot trace an unresolved value precisely through a transformation, the result says so.

## Choose inputs and context

The extension automatically reads root-level `terraform.tfvars`, `terraform.tfvars.json` and ordered `*.auto.tfvars` / `*.auto.tfvars.json` files. Other files must be selected explicitly. Choosing a tfvars directory changes the file picker, not the active environment. The default directory is `environment` under the root module.

The selected file is remembered locally for each root module. In a trusted workspace you can explicitly select one local tfvars file outside the workspace. This does not grant access to its entire directory or extend access for `file()` and `templatefile()`.

Profiles combine named sets of inputs. For example:

```json
{
  "valuescope.profiles": [
    {
      "id": "lab",
      "name": "Local lab",
      "varFiles": ["environment/lab.tfvars"],
      "vars": {
        "environment": "lab",
        "zones": "[\"a\", \"b\"]"
      }
    }
  ]
}
```

Input precedence is: defaults, configured `TF_VAR_*` inputs, automatic root variable files, profile files in order, then explicit profile `vars`. Strings use plain text; collections use HCL text. Use **Set Secret Value** for protected inputs. Store only secret names in profile settings.

If a module is called more than once, select the root module, module context and instance you want to inspect. Child inputs are evaluated in the calling instance's context. The preview follows local modules; it does not download remote modules.

## Language and editor integration

Use **Language** in the panel to choose English, Polish or automatic selection. The choice is stored locally. The base setting is `valuescope.language`: `auto`, `en` or `pl`. Automatic selection uses Polish for a Polish VS Code locale and English otherwise.

Changing language keeps the current result, input file and pin. **About** opens this guide in the selected language. Command titles and Settings descriptions follow VS Code's own display language; the panel can use a different language. Values, HCL syntax and raw engine diagnostics are preserved.

The extension works alongside your Terraform language extension. It does not change file associations, syntax colours or formatting. It recognises `.tf`, `.tfvars`, `.tf.json` and `.tfvars.json` filenames as well as Terraform language IDs. A language companion supplies completion and syntax highlighting.

## Complete registered function catalogue

The registry contains **118 names: 97 locally implemented functions, 4 deliberately deferred functions and 17 explicitly unsupported functions**. These are not 118 fully supported Terraform functions. Implementation within a tested subset is not exhaustive compatibility with every Terraform version, provider or possible input.

### Locally implemented: 97

| Category | Functions |
|---|---|
| Numeric — 9 | `abs`, `ceil`, `floor`, `log`, `max`, `min`, `parseint`, `pow`, `signum` |
| Strings and patterns — 21 | `chomp`, `endswith`, `format`, `formatlist`, `indent`, `join`, `lower`, `regex`, `regexall`, `replace`, `split`, `startswith`, `strcontains`, `strrev`, `substr`, `title`, `trim`, `trimprefix`, `trimspace`, `trimsuffix`, `upper` |
| Collections and selection — 28 | `alltrue`, `anytrue`, `chunklist`, `coalesce`, `coalescelist`, `compact`, `concat`, `contains`, `distinct`, `element`, `flatten`, `index`, `keys`, `length`, `lookup`, `merge`, `one`, `range`, `reverse`, `setintersection`, `setproduct`, `setsubtract`, `setunion`, `slice`, `sort`, `transpose`, `values`, `zipmap` |
| Type conversion — 6 | `tobool`, `tolist`, `tomap`, `tonumber`, `toset`, `tostring` |
| Structured text — 3 | `csvdecode`, `jsondecode`, `jsonencode` |
| Text encoding — 3 | `base64decode`, `base64encode`, `urlencode` |
| Hashing — 6 | `base64sha256`, `base64sha512`, `md5`, `sha1`, `sha256`, `sha512` |
| Explicit date/time inputs — 2 | `formatdate`, `timeadd` |
| Local files and templates — 10 | `file`, `filebase64`, `filebase64sha256`, `filebase64sha512`, `fileexists`, `filemd5`, `filesha1`, `filesha256`, `filesha512`, `templatefile` |
| Paths — 3 | `abspath`, `basename`, `dirname` |
| Error handling — 2 | `can`, `try` |
| Sensitivity/ephemeral values — 4 | `ephemeralasnull`, `issensitive`, `nonsensitive`, `sensitive` |

Qualifications:

- `try`/`can` distinguish catchable dynamic errors from static errors and tool limitations. A missing schema or unsupported feature is not silently converted to a successful fallback.
- `file`/`templatefile` require UTF-8; `filebase64` supports binary content. Reads require a trusted workspace, an allowed path and a file of at most 4 MiB. They do not write data.
- Relative file paths and `abspath` use the root module as evaluation base. `path.cwd` uses launch-directory context, configurable by a profile. `path.root`/`path.module` preserve the tested relative Terraform-style representation.
- `templatefile` uses supplied variables and the available registry. Recursive template calls are unsupported.
- `range` follows the library's 1,024-element limit. A known `setproduct` result is bounded to 10,000 combinations.
- Structural wrappers preserve known leaves and origin paths where supported. `formatlist`, `split`, regex/decode operations, `setproduct` and `templatefile` can require explicit attribution fallback for unresolved inputs.
- `nonsensitive` is not a general secret-reveal permission. Declaration marks and recognizable credential-format redaction still apply at presentation boundaries.

### Deliberately deferred: 4

| Functions | Behavior |
|---|---|
| `timestamp`, `uuid`, `bcrypt` | Unknown with an `impure-function` reason; no invented timestamp, identifier or hash |
| `plantimestamp` | Unknown with a `plan-time` reason; no plan runs |

### Explicitly unsupported: 17

`base64gzip`, `cidrcontains`, `cidrhost`, `cidrnetmask`, `cidrsubnet`, `cidrsubnets`, `fileset`, `matchkeys`, `pathexpand`, `rsadecrypt`, `templatestring`, `textdecodebase64`, `textencodebase64`, `timecmp`, `uuidv5`, `yamldecode`, `yamlencode`.

These produce an explicit tool limitation. Provider-defined functions are not executed. Unregistered names are not supported merely because they are valid in some Terraform version.

## Commands

IDs are stable across languages. Palette titles follow VS Code's locale; descriptions below name the actions.

| Action | Command ID |
|---|---|
| Open results panel | `valuescope.openPanel` |
| Evaluate expression/selection | `valuescope.evaluateExpression` |
| Refresh result | `valuescope.refresh` |
| Select tfvars file | `valuescope.selectTfvars` |
| Select tfvars directory | `valuescope.selectTfvarsDirectory` |
| Select profile | `valuescope.selectProfile` |
| Select root module | `valuescope.selectRootModule` |
| Select module scope | `valuescope.pinScope` |
| Select resource/module instance | `valuescope.selectInstance` |
| Set secret value | `valuescope.setSecret` |
| Change language | `valuescope.selectLanguage` |
| About / documentation | `valuescope.openAbout` |
| Restart engine | `valuescope.restartEngine` |
| Show logs | `valuescope.showLogs` |

## Settings

| Setting | Default | Purpose |
|---|---|---|
| `valuescope.language` | `auto` | `auto`, `en` or `pl`; local picker choice takes precedence |
| `valuescope.tfvars.directory` | `environment` | Picker directory, not an automatic input loader |
| `valuescope.profiles` | `[]` | Named profiles and variable inputs |
| `valuescope.inheritTfVarEnv` | `false` | Opt in to VS Code process `TF_VAR_*` inputs in trusted workspaces |
| `valuescope.codeLens.enabled` | `true` | Explicit preview actions |
| `valuescope.highlight.enabled` | `true` | Subtle source range outline/background |
| `valuescope.compat` | `auto` | Assumed 1.16.0 subset, or explicit `1.16.0`; other values unavailable |
| `valuescope.limits.hoverDeadlineMs` | `2000` | Cooperative deadline; engine caps it at 5,000 ms |
| `valuescope.terraform.path` | empty | Reserved for a future explicit CLI workflow, not live evaluation |
| `valuescope.trace.server` | `off` | Reserved trace; current logging uses event codes, not RPC payloads |

## Local calculation and privacy

The engine calculates values on your computer. Previewing code does not run Terraform, a provider, a backend or a cloud query. Your code, tfvars and results stay on your computer. The extension reads your Terraform files; input selections and interface preferences are stored separately in VS Code.

Secret inputs use VS Code SecretStorage. Values marked sensitive or ephemeral are protected in the displayed result and reference details. Recognisable credential formats are also masked, but patterns cannot identify every secret. The copy action copies the displayed, redacted value. Logs contain event codes rather than expressions or raw RPC messages.

File access is restricted in untrusted workspaces. The bundled engine checksum and version handshake detect changed or mismatched files; they do not replace publisher signing.

## Limits and unsupported workflows

| Area | Current boundary |
|---|---|
| External providers | No schema service, provider defaults/normalization, provider functions or API reads |
| State and plans | No state/saved-plan enrichment or cloud-state inspection |
| Modules | Local sources only; no automatic remote installation; header preview describes existing outputs |
| Whole external resources | Full values still require schema; configuration is a separate presentation |
| Resource-field loops | Direct repeated resource/data collections and concrete fields; whole aliases and dynamic field choice remain conservative in ordinary expressions |
| Dynamic configuration | Supported native-HCL expansion; no schema-dependent block labels; tuples are presentation shapes |
| Compatibility | Tested subset referenced to Terraform 1.16.0, not all Terraform 1.x or guaranteed OpenTofu compatibility |
| Workspace index | 8 MiB/file, 64 MiB total, 10,000 configuration files, 200,000 visited entries; incomplete indexing is reported |
| Evaluation | 20,000 dependency nodes, 1,000 instances/block, module depth 32 |
| Configuration preview | Shared expansion budget 1,000 and depth 64; complex previews can hit this before the instance limit |
| Presentation | Up to 200 visible elements/collection, 5,000 rendered nodes, depth 64, 65,536-byte value text; truncation is marked |
| Other workflows | No profile comparison or interactive paging |

The deadline is cooperative. An extreme HCL expression can require an engine restart; this is not a complete sandbox against malicious workloads. Outlines may repeat an edge when a very long boundary line wraps, a limitation of VS Code's stable decoration API.

The evaluator is not restricted to Azure resource names: it works with HCL values and configured arguments. Azure examples reflect the workflows exercised most directly, **not comprehensive certification of Azure, AWS, Google Cloud or another provider**.

## Troubleshooting

| Symptom | Check |
|---|---|
| Required variable unavailable | Select the right tfvars/profile; check root and child inputs |
| `schema-not-loaded` | Inspect a configured argument or header; full provider values intentionally remain unavailable |
| ID or `time_static` timestamp unresolved | Provider-dependent value; tfvars cannot manufacture it |
| No `each`/`count` context | Select source inside the block and choose its scope/instance |
| Header differs from expression | Check the configuration-only label; they describe different things |
| Truncated result | Inspect a smaller subexpression; invisible elements may still exist |
| File access denied | Check trust/path; explicitly select an external tfvars file, not its directory |
| No colors or completion | Keep a Terraform language companion; Live Values & Results for Terraform is not a language extension |
| Stale result/engine stopped | Refresh, inspect safe event codes, then Restart Engine if needed |
| Linux: disk edits do not update previews, or watcher logs show `EMFILE` | Check [inotify limits](#linux-inotify); VS Code may be unable to start a file watcher |
| Panel/title languages differ | Runtime override controls Live Values & Results for Terraform UI; static command titles follow VS Code |

## Linux: inotify

`inotify` delivers Linux file and directory change notifications. The `fs.inotify.max_user_instances` limit is shared by applications running under the same user account. A value of 128 means 128 instances, each able to watch many paths. The separate `fs.inotify.max_user_watches` setting limits watched paths. [Linux documentation](https://man7.org/linux/man-pages/man7/inotify.7.html).

The extension uses VS Code file events to detect changes to Terraform files, selected tfvars and dependencies of `file()` or `templatefile()`. If VS Code cannot start the required watcher, a disk edit can leave the preview showing an earlier result. Typing in an open Terraform document may still update it through editor events, so that alone does not prove disk watching works.

An `EMFILE` error in file-watcher logs can mean the instance limit is exhausted; it can also mean a process has exhausted its file descriptors. Check the logs before attributing every stale result to inotify. [Error definitions](https://man7.org/linux/man-pages/man2/inotify_init.2.html).

If your instance limit is 128 and several applications are using file watchers, consider increasing it to **1024**. This resolved watcher failures in our Linux tests. The value is a starting point, not a requirement for every computer. Keep a higher existing limit.

Check your settings and note the original value:

```bash
sysctl fs.inotify.max_user_instances fs.inotify.max_user_watches
```

If the instance limit is lower than 1024, an administrator can change it for the current boot:

```bash
sudo sysctl -w fs.inotify.max_user_instances=1024
```

This command does not save a boot-time setting. After a temporary test, restore your recorded value with `sudo sysctl -w fs.inotify.max_user_instances=VALUE`. [sysctl commands](https://man7.org/linux/man-pages/man8/sysctl.8.html).

To keep 1024 after reboot on a system using `sysctl.d`, open the local configuration file:

```bash
sudoedit /etc/sysctl.d/90-live-values-results-inotify.conf
```

Add or update this line, then save:

```ini
fs.inotify.max_user_instances = 1024
```

Apply that file and verify the active value:

```bash
sudo sysctl -p /etc/sysctl.d/90-live-values-results-inotify.conf
sysctl fs.inotify.max_user_instances
```

Other system settings can override this value at boot; verify it after restarting Linux. See [sysctl.d configuration](https://man7.org/linux/man-pages/man5/sysctl.d.5.html).

Restart VS Code after changing the limit and check a preview after editing a dependency on disk. The extension does not change system limits automatically.

## Licenses

From version 0.0.12, the original application is distributed under a [proprietary license](LICENSE.txt). You may use official releases free of charge for personal and commercial work; modification and redistribution of the original application are restricted as stated in that license.

Third-party libraries retain their own licenses: [notices](THIRD_PARTY_NOTICES.txt) and [source availability](SOURCE_AVAILABILITY.txt). The package includes the unmodified HCL source archive required for its MPL-2.0 components. The application development sources are private.

Live Values & Results for Terraform is not affiliated with, endorsed by or sponsored by HashiCorp. Terraform is a HashiCorp trademark. Compatibility descriptions identify the language and do not imply an official relationship.
