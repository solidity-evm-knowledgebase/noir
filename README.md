# Noir

## Architecture

### Nargo

- CLI tool.
- Enables us to compile our circuits and execute them.
- noirup to install latest version of nargo
- nargo will compile our circuits to create ACIR, the intermediate representation used by the backend.
- Execute creates the witness (it will also compile the circuits)

#### Commands
- `nargo check`: Check the Noir code. Are you using your variables and types correctly? It checks any dependencies being used, and checks all of the functions and circuits are well formed. (without having to compile/generate proofs). It will create `Prover.toml` file.
- `nargo compile`: Will generate the ACIR file without actually creating a proof.
- `nargo execute`: Will compile into ACIR, execute the circuits with the inputs, and compute a witness.

### Barretenberg (backend)

- Using the backend, we can generate proofs and verify those proofs, by using the witness and ACIR files we generated.
- Verification can be done either offchain or onchain (via Verify smart contract).

#### Commands:

- `bb prove -b ./target/simple_circuit.json -w ./target/simple_circuit -o ./target`: Generate the proof. -b is path to ACIR file, -w is path to witness file, -o target path for the proof. By default, it will use ultra_honk scheme.
- `bb write_vk -b ./target/simple_circuit.json -o ./target`: Will generate a verification key. Small cryptographic object that allows the verifier to check the validity of a proof without having to rerun the full computations. It's generated from the ACIR.
- `bb verify -k ./target/vk -p ./target/proof`: Verify proof using the verification key. 

## Project Types and Layout

### Nargo.toml

- contains all environment options for the project
- package section with name of project, type (can be bin, lib or contract), compiler version, main entrypoint...
- dependencies section

### Src folder

- main.nr is the main entrypoint to our project

## Data Types

Inputs by default are private in Noir. To make them public use the `pub` keyword. When we verify our proofs, we provide the public inputs along with the proofs.

### Variables Types

- Most common is `Field` type. Essentially, it's an integer with a maximum value defined by the field modulur (or field size). Supports integer arithmetic.
- The exception to use Integers instead of Fields is when we have something related to ordering, like `greater than` and `less than`.

## Depencies

- To use a dependecy, add it under dependencies in the Nargo.toml file like this:
```toml
[dependencies]
ecrecover = {tag = "v0.8.0", git = "https://github.com/colinnielsen/ecrecover-noir"}
```

- Then you can use it in the circuit by using the `use` kewyword and specifying `dep` like this:
```noir
use dep::ecrecover;
```
