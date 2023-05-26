# Doppler Secrets Buildkite Plugin

[![Build status](https://img.shields.io/github/actions/workflow/status/muhlba91/doppler-secrets-buildkite-plugin/pipeline?style=for-the-badge)](https://github.com/muhlba91/doppler-secrets-buildkite-plugin/actions/workflows/pipeline.yml)
[![Release](https://img.shields.io/github/v/release/muhlba91/doppler-secrets-buildkite-plugin?sort=semver&style=for-the-badge)](https://github.com/muhlba91/doppler-secrets-buildkite-plugin/releases)
[![Release date](https://img.shields.io/github/release-date/muhlba91/doppler-secrets-buildkite-plugin?style=for-the-badge)](https://github.com/muhlba91/doppler-secrets-buildkite-plugin/releases)
[![License](https://img.shields.io/github/license/muhlba91/doppler-secrets-buildkite-plugin?style=for-the-badge)](LICENSE.md)
<a href="https://www.buymeacoffee.com/muhlba91" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="28" width="150"></a>

A [Buildkite plugin](https://buildkite.com/docs/agent/v3/plugins) for exposing secrets from [Doppler](http://doppler.com) to your build steps.

**Plugin State**: Beta

---

## Requirements

The [`doppler` CLI](https://docs.doppler.com/docs/cli#installation) must be installed!

## Examples

The following pipeline uses a [Service Token](https://docs.doppler.com/docs/service-tokens) to set all secrets as environment variables.
The Service Token is set on the runner through the enviroment variable [`DOPPLER_TOKEN`](https://docs.doppler.com/docs/service-tokens#option-2-the-doppler_token-environment-variable).

```yml
steps:
  - command: "echo $MY_SECRET"
    plugins:
      - muhlba91/doppler-secrets#v0.0.0
```

You can also directly specify the token (insecure!):

```yml
steps:
  - command: "echo $MY_SECRET"
    plugins:
      - muhlba91/doppler-secrets#v0.0.0:
          token: dp.XXX
```

Personal Tokens are also supported but require setting `project` and `config`:

```yaml
steps:
  - command: "echo $MY_SECRET"
    plugins:
      - muhlba91/doppler-secrets#v0.0.0:
          project: project
          project-config: prod
```

If you want to control what secrets are being exposed you can specify the `variables` parameter:

```yml
steps:
  - command: "echo $MY_SECRET"
    plugins:
      - muhlba91/doppler-secrets#v0.0.0:
          secrets:
            - MY_SECRET
```

### Warning

The plugin does not perform variable sanitation!

---

## Configuration

### Optional

#### `token` (optional, string)

The Buildkite token to use (Service Token, or Personal Token).

Example: `dp.XXX`

### `project` (optional, string)

The Doppler project to read the secrets from.

***Required*** for Personal Tokens!

Example: `project`

### `project-config` (optional, string)

The Doppler configuration within the set project to read the secrets from.

***Required*** for Personal Tokens!

Example: `prod`

### `secrets` (optional, array)

Sets the secrets to be read as environment variables.

***Attention:*** at the moment, this forces multiple calls to Doppler, and incurs performance penalty!

Example: `[ "MY_SECRET1", "MY_SECRET2" ]`

---

## License

MIT (see [LICENSE](LICENSE.md))

## Supporting

If you enjoy the application and want to support my efforts, please feel free to buy me a coffe. :)

<a href="https://www.buymeacoffee.com/muhlba91" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="75" width="300"></a>
