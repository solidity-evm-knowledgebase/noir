# Noir

## Architecture

### Nargo

- CLI tool.
- Enables us to compile our circuits and execute them.
- noirup to install latest version of nargo
- nargo will compile our circuits to create ACIR, the intermediate representation used by the backend.
- Execute creates the witness (it will also compile the circuits)

### Barretenberg (backend)

- Using the backend, we can generate proofs and verify those proofs, by using the witness and ACIR files we generated.
- Verification can be done either offchain or onchain (via Verify smart contract).

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
