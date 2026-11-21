<img src="assets/logo.png" width="112" height="112" alt="TokenBucket logo">

# TokenBucket

Refill a rate bucket up to its burst capacity. This Blyx library is part of the queues and messaging collection.

Charging a delayed request immediately can remove capacity from unrelated work. Return the wait separately from the updated balance. [IETF RFC 2697, token buckets](https://www.rfc-editor.org/rfc/rfc2697)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-tokenbucket.git
cd blyx-tokenbucket
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-tokenbucket) · [Package page](https://www.blyx-lang.space/packages/tokenbucket) · [Handbook](https://doc.blyx-lang.space/guide/petrel)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-tokenbucket.git vendor/tokenbucket
```

```blyx
use vendor::tokenbucket::tokenbucket;

fn main() {
    let tokens = 2.0;
    let capacity = 10.0;
    let rate = 3.0;
    let elapsed = 4.0;
    let result = tokenbucket_refill(tokens, capacity, rate, elapsed);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
10
4
```

## API

`tokenbucket_refill(tokens, capacity, rate, elapsed)`

Returns [available tokens, refill discarded at capacity]. Tokens, capacity and rate use the same work unit. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| tokens | A nonnegative finite number |
| capacity | A positive finite number |
| rate | A positive finite number |
| elapsed | A nonnegative finite number |

## In use

[Petrel](https://github.com/Rahulchaube1/blyx-petrel) uses this module to admit an immediate charge or report the wait a request can afford.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-tokenbucket/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
