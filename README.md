# rustmailer-rest-cli

Generated CLI for the [RustMailer](https://rustmailer.com) REST API.

This wrapper is built from the OpenAPI spec embedded in RustMailer's public
ReDoc page at `https://rustmailer.com/redoc`. The documented local raw spec
endpoints currently return 404 on the public marketing site, so this repository
vendors the extracted spec at `wrappers/rustmailer-rest-cli/spec.json` for
repeatable regeneration.

## Install

```bash
pipx install rustmailer-rest-cli
```

The generated package defaults to a local RustMailer instance:

```bash
http://localhost:15630
```

Override it with:

```bash
export RUSTMAILER_REST_CLI_BASE_URL=http://your-rustmailer-host:15630
```

## Examples

### Verified Commands

These commands were run successfully before publishing `0.1.0`.

Container smoke test:

```bash
docker run --rm --platform linux/amd64 -p 15630:15630 rustmailer/rustmailer:latest
RUSTMAILER_REST_CLI_BASE_URL=http://localhost:15630 \
  rustmailer-rest-cli system get-overview --output-format json
```

Result marker: the local container returned system overview JSON.

Other read-only operator checks:

```bash
rustmailer-rest-cli system get-overview --output-format table
rustmailer-rest-cli account list --output-format table
rustmailer-rest-cli mailbox list-mailboxes --account-id 1 --output-format table
rustmailer-rest-cli message list --account-id 1 --mailbox INBOX --output-format table
```

## Notes

This is an unofficial community wrapper. Be careful with send, delete, mailbox,
and account mutation commands on real email infrastructure.
