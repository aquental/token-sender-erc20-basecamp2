## setup

### scarb _2.6.3_ [docs](https://docs.swmansion.com/scarb/download.html)

```sh
asdf install scarb 2.6.3
asdf global scarb 2.6.3
```

### starknet-foundry _0.22.0_ [docs](https://foundry-rs.github.io/starknet-foundry/getting-started/installation.html)

```sh
asdf plugin add starknet-foundry
asdf install starknet-foundry 0.22.0
asdf global starknet-foundry 0.22.0
```

### openzeppelin _0.10.0_

```text
[dependencies]
openzeppelin = { git = "https://github.com/openzeppelin/cairo-contracts", tag = "v0.10.0"}
```

---

```sh
scarb build
snforge test
```
